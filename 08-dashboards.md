# Indicadores e TVs

## Grafana (5.1.0-rc8)

Os indicadores e as TVs voltaram para o **Grafana**, como antes da 5.0, agora lendo **só o banco da Central** (o
banco do GLPI saiu na virada). Com o endereço do Grafana configurado (o instalador do Grafana preenche sozinho; também
em **Situação › Telas de TV › Endereço do Grafana**), a tela **Indicadores** e os links das TVs mostram o Grafana. Sem
o endereço, continuam as telas próprias da Central (seções abaixo).

**Dashboards** (pasta *Central de chamados* do Grafana; gerados por `grafana/gerador/gerar_dashboards.py`):

| Dashboard | Para quê | Período | Filtros |
| --- | --- | --- | --- |
| **Operacional** | O atendimento agora: números, fila, carga por técnico, distribuição, hoje hora a hora, terceiros, campo | hoje (30 s) | Unidade, Equipe |
| **Gerencial** | O período: números com o ritmo diário, tendência de 12 semanas, o que mais quebra e se pede, unidades, equipe, ritmo, terceiros, qualidade do registro, cancelamentos, visitas e comunicados | 30 dias (ajustável) | Unidade, Equipe |
| **Vistoria técnica** | Saúde da TI nas unidades pelas vistorias | 6 meses | — |

Os painéis são os escolhidos no catálogo (códigos O1 a O21 e G1 a G38; ficaram de fora O9, O10, G10, G12 e G29 a G31)
e seguem as regras da Central: subchamado não conta, cancelado não conta como solucionado, a solução conta para quem a
registrou e "aguardando terceiros" é o pendente com fornecedor. As esperas aparecem em português ("1 d 4 h", "25 min")
com as cores de sempre (verde, amarelo em 15 min, laranja em 30, vermelho em 60; pendência em 1, 3 e 7 dias) e os
tempos médios em horas.

**TVs.** Cada TV abre o link da Central (Situação › Telas de TV), sem login na Central. A tela mostra o Grafana em tela
cheia, sem os controles, girando as páginas da playlist a cada 20 segundos: os números de cima ficam iguais em todas as
páginas e o resto muda (TV operacional: 4 páginas; TV gerencial: 8). Por cima, a Central mostra cada **chamado novo**
com som (incidente: alerta e a borda piscando em vermelho; requisição: toque suave), só na TV operacional. Toque uma vez
na tela para ligar o som e a tela cheia. Na primeira vez, o Grafana da TV pede o usuário **tv** (a senha fica no
`grafana/.env`, `GRAFANA_TV_PASSWORD`); a sessão dura 90 dias. Cada TV continua contando o último contato na Situação.

**Computador.** **Indicadores** mostra o Gerencial, o Operacional e a Vistoria técnica dentro da Central (abas no
topo), com **Abrir no Grafana** e o **CSV** e o **PDF** de sempre (últimos 30 dias). Se o Grafana pedir login, use o
usuário de cada um ou o **gestao** (`GRAFANA_GESTAO_PASSWORD`).

**Instalação e atualização.** O `./atualizar.sh` reinstala o Grafana quando o `instalacao.conf` tem `GRAFANA=pacote`
(o `./grafana/instalar.sh` rodado à parte marca isso). O instalador da Central cria o usuário **somente leitura**
`grafana` no banco (`python -m app.cli grafana-leitura`): ele lê os chamados, as unidades, os setores, os grupos, as
categorias, os técnicos (só nome e número), os fornecedores (só nome), a chegada e saída, os comunicados e as vistorias;
não lê senhas, telefones nem a Personalização (só a triagem, pela visão `grafana_config`). O instalador do Grafana
cria as playlists (`grafana/playlists.py`), deixa o Grafana em português, confere as consultas no banco
(`grafana/testar_consultas.py`) e informa o endereço à Central. Com o Grafana em HTTPS, o login dele vale também dentro
das telas da Central abertas por outro endereço (ex.: o painel pelo IP da rede).

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