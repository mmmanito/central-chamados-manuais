# Indicadores e TVs

## Grafana (5.1.0-rc8)

Os indicadores e as TVs voltaram para o **Grafana**, como antes da 5.0, agora lendo **só o banco da Central** (o
banco do GLPI saiu na virada). Com o endereço do Grafana configurado (o instalador do Grafana preenche sozinho; também
em **Situação › Telas de TV › Endereço do Grafana**), a tela **Indicadores** e os links das TVs mostram o Grafana. Sem
o endereço, continuam as telas próprias da Central (seções abaixo).

**Dashboards** (pasta *Central de chamados* do Grafana; gerados por `grafana/gerador/gerar_dashboards.py`):

| Dashboard | Para quê | Período | Filtros |
| --- | --- | --- | --- |
| **Operacional** | O atendimento agora: números (com Parados, Esperando compra e Sem quem pediu), distribuição (por unidade, idade, carga por técnico), a equipe na semana; abaixo, hoje hora a hora e terceiros | hoje (30 s) | Unidade, Equipe |
| **Gerencial** | O período comparado ao anterior: 8 números com a variação, fluxo (entra × sai × estoque) e vazão, semanas com projeção, mapa dia × hora, Pareto dos assuntos, área × anterior, unidades (volume × espera e mapa unidade × área), equipe, recorrência, canais e cancelamentos | 30 dias (ajustável) | Unidade, Equipe |
| **TV operacional · Compras** | Pedidos por etapa (cartões), o que trava o atendimento e o que chega | agora | — |
| **Vistoria técnica** | Saúde da TI nas unidades pelas vistorias | 6 meses | — |

**5.6.0 (repaginado em 14/11/2026).** Saíram do Operacional os Comunicados, o Em campo, a pizza por área e a Fila (sem
triagem, quem abre o chamado já é o técnico dele); do Gerencial, o 1º atendimento, o tempo de solução, a satisfação, os
resolvidos de primeira, as reaberturas, as visitas técnicas e os comunicados. Os painéis continuam no gerador, para uma
instalação que use essas funções. As regras de sempre valem: subchamado não conta, cancelado não conta como
solucionado, a solução conta para quem a registrou e "aguardando terceiros" é o pendente com fornecedor.

**Como a equipe é medida** (o mesmo texto está no manual de Atendimento, capítulo *Como a equipe é medida*):

- **Em dia / Parados:** a regra dos *Chamados parados* do painel da liderança. Chamado com técnico em andamento (5.6.3: os pendentes ficam de fora por enquanto)
  sem nenhum registro do técnico atribuído (acompanhamento, tarefa, solução ou mudança de situação); contam os dias
  úteis inteiros: 1 = amarelo, 2 ou mais = vermelho; o que espera uma compra travada não conta. O Grafana não sabe
  contar dias úteis com o expediente e os feriados: a Central grava a situação de cada chamado na tabela
  `painel_parados` a cada minuto (laço das tarefas do atendimento) e o Grafana lê dali. Os números batem com o painel.
- **Solucionados na semana:** de domingo até agora, para quem registrou a solução.
- **Quem saiu da equipe** (conta desativada na Central, em Equipe técnica) fica fora do ranking, do registro durante e
  do desempenho; onde ainda tem chamado com ele (Em dia, carga), aparece como "(inativo)" para alguém redistribuir.
- **Registro durante o atendimento:** dos solucionados que não foram resolvidos no mesmo dia em que foram abertos,
  quantos tiveram acompanhamento ou tarefa do técnico antes da solução.
- **Compras:** pedido parado na etapa a partir de 5 dias corridos (vermelho; amarelo a partir de 3); prazo de
  fornecedor conta fim de semana.

**As TVs, abertas direto no Grafana** (sem o link da Central), com o usuário **tv** (senha em `GRAFANA_TV_PASSWORD`;
a sessão dura até 90 dias):

```text
TV operacional (Operacional, Operacional e Compras, 30 s cada):
https://NOME/grafana/playlists/play/central-tv-operacional?kiosk&_dash.hideTimePicker&_dash.hideVariables&_dash.hideLinks
TV gerencial (5.6.2: duas telas, Atendimento e Compras e equipe, 1 min cada):
https://NOME/grafana/playlists/play/central-tv-gerencial?kiosk&_dash.hideTimePicker&_dash.hideVariables&_dash.hideLinks
```

