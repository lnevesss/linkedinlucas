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

## Etapa 4 — Salvar rascunho no Gmail
Use a ferramenta MCP Gmail (`gmail_create_draft`) para salvar o rascunho nos Drafts de `nevess.lucas@gmail.com`.

Parâmetros:
- **to:** `nevess.lucas@gmail.com`
- **subject:** `[LinkedIn] Rascunho para aprovação — AAAA-MM-DD`
- **body:** texto com o post completo, fonte/link e instruções para publicar

Se a ferramenta MCP falhar: mostre o post diretamente no chat e avise o Lucas.

## Ao final
Responda ao Lucas com um resumo curto:
- Notícia escolhida e por quê (1 linha).
- O texto do post.
- Confirmação que o rascunho foi salvo nos Drafts do Gmail.
- Lembrete: aprovar → postar no LinkedIn → mover o arquivo para `posts/publicados/`.

## Regras gerais
- Tudo em português, somente texto. Sempre respeitar `CLAUDE.md` e os arquivos de `context/`.
- Datas no formato `AAAA-MM-DD`, fuso de Brasília.
- Nunca afirmar que algo foi publicado no LinkedIn — a publicação é manual, feita pelo Lucas.
