---
name: criar-post-linkedin
description: Pipeline completo de criação de post de LinkedIn sobre wellness para o Lucas — pesquisa notícias, escolhe a melhor, escreve o post em português e envia o rascunho por e-mail para aprovação. Use quando o Lucas pedir um novo post de LinkedIn, "criar post", "post do dia" ou quando rodar de forma agendada.
---

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

## Etapa 4 — Enviar post via Telegram
Use PowerShell para enviar o post ao Telegram do Lucas via Bot API. As credenciais estão em `.claude/config/telegram.md`.

Execute via Bash (substitua MESSAGE pelo conteúdo real):

```bash
python3 -c "
import json, urllib.request
token = '8561809125:AAHonpQsbKzkW83dWoTYqn6DtVyQQr7gEuU'
chat_id = '8983818235'
text = '''MESSAGE'''
data = json.dumps({'chat_id': chat_id, 'text': text, 'parse_mode': 'Markdown'}).encode('utf-8')
req = urllib.request.Request(f'https://api.telegram.org/bot{token}/sendMessage', data=data, headers={'Content-Type': 'application/json'})
urllib.request.urlopen(req)
print('Telegram: enviado com sucesso')
"
```

A mensagem deve ter este formato:
```
*[LinkedIn] Rascunho do dia — AAAA-MM-DD*

<texto completo do post>

---
Fonte: <título> — <link>

Se aprovar: poste no LinkedIn e mova posts/rascunhos/AAAA-MM-DD.md para posts/publicados/
```

Se o envio falhar: mostre o post no chat e avise o Lucas.

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
