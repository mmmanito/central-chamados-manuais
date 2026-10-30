# Suprimentos: fornecedores, serviços, compras e estoque (5.1)

Quatro módulos independentes, na categoria **Suprimentos e ativos** (Administração › Módulos). Cada instalação liga só
o que usa; ligar um módulo liga junto o que ele precisa.

| Módulo | O que traz | Precisa de |
|---|---|---|
| 🏢 **Fornecedores** | O cadastro único dos fornecedores; no chamado, o **acionamento de fornecedor** e o aplicativo do fornecedor | — |
| 🤝 **Serviços e contratos** | Os serviços acompanhados (links, sistemas, manutenções) com contrato e SLA; o **serviço avulso** com o limite pré-aprovado; **Serviços a pagar**; o gasto por fornecedor | Fornecedores |
| 🛒 **Compras** | Pedidos, cotação, propostas, avaliação, Financeiro, compra, recebimento e entrega; o **subchamado de aquisição** abre o pedido | Fornecedores |
| 📦 **Estoque de TI** | Equipamentos com patrimônio, almoxarifados, consumíveis, entregas, assistências, saídas; o estoque no chamado pelo aplicativo | — |

## Fornecedores (`/fornecedores`)

Para o Gestor de TI, o administrador, Compras e Estoque. Cada fornecedor marca o que faz: **vende** (aparece nas
compras), **assistência técnica** (no envio para conserto), **serviço** (nos acionamentos e contratos); e se **atende
pelo aplicativo** (as pessoas com o papel Fornecedor ligadas a ele veem só os acionamentos dele). Com o módulo Serviços,
o **limite pré-aprovado** por acionamento avulso.

### Contatos e lojas

Um fornecedor pode ter **vários contatos** (ex.: um para vendas e outro para a assistência técnica) e **várias lojas**
(cada uma com o CNPJ da filial e o endereço). Em **Fornecedores › Editar**, no quadro **Contatos e lojas**:

1. **Tipo**: *Contato* (uma pessoa ou um setor do fornecedor) ou *Loja ou filial*.
2. **Nome** (ex.: Vendas, Assistência, Loja Doca), a **pessoa** (opcional), o **telefone**, o **WhatsApp** e o **e-mail**;
   na loja, também o **CNPJ da loja** e o **endereço**.
3. **Para que serve**: vendas, assistência, financeiro ou outro (o contato precisa de ao menos um; a loja serve para
   tudo).

O contato principal continua nos campos de cima. Onde cada um aparece:

- **Proposta** (Compras): o campo **Loja ou contato** diz de qual loja ou vendedor veio a proposta. Aparece no mapa, na
  ficha e na ordem de compra (com o CNPJ da loja).
- **Registrar a compra**: com o fornecedor tendo lojas, **Retirar ou receber em** escolhe a loja de onde sai o
  equipamento, que pode ser outra, não a da proposta (comprou na Loja Doca e retira na Loja Nazaré). Sai na ficha do
  pedido e na ordem de compra.
- **Envio para a assistência** (Estoque): **Loja ou contato da assistência** mostra só os contatos de assistência e as
  lojas daquele fornecedor; a ficha da assistência mostra o telefone e o WhatsApp de quem recebeu o equipamento.

Exemplos: um fornecedor que **vende toner e faz assistência de impressoras**, com um contato para cada coisa:
cadastre um fornecedor só, marcado como *vende* e *assistência técnica*, com dois contatos (Vendas e Assistência). Uma
loja de informática com **duas lojas**: um fornecedor só, com as duas lojas; a proposta diz de qual loja veio e a
compra, de qual retirar. O histórico e os painéis continuam juntos, no mesmo fornecedor.

## Serviços e contratos (Atendimento › Serviços)

O serviço com contrato, as unidades atendidas, as características e o SLA do fornecedor. No **acionamento de
fornecedor** (subchamado), o técnico escolhe o serviço com contrato ou **avulso** e o valor combinado: com contrato, não
pede aprovação; avulso até o limite segue direto; acima (ou sem limite), espera a aprovação interna do Gestor de TI.
Depois da solução, o técnico registra o valor final e a nota; o pagamento é marcado em **Serviços a pagar** (Gestor de
TI e Financeiro). Sem o módulo, o acionamento continua (com Fornecedores), sem valor nem pagamento.

## Compras (`/compras`)

Os pedidos nascem do **subchamado de aquisição** (o chamado espera e recebe as etapas), do estoque mínimo dos
consumíveis (com o Estoque) ou direto, e passam por cotação, avaliação do Gestor, autorização do Financeiro
(`/compras/financeiro`), compra, recebimento e entrega. Com o Estoque, ele recebe no almoxarifado (com patrimônio) e
entrega; sem o Estoque, Compras recebe e entrega, sem almoxarifado nem patrimônio. O passo a passo de cada papel está
em [Compras](24-compras.md).

## Estoque

Veja [Estoque](18-estoque.md). O cadastro de equipamentos é o mesmo da vistoria.

## Combinações comuns

| Instalação | Ligue |
|---|---|
| Só atendimento e acionamento de terceiros | Fornecedores |
| Atendimento com contratos de links e serviços | Fornecedores + Serviços |
| Compra sem controlar estoque | Fornecedores + Compras |
| Tudo | Fornecedores + Serviços + Compras + Estoque |
