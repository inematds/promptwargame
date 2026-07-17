# War Game em Massa

O prompt de war game analisa **um** projeto a fundo. Este modo analisa **vários de uma vez** e responde a pergunta que o outro não responde: _tenho N projetos parados — qual eu faço primeiro, qual eu simplifico, qual eu abandono?_

Use quando você tiver muitos projetos, ideias ou sistemas para comparar, e quiser usar o modelo caro só para **pensar** — deixando a execução, depois, para um modelo barato seguindo o plano já mastigado.

O objetivo aqui **não é executar**. É compreender, comparar, antecipar e priorizar.

---

## 1. Estrutura de pastas

```
analise-projetos/
├── projetos/
│   ├── projeto-01.md
│   ├── projeto-02.md
│   └── projeto-03.md
├── resultados/
├── contexto-geral.md
├── criterios.md
├── ledger.md
├── assumptions.md
└── prompt-mestre.md
```

| Arquivo | Função |
|---|---|
| `projetos/` | Um arquivo por projeto. Nunca junte vários num só — mistura contexto e estraga a comparação. |
| `resultados/` | Recebe as análises geradas. |
| `contexto-geral.md` | O que vale para todos: cenário, recursos, restrições. |
| `criterios.md` | Os mesmos critérios aplicados a todos — é o que torna a comparação possível. |
| `ledger.md` | Bloqueios: informação ausente, decisão pendente, acesso necessário. |
| `assumptions.md` | Tudo que a IA precisou supor, com impacto se estiver errado. |
| `prompt-mestre.md` | O comando que roda a análise em massa. |

O `ledger.md` e o `assumptions.md` são o que impede a análise de virar ficção. Sem eles, o modelo inventa o que falta para conseguir continuar.

---

## 2. Briefing de cada projeto

Versão mínima — comece por ela quando souber pouco:

```markdown
# Projeto — Nome

## O que é?
## O que quero conseguir?
## Como está hoje?
## Qual problema quero resolver?
## O que seria sucesso?
```

Versão completa — quando o projeto já tem corpo, acrescente:

```markdown
## Para quem é?
Quem usa, compra ou se beneficia.

## Problemas conhecidos
Os que você já percebeu.

## Recursos disponíveis
O que já existe: equipe, código, domínio, banco, servidores, conteúdo,
clientes, comunidade, orçamento, modelos de IA, APIs.

## Restrições
O que precisa ser respeitado: orçamento, prazo, equipe, tecnologia
obrigatória, privacidade, rodar localmente, evitar serviços caros.

## Pedido específico para a IA
O que você quer receber desta análise.
```

O que você não souber, deixe em branco. A IA registra como bloqueio — não preencha com chute.

---

## 3. `contexto-geral.md`

```markdown
# Contexto Geral

## Objetivo
Analisar vários projetos para identificar melhorias, riscos, prioridades e oportunidades.

## Situação atual
[Descreva o cenário: quantos projetos, em que estágios, o que já roda em produção.]

## Recursos disponíveis
[Equipe, modelos de IA, infraestrutura, canais, orçamento.]

## Restrições gerais
- reduzir custos
- priorizar soluções simples
- reutilizar o que já existe
- evitar dependências difíceis de manter
- não inventar informação: registrar dúvidas e bloqueios

## Resultado desejado
Uma análise individual por projeto e uma comparação geral que permita decidir
o que executar primeiro, o que simplificar, o que automatizar, o que pausar e
o que abandonar.
```

---

## 4. `criterios.md`

Os mesmos critérios para todos os projetos — sempre.

