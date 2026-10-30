# Compras

Manual de quem pede, cota, avalia, autoriza, recebe e entrega as compras de TI. O módulo **🛒 Compras** (painel ›
Módulos) funciona com ou sem o **📦 Estoque**; o que muda sem ele está em [Sem o Estoque](#sem-o-estoque). Fornecedores
e serviços: [Suprimentos](23-suprimentos.md). Equipamentos e consumíveis: [Estoque](18-estoque.md).

![Compra: do pedido à compra](fluxos/compra.svg)

## Em uma página

**5.2.5: a proposta é o arquivo.** Cada proposta é só **fornecedor, valor total e arquivo** (PDF ou print do anúncio);
quem cota **escolhe a mais vantajosa ao enviar ao Gestor**; o Financeiro recebe o **espelho do pedido** (página 1) e o
**arquivo da proposta escolhida** (páginas seguintes).

**Etapas, com o Financeiro fora do sistema (o caso da Tudo):** Em cotação → **Assinaturas** (Gestor e Financeiro, no
papel) → Autorizado → Comprado → Recebido (em parte ou todo) → Concluído.
**Com alguém no papel Financeiro:** Em cotação → Com o Gestor → Com o Financeiro → Autorizado → Comprado → Recebido →
Concluído. Fins sem compra: **Cancelado** (antes de *Comprado*) e **Recusado** (pelo Gestor ou pelo Financeiro), sempre
com o motivo.

| Quem | O que faz | Onde |
| --- | --- | --- |
| **Técnico** (ou quem atende o chamado) | Pede a compra a partir do chamado | Ficha do chamado › **Deixar pendente › Pendente de compras** |
| **Estoque** | Pede reposição ou faz uma requisição; recebe e entrega (com o Estoque ligado) | Menu **Compras** · **Estoque** |
| **Compras** | Inclui os itens, anexa as propostas, escolhe a mais vantajosa e envia ao Gestor, imprime o espelho, anexa os documentos assinados, registra a compra, resolve divergências | Menu **Compras** |
| **Gestor de TI** | Assina **Autorização TI** e colhe a assinatura do Financeiro; devolve ou recusa | O espelho impresso · ficha do pedido |
| **Financeiro** (fora do sistema) | Assina **Autorização Financeiro** no espelho e a proposta do fornecedor | O papel |
| **Financeiro** (no sistema, se houver) | Escolhe a condição de pagamento, autoriza, devolve ou recusa | Menu **Financeiro** |

**Regras que valem sempre:**
- **Ninguém aprova o próprio pedido.** Quem enviou pela TI não autoriza pelo Financeiro.
- **O Estoque não vê valores nem propostas.** Compras, o Gestor e o Financeiro veem.
- **Não há lembretes em horários fixos.** O que está parado (2 dias ou mais na etapa) ou atrasado aparece em vermelho
  na tela Compras e no contador do menu de quem precisa agir.

## Antes de começar (uma vez)

1. **Ligue o módulo** em painel › Módulos › 🛒 Compras (e o 🏢 Fornecedores, que ele usa).
2. **Dê os papéis** em **Usuários**, na ficha de cada pessoa: *Compras*, *Gestor de estoque e compras*, *Financeiro* e,
   para quem recebe e entrega, *Estoque*. Uma pessoa pode ter vários.
3. **Dados da empresa** (Personalização › Dados da empresa, administrador): razão social, CNPJ, endereço e o e-mail para
   cotações. Eles saem na solicitação de cotação e na ordem de compra.
4. **Cotações do padrão** (Estoque › Configuração › Compras, só o Gestor): quantas propostas a compra precisa (padrão
   3, de 1 a 10) e se a Central avisa quem precisa agir em cada etapa. Sem o módulo Estoque, essa tela não aparece e
   vale o padrão de 3.
5. **Fornecedores** marcados como *vende* (menu **Fornecedores**). Um fornecedor novo também pode ser cadastrado direto na
   proposta (veja abaixo).

## 1. Pedir uma compra

São quatro caminhos, e todos geram o mesmo **pedido de compra**:

- **Pelo chamado (o mais comum).** Na ficha do chamado, **Mais ações › Deixar pendente › Pendente de compras** (no
  painel ou no aplicativo do técnico): abre uma janela com o que é preciso e a Central cria o subchamado de compra
  (nº X.1) e o pedido, com o título, a descrição, a unidade e o vínculo. O chamado fica **pendente** enquanto a compra
  anda e volta sozinho para o técnico na entrega.
- **Reposição de consumível** (com o Estoque): em *Estoque › Consumíveis* ou no início do estoque, **Pedir compra** no item
  abaixo do mínimo abre o pedido com a quantidade que falta. Se já houver um pedido em andamento com o mesmo item e
  almoxarifado, ele não abre outro.
- **Requisição** (papel Estoque): *Compras › Nova requisição de compra*. Descreva o que precisa; Compras inclui os itens.
- **Pedido direto** (papel Compras): *Compras › Novo pedido de compra*.

O número de um chamado pode ser informado na abertura ou depois, em **Editar**.

## 2. Cotar (Compras)

1. **Incluir os itens** (tipo, quantidade e especificação). Cada item mostra o **último preço pago**.
2. **Pedir as propostas** aos fornecedores (a solicitação de cotação em PDF continua disponível, se ajudar).
3. **Anexar cada proposta** (*Registrar proposta*): o **fornecedor** (da lista ou *+ Novo fornecedor*), o **valor
   total** (com frete, se houver) e o **arquivo** da proposta, obrigatório: o PDF do fornecedor ou o anúncio salvo em
   PDF (Ctrl+P) ou como imagem. Não se digita mais item por item, marca, prazo, validade nem condição de pagamento: o
   arquivo diz. Errou? **Revisar** abre uma nova rodada e a anterior fica no histórico.
4. O quadro das propostas mostra o **total** de cada uma (o menor em verde) e o link **abrir o arquivo**.

## 3. Escolher e enviar ao Gestor (Compras)

Em **Enviar ao Gestor**:
1. **Escolha a mais vantajosa.** As propostas aparecem da menor para a maior; a de **menor valor** já vem marcada.
2. Se escolher outra, escreva o **motivo da escolha** (ex.: entrega em 2 dias). Ele **sai impresso no espelho**.
3. Com menos propostas que o padrão, escreva a **justificativa** da exceção (também sai impressa).
4. Clique em **Enviar ao Gestor**. A escolhida fica fixada no pedido; as outras ficam *não escolhidas*.
5. **Imprima o pedido**: página 1 com o **espelho** (os dados do chamado: nº, data e hora, unidade, quem pediu e
   técnico; os itens; a proposta escolhida; o motivo e a justificativa, se houver; as assinaturas **Autorização TI** e
   **Autorização Financeiro**) e, nas páginas seguintes, o **arquivo da proposta**, como veio do fornecedor.

## 4. Assinaturas da TI e do Financeiro (sem o Financeiro no sistema)

1. O **Gestor de TI** confere o espelho e a proposta e assina **Autorização TI** (vale também como a autorização da
   exceção de cotações, quando houver).
2. O Gestor leva ao **Financeiro**, que assina **Autorização Financeiro** no espelho e assina a **proposta do
   fornecedor**.
3. Com os documentos de volta, **qualquer pessoa de Compras** escaneia e, na ficha do pedido, em **Assinaturas da TI e
   do Financeiro**, preenche **Quem assinou pelo Financeiro**, anexa o arquivo e clica em **Anexar documentos
   assinados**. O pedido segue direto para a **compra**.
4. Proposta errada ou faltando cotação: o Gestor usa **Devolver para completar as cotações**; para desistir, **Recusar a
   compra** (com o motivo).

O escaneado fica no pedido: é a prova de que a TI e o Financeiro autorizaram. O histórico registra quem anexou e quem
assinou pelo Financeiro.

### Com o Financeiro no sistema

Se alguém tiver o papel **Financeiro**, o caminho pelo sistema continua: o Gestor confirma a escolha em **Aprovar a
escolhida e enviar ao Financeiro** e o Financeiro, no menu **Financeiro**, escolhe a condição de pagamento e autoriza,
devolve ao Gestor ou recusa.

### Pedidos de antes da 5.2.5

Os pedidos enviados ao Gestor antes da 5.2.5 (sem a escolha) seguem como estavam: o Gestor escolhe e aprova no sistema
e Compras anexa a autorização em papel. As propostas antigas mantêm os dados que tinham (frete, prazo, validade,
condições), e o quadro os mostra.

## 5. Comprar (Compras)

Com o pedido **Autorizado** (filtro *autorizados, a comprar*):

1. **Ordem de compra em PDF:** o documento para o fornecedor escolhido, com os dados da empresa, os itens e os valores
   dele, o frete, o prazo e o local de entrega e as datas de pagamento, sem as outras propostas.
2. Feita a compra no fornecedor, **Registrar a compra**: o número do pedido no fornecedor e a previsão de entrega. Se
   algum item chega em outra data, marque *Algum item chega em outra data?* e informe a previsão de cada um. Se o
   fornecedor tem mais de uma loja, escolha **Retirar ou receber em**: a loja de onde sai o equipamento, que pode ser
   outra, não a da proposta. Ela aparece na ficha e na ordem de compra.

Quem tem o papel Estoque é avisado da entrega prevista. Passada a data, o pedido fica em vermelho como **atrasado** (o atraso conta
pelo próximo item que falta).

## 6. Receber

![Recebimento e entrega](fluxos/recebimento-entrega.svg)

Com o Estoque ligado, quem recebe é o **Estoque**; sem ele, **Compras**. O recebimento pode ser **parcial** (uma entrega
de cada vez). No pedido, **Receber**:

1. Escolha o **almoxarifado** (o padrão já vem marcado).
2. Para cada item: a **quantidade** que chegou, a **marca e o modelo** (vêm da proposta) e as **séries** dos
   equipamentos.
3. A **nota fiscal**: o número, a data da nota, a data da compra, a **garantia** (em meses, ex. `12`, ou uma data) e o
   arquivo. Para várias entregas com a mesma nota, a Central sugere as notas já registradas no pedido.

Com o Estoque, cada equipamento ganha o **patrimônio na hora** e entra **em estoque** no almoxarifado, com o valor, a
marca, o modelo e o fornecedor na ficha; os consumíveis somam ao saldo. Boleto com vencimento em dias após a nota: a data
é calculada aqui. Datas impossíveis são recusadas (garantia antes da compra, nota ou compra no futuro, nota antes da
autorização).

### Divergência

Chegou faltando, com outro modelo ou com defeito? Registre a **divergência** no próprio recebimento. As unidades com
problema não entram e o pedido volta para **Compras** resolver com o fornecedor:

- **Troca** ou **complemento**: as unidades continuam a receber;
- **Devolução sem reposição**: a quantidade do item diminui e o pedido pode se concluir.

## 7. Entregar à unidade

No pedido recebido (filtro *a entregar à unidade*), **Entregar** registra a entrega de tudo o que foi recebido e ainda não
foi entregue, com o **termo de entrega** em PDF para colher a assinatura. Com o Estoque, os equipamentos passam para a
unidade (em uso), com a movimentação no histórico.

## O chamado de origem

- Fica **pendente** durante a compra e recebe um **acompanhamento privado** a cada etapa, sem valores.
- É **solucionado** pela Central quando a compra chega a quem pediu: na **última entrega** à unidade ou, na reposição
  do almoxarifado, no **recebimento** total. A solução descreve o pedido, os itens e os patrimônios, sem valores, e a
  unidade aprova ou recusa como em qualquer chamado.

## Cancelar ou recusar

- **Cancelar** (antes de *Comprado*): quem abriu o pedido, Compras ou o Gestor, com o motivo.
- **Recusar**: o Gestor ou o Financeiro, com o motivo.

Ao cancelar ou recusar, o Gestor e Compras escolhem entre **Encerrar e avisar a unidade** (o chamado é cancelado, com
um acompanhamento visível à unidade com o motivo, sem pesquisa de satisfação) ou **Deixar com a equipe para outra
solução**. Recusada pelo Financeiro, o chamado **sempre volta para a TI**, e o Gestor e Compras são avisados. Um pedido
cancelado ou recusado não volta sozinho: para tentar de novo, abra outro.

## Avisos

Pelo **sino**, pelo **push** do celular (para quem ligou os avisos no aplicativo) e pelo e-mail reserva, para quem
precisa agir:

| Acontecimento | Quem é avisado |
| --- | --- |
| Pedido novo, pedido devolvido pelo Gestor | Compras |
| Propostas para avaliar, devolvido pelo Financeiro | Gestor |
| Homologadas enviadas | Financeiro; sem ninguém com o papel Financeiro, Compras e quem abriu (autorização em papel) |
| Autorizado | Compras e quem abriu |
| Compra feita, com a entrega prevista | Quem tem o papel Estoque |
| Divergência no recebimento / resolvida | Compras / Estoque |
| Cancelado ou recusado | Compras, Gestor e quem abriu |

Cada aviso tem o link da ficha, que abre **na rede interna**.

## Documentos (PDF)

Todos no padrão de documento da Personalização (papel timbrado e margens): **pedido de compra** (com a proposta
escolhida, é o **espelho** na página 1 e o arquivo da proposta nas seguintes, para as assinaturas; sem valores para o
Estoque), **solicitação de cotação**, **mapa comparativo**, **ordem de compra** (para o fornecedor escolhido) e
**termo de entrega**. Com o timbrado compacto (cabeçalho de até 3 cm, margens de 2,9 cm e 2,0 cm), o espelho cabe numa
página.

## Sem o Estoque

Compras funciona sozinho:

- Itens: **equipamento** e **outro item** (o **consumível** precisa do Estoque, porque vem do catálogo dele).
- **Compras recebe e entrega.** O recebimento registra as quantidades, as divergências, a nota e as **séries** (no
  registro), sem almoxarifado nem patrimônio. A entrega conclui o pedido e soluciona o chamado.
- A reposição pelo estoque mínimo não existe (é do Estoque).
- As **cotações do padrão** ficam em 3 (a tela de configuração é a do Estoque).
- O menu **Painéis** (com a aba Compras) também é do Estoque: sem ele, o acompanhamento é pela tela Compras e pelo
  Calendário.
- O aviso de "compra feita" vai para quem tem o papel Estoque: sem o módulo, acompanhe pelo filtro *a receber do
  fornecedor*.

## Painéis e calendário

- **Painéis › Compras**: o funil por etapa com o tempo médio em cada uma (12 meses), os parados, as entregas atrasadas,
  o prazo prometido × o real, as exceções de cotação e as divergências; para quem vê valores, o valor por mês, por
  categoria e por fornecedor, e a diferença entre a escolhida e a mais cara (e a mais barata) homologada.
- **Painéis › Projeções**: o gasto comprometido (autorizado e não concluído), o *a pagar* e a tendência dos 6 meses.
- **Painéis › Relatórios**: compras com valores (Compras, Gestor, Financeiro), em PDF e CSV, com período e unidade.
- **Calendário**: as entregas previstas (Estoque, Compras), a validade das propostas (Compras, Gestor) e os
  vencimentos de pagamento (Financeiro).

## Problemas comuns

| Situação | O que fazer |
| --- | --- |
| Não consigo mudar os itens | Já há proposta registrada: os itens travam. Remova as propostas ou abra outro pedido |
| "Enviar ao Gestor" pede justificativa | Há menos propostas válidas que o padrão: explique por que (fornecedor único, urgência) |
| O Financeiro não vê o botão de autorizar | Quem enviou pela TI não autoriza; outra pessoa com o papel Financeiro autoriza |
| O pedido está *com o Financeiro* e ninguém tem esse papel | Autorização em papel: imprima, colha a assinatura e anexe (passo 4) |
| O pedido está em vermelho | Parado há 2 dias ou mais na etapa, ou a entrega passou da previsão |
| O Estoque não vê os valores | É de propósito: só Compras, o Gestor e o Financeiro veem valores |
| O fornecedor não aparece na proposta | Ele precisa estar ativo e marcado como *vende* em Fornecedores |