**A TV gerencial (5.6.2).** Duas telas que alternam a cada minuto, com os 8 números do período (30 dias) no alto,
iguais nas duas, e 9 gráficos embaixo (2 grandes, 3 e 4). Nada repete a TV operacional.

- *Tela 1, atendimento:* entradas × saídas e o estoque; semanas com a projeção; Pareto dos assuntos; por onde chega →
  área → como terminou; unidades volume × espera; chamados por dia (calendário, desde o início do histórico, até 16
  semanas); quando a demanda chega (dia × hora); por área, este período × anterior; recorrência na mesma unidade.
- *Tela 2, compras e equipe:* linha do tempo dos 8 pedidos mais recentes (3 semanas), com o valor de cada um;
  compras por mês em R$ mil (comprado × cancelado ou recusado, 6 meses, com o total na legenda); funil das compras
  (pedidos de 90 dias: quantos e quanto chegaram a cada etapa); onde a compra demora (média de dias corridos em cada
  etapa); a compra atrasa o atendimento? (mediana de dias até solucionar, com e sem subchamado de Compra, 90 dias);
  quanto tempo leva um pedido (cada pedido entregue e a mediana do mês, 6 meses); solucionados por semana por técnico;
  o que cada técnico atende (por área); cancelamentos por motivo.
- *Valor de um pedido:* a cotação escolhida (ou, sem escolha, a mais barata ativa) mais o frete.

O Operacional até a seção *Equipe na semana* cabe numa tela 1920 × 1080 sem rolar; o que vem abaixo é para o
computador. Pelo link da Central (Situação › Telas de TV) a TV operacional continua com o aviso com som de cada chamado
novo e o registro do último contato; aberta direto no Grafana, não.

**Plugins (5.6.0; na 5.6.2, também o calendário, o Sankey, o mapa dia × hora e o funil da TV gerencial).** Três painéis usam plugins, mantidos pela Grafana Labs: **Business Text** (os cartões dos pedidos
por etapa) e **Business Charts**/Apache ECharts (o Pareto e as unidades volume × espera). O `./grafana/instalar.sh`
instala os dois com a **versão fixa** (`PLUGINS_FIXOS`) uma vez, no volume do Grafana; o Grafana não baixa nem atualiza
nada sozinho ao subir (`GF_PLUGINS_PREINSTALL_DISABLED`), porque, com a instalação automática, sem internet ele nem
subia. Sem conseguir instalar (sem internet), ou com `GRAFANA_PLUGINS=nao` no `grafana/.env`, esses painéis usam as
versões nativas do Grafana (uma tabela de pedidos por etapa, barras com o acumulado e uma tabela das unidades). Para
mudar: edite o `grafana/.env` e rode `./grafana/instalar.sh`.

**TVs pelo link da Central.** O link de Situação › Telas de TV continua valendo: mostra a mesma playlist em tela
cheia, com o aviso de chamado novo por cima.

**Computador.** **Indicadores** mostra o Gerencial, o Operacional e a Vistoria técnica dentro da Central (abas no
topo), com **Abrir no Grafana** e o **CSV** e o **PDF** de sempre (últimos 30 dias). Desde a 5.5.1, quem está logado
na Central entra direto (veja abaixo); sem o login da Central ligado, cada um entra com o seu usuário do Grafana,
criado pelo **admin** (Administração › Usuários). O antigo usuário **gestao** saiu na 5.5.1: o instalador o apaga.

**Instalação e atualização.** O `./atualizar.sh` reinstala o Grafana quando o `instalacao.conf` tem `GRAFANA=pacote`
(o `./grafana/instalar.sh` rodado à parte marca isso). O instalador da Central cria o usuário **somente leitura**
`grafana` no banco (`python -m app.cli grafana-leitura`): ele lê os chamados, as unidades, os setores, os grupos, as
categorias, os técnicos (só nome e número), os fornecedores (só nome), a chegada e saída, os comunicados, as vistorias
e, de Compras, os pedidos, a fila, o total e o frete das cotações e o histórico das etapas (5.6.2; sem pagamentos);
não lê senhas, telefones nem a Personalização (só a triagem, pela visão `grafana_config`). O instalador do Grafana
cria as playlists (`grafana/playlists.py`), deixa o Grafana em português, confere as consultas no banco
(`grafana/testar_consultas.py`) e informa o endereço à Central. Com o Grafana em HTTPS, o login dele vale também dentro
das telas da Central abertas por outro endereço (ex.: o painel pelo IP da rede).

### O login da Central no Grafana (5.5.1)