```markdown
# Critérios Gerais de Análise

## Substância
- Clareza: o projeto está definido de forma inequívoca?
- Problema: existe um problema real sendo resolvido?
- Público: está claro para quem foi criado?
- Valor: gera valor suficiente para o usuário?
- Diferencial: tem vantagem sobre as alternativas existentes?

## Execução
- Viabilidade: dá para executar com os recursos que existem hoje?
- Complexidade: está mais complexo do que precisaria ser?
- Gargalo: qual é o principal fator que impede o avanço?
- Simplificação: o que pode ser removido?
- Automação: quais tarefas podem ser automatizadas?

## Risco
- O que pode impedir o projeto de funcionar?
- Segurança: existem riscos de dados, permissões ou acesso?
- Manutenção: será fácil manter depois de pronto?
- Escalabilidade: cresce sem estourar o custo?

## Retorno
- Receita: como gera retorno financeiro?
- Custo: quais custos podem ser reduzidos?

## Classificação final
- impacto: alto / médio / baixo
- esforço: alto / médio / baixo
- risco: alto / médio / baixo
- prioridade: executar agora / executar depois / estudar melhor / pausar / abandonar
```

---

## 5. `ledger.md` e `assumptions.md`

Comece os dois assim:

```markdown
# Ledger de Bloqueios

Registra: informação ausente, decisão pendente, acesso necessário,
permissão ausente, dependência externa, risco não resolvido.

## Bloqueios encontrados
Nenhum registrado até o momento.
```

```markdown
# Suposições

Para cada suposição: projeto relacionado, suposição feita, motivo,
impacto caso esteja errada, como verificar.

## Suposições registradas
Nenhuma registrada até o momento.
```

Quando faltar uma informação, a IA deve escrever, no ponto exato onde ela faria falta:

```
[PRECISA_DEFINIR: orçamento mensal disponível]
```

---

## 6. Prompt mestre

```markdown
# Prompt Mestre — Análise em Massa

Você é um estrategista técnico, operacional e de negócio.

Existem vários projetos na pasta /projetos. Sua missão é analisar todos em massa.

Você NÃO deve executar os projetos.
Você NÃO deve alterar os arquivos originais.
Você NÃO deve programar nem implementar soluções nesta etapa.

Sua função é analisar, criticar, comparar, simular e preparar planos de melhoria.

Leia: todos os arquivos de /projetos, /contexto-geral.md, /criterios.md,
/ledger.md e /assumptions.md.

Para cada projeto, crie /resultados/resultado-projeto-NN.md contendo:

1. resumo do projeto
2. diagnóstico geral
3. problema real sendo resolvido
4. pontos fortes
5. pontos fracos
6. maior gargalo
7. problemas invisíveis ou não declarados
8. oportunidades
9. melhorias rápidas
10. melhorias estruturais
11. o que pode ser removido ou simplificado
12. o que pode ser automatizado
13. riscos técnicos, de negócio e operacionais
14. dependências externas
15. informações ausentes
16. plano de execução por fases
17. war-game de execução
18. checklist de validação
19. recomendação final
20. modelo de IA indicado para executar

Classifique cada recomendação por impacto, esforço, risco e prioridade,
usando a escala de /criterios.md.

## Formato do war-game

Para cada movimento do plano:

### Ação
O que deve ser feito.
### Resultado esperado
O que acontece se funcionar.
### Sinal de sucesso
Qual evidência confirma que funcionou.
### Sinal de falha
Qual evidência indica que não funcionou.
### Causa provável
A causa mais provável dessa falha.
### Contra-ação
O que fazer para corrigir.
### Caminho alternativo
Qual rota seguir se a correção não resolver.
### Condição de parada
Em qual situação interromper a execução em vez de improvisar.

## Ordem de trabalho

Primeiro gere uma primeira versão da análise de TODOS os projetos.
NÃO aperfeiçoe o primeiro projeto antes de analisar os demais.
Só depois que todas as primeiras versões existirem, revise cada uma.

Atualize /ledger.md sempre que encontrar informação ausente, decisão pendente,
bloqueio, acesso necessário ou risco não resolvido.

Atualize /assumptions.md sempre que precisar assumir alguma informação.

Não invente fatos. Se algo não estiver disponível, registre com clareza.
Seja crítico, direto e específico. Evite recomendação genérica.

## Comparação final

Depois de concluir as análises individuais, crie /resultados/resumo-geral.md
comparando todos os projetos:

1. ranking geral
2. maior potencial
3. menor esforço
4. maior risco
5. retorno mais rápido
6. mais complexo / mais fácil de executar
7. o que fazer primeiro
8. o que pausar
9. o que abandonar
10. projetos que compartilham recursos
11. possíveis integrações entre projetos
12. dependências e gargalos em comum
13. plano recomendado para os próximos 30 dias
14. plano recomendado para os próximos 90 dias
```

