# Configuração

No primeiro acesso do Administrador, o **Assistente** mostra os passos, com a situação de cada um (feito, pendente,
para depois). Quem não precisar de um passo marca "Já está como eu quero".

## Os passos do Assistente

1. **Personalização**: nome, logotipo, cores e o termo da "unidade" (loja, filial...).
2. **Unidades** e **setores**: endereço, tipo, expediente (calendário) e os setores.
3. **Pessoas**: o cadastro, os papéis e o vínculo de cada pessoa com a unidade (e quem é o gerente).
4. **Origem dos dados**: começar do zero ou **importar do GLPI** (Virada).
5. **Atendimento › Configuração**: grupos (com os níveis e os técnicos), categorias (em árvore), prazos do SLA,
   calendários da TI e das unidades.
6. **Avisos**: quem recebe o quê, os horários e o **e-mail reserva** (SMTP, com o botão de teste).
7. **Módulos**: o que vai ser usado ([Módulos](16-modulos.md)).

## Atendimento › Configuração

- **Geral**: triagem (ligada ou não), o grupo de entrada, os dias para fechar o solucionado sem resposta, os motivos de
  cancelamento.
- **Grupos**: nome, nível (N1, N2...) e os técnicos. O nível organiza a faixa "Em atendimento no meu nível".
- **Categorias**: a árvore (abrir e fechar, **Editar**, **+ Subcategoria**); o grupo sugerido de cada uma (vazio:
  herda de cima) e para que tipo vale.
- **Prazos do SLA** e **Calendários**: começam zerados; quem configura preenche.
- **Unidades**: o calendário de cada unidade.

O **SLA** e a **prioridade** se ligam separadamente; o sobreaviso é um módulo.

## Fornecedores

No módulo **Fornecedores** (`/fornecedores`, fora do Estoque desde a 5.1): venda, assistência, serviço, se atende pelo
aplicativo e, com o módulo Serviços, o **limite pré-aprovado por acionamento avulso** ([Suprimentos](23-suprimentos.md)).
