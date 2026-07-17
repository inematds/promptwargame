# War Game Prompt

Prompt reutilizável que transforma o planejamento de qualquer build de IA num **war game**: em vez de assumir o caminho feliz de A a B, força a IA a quebrar o projeto em fases, cada uma com objetivo, suposição otimista, suposição pessimista, modos de falha prováveis com correção, critérios de saída verificáveis, caminho alternativo, condição de parada e orçamento de tentativa — além de uma tabela mestre de riscos (infra, API do modelo, frontend, qualidade de conversa, segurança, loop de aprendizado) e um loop semanal de autoavaliação.

📖 **Guia completo (landing + passo a passo):** https://inematds.github.io/promptwargame/guia/

## Dois modos

| | **War Game** | **War Game em Massa** |
|---|---|---|
| Para | Um projeto, a fundo | Vários projetos, comparados |
| Responde | Como construir isso sem levar porrada no caminho? | Tenho N projetos parados — qual faço primeiro, qual simplifico, qual abandono? |
| Entrega | Plano em fases + tabela de falhas + dossiê HTML | Uma análise por projeto + ranking + plano de 30/90 dias |

Os dois usam a mesma lógica — **ação → reação → contra-ação** — e a mesma regra: prever a barreira antes de escrever a primeira linha de código.

## Conteúdo

| Arquivo | O que é |
|---|---|
| [`doc/war-game-prompt.md`](doc/war-game-prompt.md) | O prompt de um projeto, em **inglês** |
| [`doc/prompt-war-game-portugues.md`](doc/prompt-war-game-portugues.md) | O prompt de um projeto, em **português** |
| [`doc/mass-war-game.md`](doc/mass-war-game.md) | O modo massa, em **inglês** |
| [`doc/war-game-massa-portugues.md`](doc/war-game-massa-portugues.md) | O modo massa, em **português** |
| [`doc/war-game.html`](doc/war-game.html) | Dossiê de exemplo (EN) gerado a partir do prompt para o caso PA-CHAT-V0 |
| [`doc/war-game-portugues.html`](doc/war-game-portugues.html) | Dossiê de exemplo (PT-BR) do mesmo caso |

## Como usar — um projeto

1. Abra `doc/prompt-war-game-portugues.md` (ou a versão EN) e copie o conteúdo inteiro.
2. Preencha os campos entre colchetes (`[PROJETO]`, `[Claude Haiku]`, `[Supabase Edge Functions]`, `[workshops/serviços]` etc.) com os detalhes reais do seu projeto.
3. Cole como a **primeira mensagem** de uma conversa nova com sua IA de planejamento — sem contexto prévio, o prompt já foi desenhado para um cold-start agent.
4. Peça os dois entregáveis: o plano em Markdown e a versão visual em HTML com diagramas.
5. Execute fase por fase, conferindo os critérios de saída antes de avançar.

Veja o passo a passo detalhado, com exemplos, no [guia publicado](https://inematds.github.io/promptwargame/guia/).

## Como usar — vários projetos

1. Abra `doc/war-game-massa-portugues.md` (ou a versão EN) e monte a estrutura de pastas que ele descreve.
2. Escreva **um arquivo por projeto** — nunca todos num só. Comece pelo briefing mínimo (5 perguntas); o que você não souber, deixe em branco.
3. Preencha `contexto-geral.md` e `criterios.md`. São eles que tornam os projetos comparáveis.
4. Rode o **prompt mestre** com o modelo mais capaz. Ele gera uma primeira versão de todos, sem polir nenhum.
5. Rode o **prompt de revisão** por cima — é essa segunda rodada que tira o genérico.
6. Leia o `resumo-geral.md`, escolha **um** projeto e entregue o war-game dele ao modelo barato com o prompt de execução.

O modelo caro pensa e antecipa. O barato executa o plano já mastigado.