Com o Grafana atrás do Nginx da própria Central (`https://NOME/grafana`), **quem está logado na Central entra direto
no Grafana**, sem outra senha: o **Gestor de TI** e o **Administrador** como **Admin**; os demais usuários do painel
(técnicos, Compras, Estoque...) como **Viewer**. O usuário do Grafana é criado no primeiro acesso, com o mesmo login e
o nome da Central, e o papel acompanha o da Central. Quem só usa o aplicativo (lojas, gerentes, fornecedores) não entra
por aí.

- **Sem sessão na Central** (as TVs, outro navegador), aparece o login do próprio Grafana: o **tv** (senha
  `GRAFANA_TV_PASSWORD` no `grafana/.env`; para uma senha simples, troque ali e rode `./grafana/instalar.sh`) e o
  **admin** de emergência (`GRAFANA_ADMIN_PASSWORD`). Os logins `admin`, `tv` e `gestao` da Central não passam pelo
  login automático: os dois primeiros são contas do próprio Grafana e o `gestao` foi conta dele até a 5.5.1.
- **Como funciona:** antes de cada página do `/grafana`, o Nginx pergunta à Central (`/central/grafana/sessao`) quem
  está logado e manda a resposta nos cabeçalhos `X-WEBAUTH-*` (o modo *auth proxy* do Grafana). O que o navegador
  mandar nesses cabeçalhos é sempre trocado. A consulta não renova a sessão da Central (o tempo de inatividade continua
  valendo) e, com a Central fora do ar, o Grafana mostra o login dele.
- **A porta 3000 fica presa ao servidor** (`GRAFANA_PORTA=127.0.0.1:3000`): da rede, o Grafana só responde pelo
  `https://NOME/grafana`. Antes, `IP:3000` abria direto; quem usava esse endereço passa a usar o do domínio.
- **Ligar e desligar:** o `./grafana/instalar.sh` liga sozinho quando o Grafana fica atrás do Nginx da Central
  (`GRAFANA_LOGIN_CENTRAL=true`). Com um servidor web que já existia (`APP_PROXY=existente`) ou sem HTTPS, continua só o
  login do Grafana. Para desligar: `GRAFANA_LOGIN_CENTRAL=false ./grafana/instalar.sh`.

## Telas próprias (sem o Grafana)

## Indicadores do atendimento (Painéis › Atendimento)

Os gráficos (5.1.0-rc4) seguem o estilo do Grafana: passe o mouse para ver os números de cada ponto, use a roda do
mouse no gráfico de entrada e saída para aproximar um trecho, e escolha **Atualizar a cada 1 ou 5 minutos** para
deixar o painel aberto numa tela. Eles usam o Apache ECharts, servido pela própria Central (funciona sem internet).

Abre pelo botão **Indicadores**, em Atendimento (Gestor de TI, Líder técnico e Administrador). No topo, os atalhos de
período (7, 30 e 90 dias, este mês, mês passado); em **Período e filtros**, as datas, a unidade, o setor, o grupo, o
técnico e a categoria. O painel responde, em ordem, às perguntas do dia a dia:

- **Como foi o período**: quantos chegaram e quantos foram solucionados, o SLA de solução cumprido e a avaliação média,
  com a comparação com o período anterior de mesmo tamanho; e o gráfico de **entrada e saída** (por dia, os que chegaram
  para cima, os solucionados para baixo e a fila acumulada).
- **O que está aberto agora**: na fila sem técnico, prazo estourado, perto de estourar, críticos; a **fila de cada
  grupo** por situação; **há quanto tempo** estão abertos e os mais antigos.
- **Estamos rápidos?**: até o 1º atendimento e até a solução, com a média, a metade em até e 90% em até; em quanto tempo
  os chamados foram solucionados (faixas); as soluções recusadas pelo usuário.
- **De onde vêm os chamados**: por unidade e por categoria (com a parte de cada uma), por tipo, por canal e por grupo.
- **Quando chegam**: o mapa de dia da semana × hora (ajuda a planejar o expediente e o sobreaviso).
- **Quem atende**: por técnico, os solucionados, o tempo médio e a avaliação (a solução conta para quem a registrou);
  **o que os usuários acham**: as estrelas e os comentários mais recentes.
