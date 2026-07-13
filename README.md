# War Game Prompt

Prompt reutilizável que transforma o planejamento de qualquer build de IA num **war game**: em vez de assumir o caminho feliz de A a B, força a IA a quebrar o projeto em fases, cada uma com objetivo, suposição otimista, suposição pessimista, modos de falha prováveis com correção, critérios de saída verificáveis e orçamento de tentativa — além de uma tabela mestre de riscos (infra, API do modelo, frontend, qualidade de conversa, segurança, loop de aprendizado) e um loop semanal de autoavaliação.

📖 **Guia completo (landing + passo a passo):** https://inematds.github.io/promptwargame/guia/

## Conteúdo

| Arquivo | O que é |
|---|---|
| [`doc/war-game-prompt.md`](doc/war-game-prompt.md) | O prompt em **inglês** |
| [`doc/prompt-war-game-portugues.md`](doc/prompt-war-game-portugues.md) | O prompt em **português** |
| [`doc/war-game.html`](doc/war-game.html) | Dossiê de exemplo (EN) gerado a partir do prompt para o caso PA-CHAT-V0 |
| [`doc/war-game-portugues.html`](doc/war-game-portugues.html) | Dossiê de exemplo (PT-BR) do mesmo caso |

## Como usar

1. Abra `doc/prompt-war-game-portugues.md` (ou a versão EN) e copie o conteúdo inteiro.
2. Preencha os campos entre colchetes (`[PROJETO]`, `[Claude Haiku]`, `[Supabase Edge Functions]`, `[workshops/serviços]` etc.) com os detalhes reais do seu projeto.
3. Cole como a **primeira mensagem** de uma conversa nova com sua IA de planejamento — sem contexto prévio, o prompt já foi desenhado para um cold-start agent.
4. Peça os dois entregáveis: o plano em Markdown e a versão visual em HTML com diagramas.
5. Execute fase por fase, conferindo os critérios de saída antes de avançar.

Veja o passo a passo detalhado, com exemplos, no [guia publicado](https://inematds.github.io/promptwargame/guia/).
