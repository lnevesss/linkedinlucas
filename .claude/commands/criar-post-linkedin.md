# Criar post de LinkedIn (pipeline completo)

Orquestra as 4 etapas do projeto LinkedInLucas. Execute **em ordem**, cada uma depende da anterior.

## Etapa 1 — Pesquisar
Use o subagent **`pesquisador-wellness`** (via Agent tool).
- Resultado esperado: arquivo `pesquisas/AAAA-MM-DD.md` com 5–8 candidatas.
- Se o agente não encontrar boas notícias, pare e avise o Lucas em vez de inventar.

## Etapa 2 — Curar
Use o subagent **`curador-noticias`**.
- Ele adiciona a seção "✅ Notícia escolhida" ao arquivo de pesquisa.

## Etapa 3 — Escrever
Use o subagent **`redator-linkedin`**.
- Resultado esperado: `posts/rascunhos/AAAA-MM-DD.md` com o post pronto em português.

## Etapa 4 — Publicar rascunho no GitHub
Faça commit e push do rascunho. O GitHub Actions dispara automaticamente e envia o post para o Telegram do Lucas.

```bash
git config user.email "bot@linkedinlucas.com"
git config user.name "LinkedInLucas Bot"
git add posts/rascunhos/
git commit -m "post: AAAA-MM-DD"
git push
```

Se o push falhar: mostre o post no chat e avise o Lucas.

## Ao final
Responda ao Lucas com um resumo curto:
- Notícia escolhida e por quê (1 linha).
- O texto do post.
- Confirmação que a mensagem foi enviada no Telegram.
- Lembrete: aprovar → postar no LinkedIn → mover o arquivo para `posts/publicados/`.

## Regras gerais
- Tudo em português, somente texto. Sempre respeitar `CLAUDE.md` e os arquivos de `context/`.
- Datas no formato `AAAA-MM-DD`, fuso de Brasília.
- Nunca afirmar que algo foi publicado no LinkedIn — a publicação é manual, feita pelo Lucas.