---

## 7. Prompt de revisão (segunda rodada)

A primeira rodada quase sempre sai genérica. Rode isto por cima:

```markdown
Revise todos os arquivos dentro de /resultados.

Para cada relatório, procure e corrija:

1. recomendações genéricas
2. contradições
3. riscos ignorados
4. dependências não identificadas
5. etapas sem validação
6. ações sem condição de parada
7. suposições usadas mas não registradas em /assumptions.md

Aprofunde o war-game. Torne as recomendações mais práticas.
Atualize o ledger e as suposições.
Não remova informação útil.
```

Uma terceira rodada, se houver, deve olhar só os projetos prioritários.

---

## 8. Prompt de execução (um projeto por vez)

Analisar pode ser em massa. **Executar, não.** Escolha um projeto e entregue ao executor: briefing original, análise, war-game, critérios de sucesso, ledger atualizado.

```markdown
Você é o executor deste projeto.

Leia: o briefing original, a análise, o war-game, os critérios de sucesso
e o ledger atualizado.

Siga o war-game movimento por movimento. Antes de cada etapa:
1. confirme os pré-requisitos
2. execute a ação
3. verifique o resultado esperado
4. procure o sinal de sucesso
5. procure sinais de falha

Se ocorrer falha:
1. identifique a causa provável
2. aplique a contra-ação
3. teste novamente
4. use o caminho alternativo se necessário

Se encontrar uma condição de parada:
- interrompa a execução
- NÃO invente uma solução
- registre o bloqueio
- explique o que é necessário para continuar

Ao finalizar: rode o checklist, valide os resultados e informe o que foi
concluído, o que ficou pendente e quais riscos permanecem.
```

---

## 9. Qual modelo usar em cada etapa

| Etapa | Modelo |
|---|---|
| Análise estratégica, riscos, problemas invisíveis, war-games, comparação, revisão crítica | O mais avançado |
| Organizar documentos, transformar análise em tarefas, revisar consistência | Intermediário |
| Executar tarefa bem definida, editar arquivos, criar documentação, testes, seguir checklist | O mais barato |

A lógica: **o modelo avançado pensa e antecipa, o intermediário organiza, o barato executa.**

É aqui que o método se paga — o caro só é gasto na parte que exige antecipar o que vai dar errado.

---

## 10. Erros que matam o método

- **Todos os projetos num arquivo só.** Mistura contexto, destrói a comparação.
- **Um prompt diferente por projeto.** Sem critério comum, não existe ranking.
- **Pedir análise e execução juntas.** A IA começa a implementar antes de entender.
- **Não definir sucesso.** O modelo não sabe quando terminou.
- **Não registrar bloqueio.** Ele inventa a informação que falta para poder continuar.
- **Polir o projeto 01 antes de olhar o resto.** Queima o orçamento no primeiro da fila, que raramente é o mais importante.
- **Aceitar análise genérica.** Exija classificação por impacto, esforço, risco e prioridade.
- **Executar tudo ao mesmo tempo.** Análise é em massa; execução é priorizada e uma por vez.

---

## Fluxo completo

1. **Preparação** — criar a estrutura, um arquivo por projeto, contexto, critérios, ledger, suposições.
2. **Análise em massa** — rodar o prompt mestre, gerar a primeira versão de todos.
3. **Revisão** — segunda rodada: caçar genérico, contradição, risco ignorado, ação sem parada.
4. **Comparação** — ranking, prioridades, plano de 30 e 90 dias.
5. **Execução** — um projeto prioritário, movimento por movimento, com o modelo barato.
6. **Aprendizado** — depois de executar, atualizar briefing, análise, ledger, suposições e war-game.

O princípio: **não use a IA só para dizer o que fazer.** Use para simular o que provavelmente vai acontecer, como saber se funcionou, o que pode dar errado, por quê, como reagir e quando parar.