- **Fornecedores**: o tempo esperando cada fornecedor e o gasto com serviços no período.
- **Como no painel gerencial do Grafana** (5.1.0-rc4): incidentes, requisições e ordens de trabalho; resolvidos de
  primeira (sem pendência nem recusa); reaberturas (soluções recusadas); quantos dependeram de terceiros; o registro
  completo (categoria, unidade e solução descrita); a tendência por semana (12 semanas); o que mais quebra (incidentes) e
  o que mais se pede (requisições) por categoria, e por área; o mapa de calor unidade × área e a satisfação por unidade;
  o desempenho por técnico (solucionados, 1º atendimento, até a solução, avaliação, reaberturas, abertos com ele agora);
  aguardando terceiros (pendentes agora, tempo médio, o que mais fica pendente, os mais antigos); qualidade do registro
  (os incompletos e a recorrência do mesmo problema na mesma unidade); cancelamentos e os motivos; visitas técnicas e
  comunicados do período.
- **Baixar CSV** (para planilha) e **Baixar PDF** (para enviar).

Os painéis de **suprimentos** ficam em **Painéis** (com o módulo Estoque): Compras (o funil das etapas e quanto foi
comprado), Estoque (o parque, onde estão, idade, consumo, vistoria), Projeções (o que vem pela frente, o que vai faltar
ou vencer) e Terceiros (chamados esperando cada fornecedor e o desempenho de cada um). Mais em [Estoque](18-estoque.md).

## Telas de TV

Duas telas sem login, com os mesmos gráficos do painel, no tema escuro e com letras maiores para ler de longe: a
primeira linha fica fixa e as páginas de baixo giram a cada 20 segundos; os dados voltam a cada minuto. **Desde a
5.1.0-rc4 as TVs precisam de um navegador atual** (Chrome ou um navegador de Android TV recente): as TVs com navegador
antigo deixaram de ser atendidas, em troca dos gráficos.

- **Operacional** (agora): fixos, a fila sem técnico, o prazo estourado e perto de estourar (com o SLA ligado), os
  críticos e o total aberto; girando, a fila de cada grupo, os estourados e críticos, os mais antigos e a idade dos
  abertos.
- **Gerencial** (últimos 30 dias): fixos, chegaram, incidentes, solucionados, o SLA cumprido, em quanto tempo metade
  foi solucionada, os resolvidos de primeira, as reaberturas e a avaliação; girando (oito páginas), entrada e saída por
  dia, a tendência por semana, o que mais quebra e o que mais se pede, unidade × área e a satisfação por unidade, os
  técnicos, por unidade e por categoria, o mapa dia × hora, e os pendentes com fornecedor e a recorrência.

Os links estão em **Situação › Telas de TV**, com o **último contato** e o navegador de cada TV. O mesmo link vale
para todas as telas: se vazar, **Gerar novo link** (e abra o novo em cada TV).


## 5.1.0-rc7: os painéis escolhidos do Grafana

O Gestor de TI escolheu, no catálogo dos painéis do Grafana, o que vai em cada tela:

- **TV operacional ("Agora")**: fixos, em aberto, incidentes, requisições, na triagem (ou na fila das equipes, com a
  triagem desligada), aguardando terceiros, abertos há mais de 7 dias, abertos e solucionados hoje, em campo e
  comunicados; girando (quatro páginas), esperando atendimento e carga por técnico; em aberto por unidade, por área e a
  idade; hoje hora a hora e as últimas soluções; pendentes com terceiros, comunicados ativos e em campo agora.
- **TV gerencial (30 dias)**: fixos (duas linhas), chamados abertos, incidentes, requisições, solucionados,
  1º atendimento, tempo de solução, satisfação, resolvidos de primeira, reaberturas, dependeram de terceiros, pendentes
  agora, tempo médio pendente e cancelados; girando (oito páginas), chamados por semana e incidentes x requisições; o
  que mais quebra, o que mais se pede e por área; unidade × área e satisfação por unidade; desempenho e tempo médio por
  técnico; horários de pico e canal de abertura; o que mais fica pendente e o registro incompleto; recorrência e
  cancelamentos; horas e visitas técnicas.
- **Painel do computador**: "Agora" (a Operacional, com os filtros de unidade, grupo e técnico) e "Como foi o período"
  (a Gerencial, com o período escolhido), mais os comunicados do período.

Saíram das telas (não escolhidos): SLA de solução cumprido, prazo estourado, fila de cada grupo, faixas de solução,
entrada e saída por dia, estrelas e comentários, e fornecedores (tempo de espera e gasto). Os cálculos continuam no
sistema (CSV e PDF) e voltam às telas se o Gestor pedir.