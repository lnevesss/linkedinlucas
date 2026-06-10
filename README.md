# LinkedInLucas 🧘

Automação para criar posts de LinkedIn sobre **wellness**, feita 100% dentro do **Claude Code**.
Ela pesquisa notícias, escolhe a melhor, escreve o post em português e te envia por e-mail para
você aprovar e postar.

---

## Como funciona (visão geral)

```
  /criar-post-linkedin
          │
          ▼
  1. pesquisador-wellness   →  busca notícias de wellness na web
          │
          ▼
  2. curador-noticias       →  escolhe a melhor (engajamento + seu contexto)
          │
          ▼
  3. redator-linkedin       →  escreve o post em PT, na sua voz
          │
          ▼
  4. e-mail (Gmail)         →  rascunho chega em nevess.lucas@gmail.com
                               você revisa, aprova e posta no LinkedIn
```

## Entendendo as peças do Claude Code (você é novo nisso 👇)

| Peça | O que é | Onde está |
|------|---------|-----------|
| **CLAUDE.md** | Instruções lidas automaticamente toda vez. É o "cérebro" do projeto. | [CLAUDE.md](CLAUDE.md) |
| **context/** | Arquivos com o seu conhecimento: quem você é, como escreve, seus temas. | [context/](context/) |
| **Subagents** | Assistentes especializados, um para cada etapa. | [.claude/agents/](.claude/agents/) |
| **Skill** | Um comando (`/criar-post-linkedin`) que roda o processo inteiro. | [.claude/skills/](.claude/skills/) |
| **Agendamento** | Faz o processo rodar sozinho em horários fixos (configuramos depois). | — |

> 💡 A regra de ouro: **a qualidade dos posts depende da qualidade do `context/`.** Quanto melhor
> você preencher esses arquivos com a sua voz e seus exemplos, melhores ficam os posts.

---

## Primeiros passos

### 1. Preencha o `context/` (mais importante!)
Abra os arquivos em [context/](context/) e complete os trechos marcados com `> TODO:`.
Priorize:
- [context/voz-e-tom.md](context/voz-e-tom.md) — como você fala.
- [context/exemplos-de-posts.md](context/exemplos-de-posts.md) — cole 2–3 posts que você admira.
- [context/sobre-lucas.md](context/sobre-lucas.md) — sua trajetória e objetivos.

### 2. Rode o pipeline
No Claude Code, digite:
```
/criar-post-linkedin
```
Isso pesquisa, escolhe, escreve e (após autenticar o Gmail) envia o rascunho por e-mail.

### 3. Aprove e poste
Revise o e-mail / o arquivo em [posts/rascunhos/](posts/rascunhos/). Se aprovar, poste no
LinkedIn e **mova o arquivo para `posts/publicados/`** (isso evita repetir temas no futuro).

### 4. (Depois) Agende
Quando os posts estiverem com a sua cara, peça ao Claude para agendar o `/criar-post-linkedin`
(ex: seg/qua/sex de manhã). Antes disso é preciso autenticar o **MCP Gmail**.

---

## Estrutura de pastas

```
LinkedinLucas/
├── CLAUDE.md              # regras sempre carregadas
├── README.md             # este arquivo
├── .claude/
│   ├── agents/           # os 3 subagents
│   └── skills/           # a skill orquestradora
├── context/              # SUAS referências (edite aqui)
├── pesquisas/            # notícias pesquisadas (gerado automaticamente)
└── posts/
    ├── rascunhos/        # posts aguardando sua aprovação
    └── publicados/       # o que já foi ao ar
```
