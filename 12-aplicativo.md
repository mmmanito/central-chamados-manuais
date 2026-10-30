# Aplicativo (`/u`)

Um só aplicativo para quatro públicos, cada um com o que precisa:

| Quem | Cai em | O que faz |
|---|---|---|
| Usuário | `/u` | Abre e acompanha chamados, conversa, aprova ou recusa a solução, cancela |
| Gerente da unidade | `/u` | O mesmo, para todos os chamados da unidade; pedidos de mudança de pessoas; aprovar ou contestar as vistorias |
| Técnico, Triagem, Líder técnico e Gestor de TI | `/u/t` | Mesa (meus, fila, hoje), ficha com todas as ações, chegada e saída na unidade, vistorias, estoque no chamado; o Gestor de TI e o Líder têm também a aba **Todos** (toda a TI, ou os grupos do alcance do líder) |
| Fornecedor externo | `/u/f` | Só os acionamentos do fornecedor dele: registrar, agendar, avisar a TI, solucionar |

É um aplicativo web instalável (PWA): funciona no navegador e pode ir para a tela inicial do celular, sem loja de
aplicativos e sem Telegram. Quem pode entrar é marcado em Usuários ("acesso ao aplicativo"); usuário e
senha são entregues pelo [Acesso em lote](04-manual-painel.md#acesso-em-lote).

**Tema** (5.1.0-rc5): o botão **Claro / Escuro** no topo troca o tema. Sem escolha, o aplicativo segue o tema do
celular; a escolha fica guardada naquele aparelho.

## Instalar na tela inicial

**Android (Chrome):** abra o endereço, toque no menu **⋮** › **Instalar aplicativo** (ou **Adicionar à tela
inicial**). O ícone aparece como um aplicativo comum.

**iPhone (Safari):** abra o endereço no **Safari**, toque em **Compartilhar** (o quadrado com a seta) › **Adicionar à
Tela de Início**. Os avisos no iPhone só funcionam assim, instalado, e no iOS 16.4 ou mais novo.

## Avisos no celular

Dentro do aplicativo, **🔔 Receber avisos neste celular** e permita. Os avisos chegam mesmo com o aplicativo fechado
(Android) ou instalado na tela inicial (iPhone). Na tela bloqueada, o aviso não mostra o título do chamado (só que há
novidade). Se o celular não recebe avisos, o e-mail reserva (se a TI configurou) cobre os casos importantes.

## Sem sinal

O aplicativo guarda o que foi enviado sem conexão (abrir chamado, responder, registrar, solucionar, a vistoria, com as fotos) e
manda sozinho quando o sinal volta. "Assumir" e "Iniciar" precisam de conexão (vale quem chega primeiro).

## Fora da rede da empresa

Pelo **gateway** (veja Gateway): o aplicativo funciona pela internet (4G), e só ele passa; o painel
continua só na rede interna. Se a Central estiver fora do ar, o gateway guarda os envios que podem esperar e os
entrega quando ela voltar (em até 48 horas).

## Sair e tirar alguém do aplicativo

**Sair** apaga a sessão e os dados guardados no celular. Para tirar alguém do aplicativo, a TI desmarca o acesso ao
aplicativo ou troca a senha da pessoa: a sessão deixa de valer na hora. A sessão dura 30 dias de uso.
