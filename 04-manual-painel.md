# Manual do painel

O painel é a bancada da TI, no computador, na rede interna. Cada área do menu tem uma cor (Atendimento azul, Minha mesa roxo, Projetos índigo, Conhecimento verde-azulado, Estoque e compras laranja, Vistorias vinho, Administração cinza). O botão
**Recolher menu**, sempre no pé da tela, deixa só os ícones (a escolha fica no computador). Claro e escuro, no
topo; **Minha senha** e **Sair** ficam no menu do usuário, no canto superior direito.

## Áreas

| Área | Para quê | Detalhes |
|---|---|---|
| **Início** | O resumo do dia: em aberto, na fila (e a maior espera), aguardando terceiros, abertos e solucionados hoje, quem espera atendimento, técnicos em campo, comunicados | |
| **Atendimento** | Os chamados: faixas, lista, kanban, ficha, ações em lote, abrir chamado | [Manual do técnico](07-manual-tecnico.md), [Atendimento](19-atendimento.md) |
| **Comunicados** | Avisar as unidades de um problema geral e de quando normalizou | |
| **Minha mesa** | O quadro pessoal de tarefas | [Manual do técnico](07-manual-tecnico.md#minha-mesa) |
| **Projetos** | Projetos e demandas: fases, tarefas, riscos, diário (módulo) | [Projetos](22-projetos.md) |
| **Conhecimento** | A base de artigos (e o "Resolva sozinho" do aplicativo) | |
| **Calendário** | Planejados, programados, vistorias, entregas e pagamentos | |
| **Painéis** | Indicadores do atendimento e do estoque | [Indicadores e TVs](08-dashboards.md) |
| **Vistorias** | Módulo opcional | [Vistoria](13-vistoria.md) |
| **Estoque**, **Compras** (com o Financeiro), **Fornecedores** | Módulos opcionais de suprimentos | [Suprimentos](23-suprimentos.md), [Estoque](18-estoque.md) |

Dentro do **Atendimento**, para o Gestor de TI: **Serviços** (com contrato), **Serviços a pagar**, **Programados**,
**Indicadores** (com o Grafana: os dashboards Gerencial, Operacional e Vistoria técnica, e o CSV e o PDF; veja
[Indicadores e TVs](08-dashboards.md)), **Escala** (sobreaviso), **Prioridade** e **Configuração**.

## Administração

| Tela | Para quê |
|---|---|
| **Assistente** | Os passos da configuração inicial, do primeiro acesso em diante ([Configuração](03-configuracao.md)) |
| **Unidades** | As unidades (lojas, sede...) e os **setores** de cada uma; expediente, endereço, tipo |
| **Personalização** | Identidade e aparência (nome, logotipo, cores, o termo "unidade", o aplicativo), **feriados** (valem para o SLA e os avisos), documentos em PDF, dados da empresa |
| **Módulos** | Liga e desliga os módulos opcionais ([Módulos](16-modulos.md)) |
| **Configurações** | E-mail reserva (SMTP), avisos e opções gerais |
| **Aplicativo** | O endereço do aplicativo e quem entra |
| **Usuários** | Pessoas, papéis, vínculos com unidades (e o gerente), acesso ao aplicativo, **Acesso em lote** |
| **Situação** | Tarefas automáticas, gateway, leitura do GLPI (opcional) e as **Telas de TV** (com o endereço do Grafana) |
| **Auditoria** | Quem fez o quê, quando e de onde (toda mudança, inclusive pelo aplicativo) |
| **Importar do GLPI** | A importação da virada (pelo Assistente › Origem dos dados) |

## Acesso em lote

**Usuários › Acesso em lote**: a lista de quem ainda não tem acesso (por exemplo, os importados do GLPI).
Marque as pessoas, ligue (se for o caso) o acesso ao aplicativo e **Gerar senhas e baixar o PDF**: um cartão por
pessoa, com o usuário, uma senha temporária e os endereços. A senha não fica guardada no sistema; no primeiro acesso
a pessoa cria a dela. Perdeu o cartão? Gere de novo (a anterior deixa de valer).

## Unidades e setores

Cada unidade pode ter **setores** (a Sede administrativa com Financeiro, RH, Logística...): na ficha da unidade, seção
**Setores**, inclua, renomeie ou desative (setor não se apaga). O chamado e a pessoa podem indicar o setor;
expediente, SLA e feriados continuam sendo da unidade. As telas mostram "Unidade › Setor".
Na **abertura** do chamado (painel e aplicativo), a unidade e os setores vêm numa lista só, como no GLPI: "Loja
Centro", "Sede administrativa", "Sede administrativa › Financeiro"... Digite parte do nome na busca acima da lista
para achar o setor. Escolher o solicitante já traz a unidade e o setor dele. Para uma loja ter setores (ex.: Caixas,
Depósito), cadastre-os na ficha da loja: eles entram na lista na hora.
