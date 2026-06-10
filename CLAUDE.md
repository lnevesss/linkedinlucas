# LinkedInLucas — Automação de posts de LinkedIn

Este projeto é uma **automação dentro do Claude Code** para criar posts de LinkedIn sobre
**wellness** para o Lucas, ajudando-o a construir uma marca pessoal forte na área.

> Não existe aplicação/código de app aqui. Tudo acontece via Claude Code: subagents, skills,
> arquivos de contexto e (depois) agendamento na nuvem. A publicação no LinkedIn é **manual** —
> a automação entrega o rascunho pronto por e-mail para o Lucas copiar e postar.

## Sobre o autor

- **Lucas** trabalha no **WellHub** (plataforma de benefício corporativo de bem-estar).
- Acredita no crescimento do mercado de **wellness** e quer ser referência no tema.
- Detalhes completos em [context/sobre-lucas.md](context/sobre-lucas.md).

## Regras sempre válidas

1. **Idioma dos posts: Português (pt-BR).**
2. **Formato: somente texto** (sem imagem por enquanto).
3. **Aprovação por e-mail:** o rascunho final vai para `nevess.lucas@gmail.com`. Lucas aprova e
   posta manualmente. Nunca assuma que algo foi publicado.
4. **Voz autêntica:** sempre seguir [context/voz-e-tom.md](context/voz-e-tom.md). Evitar jargão
   vazio, clichês de LinkedIn ("estou muito feliz em compartilhar...") e autopromoção exagerada.
5. **Sem repetição:** antes de escolher um tema, conferir [posts/publicados/](posts/publicados/)
   para não repetir assunto recente.
6. **Fontes reais:** toda notícia citada precisa ter link verificável e data. Nunca inventar dados.

## O pipeline (4 etapas)

A skill `/criar-post-linkedin` orquestra tudo, chamando um subagent por etapa:

| Etapa | Subagent | Saída |
|-------|----------|-------|
| 1. Pesquisar notícias | `pesquisador-wellness` | `pesquisas/AAAA-MM-DD.md` |
| 2. Escolher a melhor | `curador-noticias` | seção "Escolhida" no arquivo de pesquisa |
| 3. Escrever o post | `redator-linkedin` | `posts/rascunhos/AAAA-MM-DD.md` |
| 4. Enviar para aprovação | (a própria skill, via MCP Gmail) | e-mail para o Lucas |

## Onde fica cada coisa

- `context/` — **referências** que definem quem é o Lucas e como ele escreve. Editar à vontade.
- `.claude/agents/` — os subagents (um por etapa).
- `.claude/skills/` — a skill que orquestra o pipeline.
- `pesquisas/` — notícias pesquisadas (uma por execução).
- `posts/rascunhos/` — posts aguardando aprovação.
- `posts/publicados/` — histórico do que já foi ao ar (mover para cá após postar).

## Convenção de datas

Arquivos usam o formato `AAAA-MM-DD` (ex: `2026-06-10.md`), sempre no fuso de Brasília.
