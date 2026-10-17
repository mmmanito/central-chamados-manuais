# Manual do técnico

O técnico trabalha pelo **painel** (no computador) e pelo **aplicativo** (no celular, em campo). Os dois mostram os
mesmos chamados; o aplicativo fecha todo o ciclo do chamado, e o painel tem tudo, inclusive o que é de bancada.

## No painel

### Atendimento: as faixas

Ao abrir **Atendimento**, você vê três faixas:

1. **Na fila, sem técnico**: os chamados dos seus grupos esperando alguém assumir. Os mais urgentes e os mais perto
   do prazo vêm primeiro. **Assumir** na própria linha.
2. **Comigo**: os seus, com a próxima ação no botão (Iniciar, Abrir).
3. **Em atendimento pela equipe**: chamados em atendimento por colegas da equipe, para ajudar, assumir junto ou
   acompanhar (os dos grupos do seu nível e os que estão com um colega desses grupos, mesmo sem grupo, como os
   importados do GLPI).

Chamado atribuído a um técnico **já está em atendimento**: não há o passo "Iniciar". Sem técnico, ele fica **Na fila
do grupo** até alguém assumir. Em cada linha, a situação aparece como um selo colorido e, ao lado, quem atende.
Categoria e subcategoria (e unidade e setor) se escolhem em listas em cascata: escolhida a categoria, aparece a lista
das subcategorias dela.

As faixas se atualizam sozinhas a cada minuto e quando você volta para a aba (não enquanto você marca chamados ou
digita).

No topo, troque para **Lista** (com filtros e colunas, como no GLPI) ou **Kanban** (arraste o cartão para mudar a
situação). O menu lateral recolhe pelo botão do rodapé.

### Ações em lote

A barra acima das faixas e da lista fica sempre à vista. Marque chamados (Shift marca um intervalo; "marcar todos"
marca a faixa inteira), escolha a ação e **Aplicar**: atribuir a um técnico, mudar o grupo, cancelar com motivo ou
cancelar como duplicado de outro chamado.

### A ficha do chamado

- **Próxima ação**: logo abaixo dos dados, o passo natural para a situação (Classificar, Iniciar o atendimento,
  Solucionar, Retomar...). Clicar abre o painel certo.
- **Classificar**: tipo (incidente, requisição, ordem de trabalho) e categoria são exigidos na primeira ação de
  atendimento. Na escolha da categoria, digite parte do nome para filtrar (ex.: "impr").
- **Acompanhar**: mensagens e anexos na linha do tempo. **Privado** fica só para a equipe.
- **Solucionar**: descreva o que foi feito. O usuário aprova (com estrelas) ou recusa.
- **Planejar o atendimento**: marca dia e hora; o chamado aparece em "planejado para hoje" e no calendário.
- **Técnicos, grupo e categoria**: mude o grupo, o técnico, a unidade, o setor, a categoria.
- **Mais ações**: deixar pendente (com o usuário ou com fornecedor; o SLA pausa), pedir aprovação interna, abrir
  **subchamado** (aquisição, acionamento de fornecedor ou outra equipe), marcar como crítico (sobreaviso), tarefa,
  cancelar.

### Subchamados

O chamado do usuário pode esperar outros (até 3 níveis): uma **aquisição** (abre o pedido de compra), o
**acionamento de um fornecedor** ou o trabalho de **outra equipe**. O pai fica aguardando e volta sozinho ao
atendimento quando os filhos terminam; o usuário só vê o pai, com mensagens simples ("Aguardando um fornecedor").

No acionamento de fornecedor, escolha o **serviço com contrato** ou **avulso** e o **valor combinado**. Avulso acima
do limite pré-aprovado do fornecedor espera a aprovação do Gestor de TI. Depois da solução, registre o **valor final**
e o **nº da nota ou do recibo** no quadro "Serviço do fornecedor".

### Minha mesa

Quadro pessoal e privado (a fazer, fazendo, feito) para organizar o seu dia, com atividades que nem são chamados. Dá
para citar um chamado num cartão.

## No aplicativo (celular)

Entre em `/u` com o seu usuário: quem atende pelo painel (Técnico, Triagem, Líder técnico e Gestor de TI) cai direto na
**mesa** da TI.

- **Meus**, **Fila** e **Hoje** (planejados para hoje).
- **Todos** (Gestor de TI e Líder técnico): o Gestor vê todos os chamados abertos; o Líder, os dos grupos do alcance
  dele.
- **Nesta unidade**: ao chegar numa loja, **Cheguei**; ao sair, **Registrar a saída**. A tela mostra os chamados
  daquela unidade.
- **Na ficha**: Assumir, Classificar, Iniciar, Registrar (com fotos), Deixar pendente, Retomar, Solucionar.
- **Claro / Escuro**, no topo: a cor da tela (sem escolha, segue o celular).
- **Sem sinal**: os registros ficam guardados no celular e são enviados quando a conexão voltar ("Assumir" e
  "Iniciar" precisam de conexão, porque vale quem chega primeiro).

### Vistorias e estoque no chamado (5.1)

- **🔎 Vistorias** (na mesa): iniciar, preencher em etapas (também sem sinal), enviar ([Vistoria](13-vistoria.md)).
- **📦 Equipamentos e itens** (na ficha do chamado, com o módulo Estoque): ligar um equipamento da unidade, trocar por
  um do almoxarifado, usar um consumível, **pedir compra** (abre o subchamado de aquisição).
- **Tarefas de projetos**: as suas aparecem na Minha mesa, no painel ([Projetos](22-projetos.md)).

## Avisos

Você é avisado de chamado novo na fila dos seus grupos, chamado atribuído a você, resposta do usuário, solução
recusada e o lembrete do planejado. Com o SLA ligado, também do prazo perto de vencer. Ligue os avisos no celular
(🔔); fora do horário, os avisos seguem as regras definidas pela TI.
