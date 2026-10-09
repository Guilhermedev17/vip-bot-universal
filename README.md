# Bot de Vendas VIP — Pacote Universal

Bot de Telegram que vende acesso a canal/grupo privado via **Pix (Epague)**,
com funil de retenção completo e anti-pirataria. Cada instalação é
independente: seu bot, seu canal, sua conta Epague (seu dinheiro), seu banco
de dados.

## Funcionalidades

- **Vendas:** 4 planos (semanal/mensal/trimestral/vitalício), QR Pix +
  copia-e-cola, confirmação automática via webhook
- **Retenção:** cutucadas promocionais a cada 2 dias pra quem não comprou
  (8 copys + descontos rotacionados), avisos de vencimento (7/3/1 dias),
  renovação com 10% OFF
- **Anti-pirataria:** entrada só com pedido aprovado pra assinante ativo;
  link compartilhado não adianta
- **Automação:** cron diário remove vencidos do canal
- **Promoções:** mecanismo de desconto temporário (ex: 50% OFF de fim de semana)
- **Admin:** listar visitantes, conceder VIP cortesia
- **Custo fixo:** R$ 0 (Vercel + Turso + GitHub gratuitos; só a taxa da
  Epague por venda)

## Instalação

Cole o conteúdo de **`PROMPT-INSTALACAO.md`** no seu Muse e siga o guia.
Ele executa a instalação inteira com você.

## Recuperação

Se o bot cair, veja **`RECUPERACAO.md`** — dá pra subir outro em ~15 min
sem perder os assinantes.

## Estrutura

| Arquivo | Papel |
|---|---|
| `app.py` | Lógica do bot (vendas, retenção, webhooks, cron, admin) |
| `config.py` | Configurações via variáveis de ambiente (`BRAND_NAME`, planos, promos) |
| `tg.py` | Cliente da API do Telegram |
| `db_cloud.py` | Banco Turso (assinaturas, pagamentos, visitantes) |
| `epague.py` | Cliente da API da Epague |
| `api/index.py` | Entrypoint da Vercel |
| `vercel.json` | Rotas + cron diário |
| `.env.example` | Todas as variáveis documentadas (copie para `.env`, nunca commite) |
