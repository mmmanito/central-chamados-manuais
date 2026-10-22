# Relatórios e painéis

O menu **Relatórios e painéis** (5.2.0) junta tudo o que a Central mede. Cada pessoa vê só as áreas do seu papel:
Atendimento (Técnico, Triagem, Líder, Gestor de TI), Compras e Estoque (Estoque, Compras, Gestor de estoque e compras,
Financeiro), Vistoria (Vistorias, Técnico, Gestor de TI) e Fornecedores e serviços. O calendário fica no menu
**Calendário** (o de toda a equipe: "Ver o calendário de toda a equipe", para Estoque, Compras e Financeiro).

## Início

- **Meus painéis e relatórios**: os que você criou e os compartilhados com você.
- **Prontos**: os que já vêm com a Central (Indicadores do atendimento, Funil e prazos das compras, Situação do estoque,
  Projeções, Terceiros, os relatórios do estoque e a saúde das unidades), filtrados pela área nas abas do topo.

## Painel personalizável

1. **+ Novo painel**: dê um nome, escolha **quem vê** (só você, todos ou quem tem um papel) e marque os
   **indicadores**: em aberto, na fila, abertos há 7 dias, abertos e solucionados no período, satisfação, por unidade,
   por categoria, carga por técnico, por dia; compras em andamento, paradas, atrasadas, por etapa e o gasto (só para quem
   vê valores); abaixo do mínimo, em assistência, equipamentos por situação; notas e agenda das vistorias; chamados com
   fornecedores.
2. Ao abrir o painel, escolha o **período** e a **unidade**. Cada indicador vira um cartão: um número, barras ou uma
   tabela.
3. **Editar** muda os indicadores, o nome e quem vê; **Apagar este painel**, no fim da edição. Só quem criou muda.

Num painel compartilhado, cada pessoa vê só os indicadores que o papel dela permite.

## Relatório personalizável

1. **+ Novo relatório** e quatro escolhas:
   - **De onde**: chamados, pedidos de compra, equipamentos, vistorias ou fornecedores;
   - **Colunas**: marque as que quer (as padrão já vêm marcadas);
   - **Filtros**: período, unidade e, nos chamados, a situação;
   - **Agrupar e ordenar**.
2. **Ver a prévia**: as primeiras 50 linhas na tela, com o total.
3. **Baixar PDF** (até 8 colunas cabem na página) ou **Baixar CSV** (todas as colunas, para o Excel).
4. **Salvar**: dê um nome e escolha quem vê. Ele aparece em "Meus painéis e relatórios".

As regras de sempre continuam: o Estoque não vê valores (a coluna Valor e o relatório de compras com valores só
aparecem para Compras, Gestor e Financeiro), e cada fonte só aparece para quem tem a área.

## Painel da liderança (tela inicial)

O **Gestor de TI** e o **Líder técnico** veem, na tela inicial, seis indicadores (o Líder, só no alcance dele: toda a
TI ou os grupos dele, e os chamados sem grupo que estão com um técnico desses grupos). O clique num indicador abre a lista dos chamados que
formam o número, com a explicação do cálculo no topo. Sem
SLA, prioridade, urgência ou impacto. Só chamados (os subchamados ficam de fora); dias úteis pelo expediente da TI e os
feriados.

1. **Fila sem técnico**: chamados abertos num grupo e sem técnico, e há quanto tempo espera o mais antigo.
2. **Chamados parados**: chamados com técnico (inclusive pendentes com o usuário, o fornecedor ou a compra) sem
   movimentação do **técnico atribuído** (acompanhamento, tarefa, solução ou mudança de situação; o que a Central faz
   sozinha e o que outras pessoas registram não contam). Contam os dias úteis **inteiros** (hoje só conta depois que
   acaba): 1 = alerta (amarelo), 2 ou mais = limite (vermelho). Ex.: última movimentação na sexta: na segunda está em
   dia, na terça fica amarelo, na quarta vermelho.
3. **Entrada x saída por semana**: abertos (sem os cancelados) e com solução registrada, por semana de domingo a sábado,
   nas últimas 8 semanas; em vermelho, as semanas em que entrou mais do que saiu.
4. **Carga por técnico**: chamados em andamento com cada um (sem os que esperam a aprovação do usuário) e há quanto
   tempo está com ele o mais antigo (desde a atribuição a ele).
5. **Soluções recusadas**: recusas no período, por técnico que registrou a solução, e o total de soluções.
6. **Quem mais abre chamados**: as 5 unidades e as 5 categorias principais (o primeiro nível) com mais chamados no
   período.

O período (7, 30 ou 90 dias) vale para as recusas e para quem mais abre; os outros são do momento.
