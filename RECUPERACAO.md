# Recuperação de Desastre — subir outro bot em ~15 min

Se o bot cair (banido, deletado, token vazado), você **não perde os
assinantes**: o banco de dados (Turso) é independente do bot. Basta subir
uma nova instância apontando para o **mesmo banco**.

## Passo a passo

1. **Novo bot no Telegram:** @BotFather → /newbot → novo token.
2. **Canal:** pode criar um canal novo (recomendado se o antigo caiu junto)
   ou reutilizar o existente. Adicione o novo bot como administrador com
   permissão de convidar.
3. **Vercel:** crie um **novo projeto** a partir do mesmo repositório
   (ou duplique o projeto atual).
4. **Variáveis de ambiente:** cadastre as mesmas de antes, trocando apenas:
   - `BOT_TOKEN` → o novo token
   - `VIP_CHANNEL_ID` → o ID do canal (novo ou mesmo)
   - `TELEGRAM_WEBHOOK_SECRET` → gere um novo valor
   - `PUBLIC_URL` → a nova URL do projeto
   - `TURSO_URL` e `TURSO_TOKEN` → **os MESMOS de antes** (é aqui que os
     assinantes são preservados)
5. **Webhook do Telegram:** rode o `setWebhook` com a nova URL e o novo secret.
6. **Teste:** `/health`, `/start` com um usuário de teste, `/cron/expire`
   com o Bearer.

## O que é preservado

- ✅ Assinantes ativos e seus vencimentos (tabela `subs`)
- ✅ Histórico de compras (tabela `payments`)
- ✅ Visitantes e campanhas de nudge (tabela `users`)

## O que precisa ser refeito

- ⚠️ Links de convite antigos: gere novos pelo bot (`/start` dos usuários
  gera automaticamente). Revogue os links antigos nas configurações do canal.
- ⚠️ Webhook da Epague: se a `PUBLIC_URL` mudou, atualize no painel da Epague.

## Prevenção

- Guarde as variáveis de ambiente num local seguro (elas são o "backup"
  da instância).
- Nunca commite o `.env`.
- Se o token do bot vazar: @BotFather → /revoke → gere um novo e atualize
  a `BOT_TOKEN` na Vercel (redeploy).
