# Resultado — Projeto 02: Pipeline de vídeos automatizado

> Exemplo fictício. Saída do prompt mestre após a rodada de revisão.

## 1. Resumo do projeto

Pipeline que transforma um roteiro em texto num vídeo publicado: gera a narração por TTS, monta as cenas a partir de templates HTML, renderiza em MP4 e sobe para o canal. Hoje roda de ponta a ponta, mas só com acompanhamento manual em três pontos.

## 2. Diagnóstico geral

O projeto não tem um problema de capacidade — tem um problema de **confiabilidade**. As peças funcionam isoladas; o que falha é a costura entre elas, sempre nos mesmos lugares (TTS que corta a última frase, render que estoura memória em vídeos longos, upload que expira o token).

O dono do projeto trata cada falha como incidente pontual e conserta na mão. Em três meses isso consumiu mais horas do que reescrever a costura levaria. É um caso clássico de custo invisível: nenhuma falha isolada justifica a refatoração, mas a soma delas já pagou por ela duas vezes.

## 3. Problema real sendo resolvido

Reduzir o custo por vídeo publicado — de ~4h de trabalho manual para minutos de máquina. O problema é real e já foi validado: o pipeline existente, mesmo frágil, já entregou vídeos.

## 4. Pontos fortes

- Já funciona de ponta a ponta — não é uma aposta, é um sistema com histórico.
- Roda local, sem dependência de serviço pago no caminho crítico.
- Cada etapa é um processo separado, o que torna a costura substituível sem reescrever o miolo.
- O template HTML→MP4 é reaproveitável pelos projetos 01 e 04.

## 5. Pontos fracos

- Nenhuma etapa tem verificação automática de sucesso: o pipeline "termina" mesmo tendo produzido um vídeo quebrado.
- O estado vive na cabeça do operador — não há registro do que rodou, quando, com qual entrada.
- Falha silenciosa: quando o TTS corta a frase, só se descobre assistindo o vídeo pronto.
- Sem retry. Qualquer erro de rede derruba a execução inteira e obriga a recomeçar do zero.

## 6. Maior gargalo

**A ausência de verificação por etapa.** Não é o render, não é o TTS — é o fato de nenhuma etapa saber dizer se deu certo. Isso força o humano a ser o validador de todas elas, o que anula boa parte da automação e explica as 3 intervenções manuais que sobraram.

## 7. Problemas invisíveis ou não declarados

- **O custo real não é o de render, é o de re-render.** Um vídeo que sai quebrado no fim consome o dobro. Isso não aparece em nenhuma métrica atual porque ninguém conta re-execuções.
- **A fragilidade está segurando o volume.** O dono publica menos do que quer porque cada publicação exige atenção — o gargalo virou psicológico antes de virar técnico.
- **Dependência de uma versão específica do ffmpeg** que não está fixada em lugar nenhum. Uma atualização do sistema derruba o pipeline sem aviso.
- Nada disso estava no briefing. Os três saíram do cruzamento entre "problemas conhecidos" e "estado atual".

## 8. Oportunidades

- A costura confiável é reaproveitável: os projetos 01 e 04 têm o mesmo padrão (etapas encadeadas sem verificação).
- Com registro de execução, o pipeline vira fonte de dados sobre o que realmente falha — hoje isso é anedota.
- Publicação previsível abre a porta para escala de volume sem contratar ninguém.

## 9. Melhorias rápidas

| Ação | Impacto | Esforço | Risco | Prioridade |
|---|---|---|---|---|
| Fixar a versão do ffmpeg e registrar em um arquivo de ambiente | Médio | Baixo | Baixo | Agora |
| Validar duração do áudio TTS contra a contagem de caracteres do roteiro (detecta a frase cortada) | Alto | Baixo | Baixo | Agora |
| Logar cada execução em um arquivo: entrada, etapa, saída, duração, resultado | Alto | Baixo | Baixo | Agora |
| Retry com backoff no upload | Médio | Baixo | Baixo | Agora |

## 10. Melhorias estruturais

| Ação | Impacto | Esforço | Risco | Prioridade |
|---|---|---|---|---|
| Dar a cada etapa um sinal de sucesso verificável e fazer o pipeline parar quando ele não aparecer | Alto | Médio | Baixo | Agora |
| Tornar cada etapa retomável, para que uma falha no fim não obrigue a refazer o começo | Alto | Médio | Médio | Depois |
| Extrair a costura para um orquestrador reutilizável pelos projetos 01 e 04 | Médio | Alto | Médio | Estudar melhor |

## 11. O que pode ser removido ou simplificado

- **A etapa de pós-processamento de cor** roda em todos os vídeos e é imperceptível no resultado final. Remover corta ~20% do tempo de render sem perda visível.
- **Dois templates HTML dos cinco existentes nunca foram usados.** Manter os cinco custa manutenção; remover os dois é gratuito.
- A conversão intermediária para PNG antes do MP4 pode ser eliminada — o render já aceita o HTML direto.

## 12. O que pode ser automatizado

- A validação do áudio (hoje: assistir o vídeo).
- A escolha do template por tipo de roteiro (hoje: manual, e sempre o mesmo).
- A publicação em si, **mas só depois** que a verificação por etapa existir. Automatizar a publicação antes disso apenas faz o vídeo quebrado chegar ao público mais rápido.

## 13. Riscos

**Técnicos**
- Atualização do sistema quebra o ffmpeg → pipeline morre sem aviso. *Mitigação: fixar versão (item 9).*
- Vídeos longos estouram a memória no render. *Mitigação: limite de duração por segmento até haver medição real.*

**De negócio**
- Publicar um vídeo quebrado custa mais que não publicar. Hoje nada impede isso.
- O ganho de tempo só se materializa se o volume aumentar; se o dono continuar publicando o mesmo tanto, a refatoração não se paga.

**Operacionais**
- Uma pessoa só entende a costura. Se ela parar, o pipeline para.
- Sem registro de execução, um erro intermitente é indepurável — só sobra o relato.

## 14. Dependências externas

- ffmpeg (versão não fixada — ver ledger)
- Motor de TTS local
- API de upload do canal, com token que expira `[PRECISA_DEFINIR: periodicidade de expiração do token de upload]`

## 15. Informações ausentes

- Volume alvo de vídeos por semana — sem isso não dá para dizer se a refatoração se paga.
- Taxa atual de re-execução (quantos vídeos precisam ser refeitos).
- Duração máxima real de um vídeo do canal.

Todas registradas em `ledger.md`.

## 16. Plano de execução por fases

**Fase 1 — Enxergar (1 dia)**
Registro de execução + fixar ffmpeg. Nada é corrigido aqui; o objetivo é parar de trabalhar às cegas.
*Critério de saída:* toda execução gera uma linha de log com entrada, etapas, resultado e duração.

**Fase 2 — Verificar (2 dias)**
Sinal de sucesso por etapa, começando pela validação do áudio, que é a falha mais cara.
*Critério de saída:* um vídeo com áudio cortado é reprovado pelo pipeline sem intervenção humana.

**Fase 3 — Podar (meio dia)**
Remover o pós-processamento de cor, os dois templates mortos e a conversão intermediária.
*Critério de saída:* mesmo resultado visual, tempo de render medido antes e depois.

**Fase 4 — Retomar (3 dias, só se a Fase 2 se provar)**
Tornar as etapas retomáveis.
*Critério de saída:* uma falha na última etapa não obriga a refazer as anteriores.

## 17. War-game de execução

### Movimento 1 — Instrumentar o pipeline com registro de execução

**Ação**
Envolver cada etapa com um wrapper que grava entrada, saída, duração e resultado num arquivo de log.

**Resultado esperado**
Toda execução passa a deixar rastro, sem alterar o comportamento do pipeline.

**Sinal de sucesso**
Rodar um vídeo conhecido de ponta a ponta produz um log com todas as etapas na ordem, e o MP4 sai idêntico ao de antes.

**Sinal de falha**
O log sai incompleto (etapas faltando), ou o vídeo muda, ou o pipeline fica mais lento de forma perceptível.

**Causa provável**
Etapas que terminam por caminhos não previstos (exceção engolida, processo que morre sem retorno) e escapam do wrapper.

**Contra-ação**
Instrumentar no ponto de entrada de cada processo em vez de envolver por fora; forçar toda saída a passar por um único ponto.

**Caminho alternativo**
Se a costura não permitir um ponto único de saída, logar de fora via arquivo-sentinela por etapa — mais grosseiro, mas suficiente para enxergar.

**Condição de parada**
Se instrumentar exigir reescrever a costura, **pare**. Isso é a Fase 4, não a 1. Registre no ledger e reavalie a ordem das fases — não emende a refatoração aqui.

---

### Movimento 2 — Validar o áudio contra o roteiro

**Ação**
Comparar a duração do áudio gerado com a duração estimada a partir da contagem de caracteres do roteiro, e reprovar fora de uma margem.

**Resultado esperado**
Áudio cortado é detectado antes do render, e não depois da publicação.

**Sinal de sucesso**
Um roteiro sabidamente problemático (o caso da frase cortada) é reprovado. Dez roteiros normais passam sem falso positivo.

**Sinal de falha**
Falso positivo em roteiro bom, ou o caso conhecido passa batido.

**Causa provável**
A margem foi calibrada com poucos exemplos; velocidade de fala varia por pontuação, números e siglas.

**Contra-ação**
Calibrar com os últimos 20 vídeos reais — não com estimativa teórica. Ajustar a margem até zero falso positivo no histórico.

**Caminho alternativo**
Se a duração não discriminar bem, transcrever o áudio gerado e comparar o texto com o roteiro. Mais caro por vídeo, mas decisivo.

**Condição de parada**
Se não houver 20 vídeos com roteiro **e** áudio preservados para calibrar, **pare**. Sem histórico, qualquer margem é chute e o pipeline passa a reprovar vídeo bom — pior que o problema original. Registre a necessidade no ledger.

---

### Movimento 3 — Podar o pós-processamento de cor

**Ação**
Remover a etapa e medir o tempo de render antes e depois.

**Resultado esperado**
Render mais rápido, resultado visualmente indistinguível.

**Sinal de sucesso**
Redução medida no tempo, e ninguém identifica qual vídeo é qual numa comparação às cegas.

**Sinal de falha**
Diferença visível, especialmente em cenas escuras.

**Causa provável**
A etapa estava compensando alguma coisa que ninguém documentou — provavelmente contraste do template.

**Contra-ação**
Corrigir na origem (o CSS do template) em vez de manter uma etapa de correção no fim do pipeline.

**Caminho alternativo**
Manter a etapa apenas para os templates que precisam dela, em vez de aplicar a todos.

**Condição de parada**
Nenhuma — este movimento é reversível por completo. Se der errado, reverta e siga.

## 18. Condições de parada do projeto

- **Se o volume alvo for igual ao atual**, pare depois da Fase 3. As Fases 4+ não se pagam: você estaria endurecendo um sistema que já dá conta do que se pede dele.
- **Se a Fase 2 revelar que as falhas não são as três conhecidas**, pare e reanalise. O plano inteiro está apoiado nesse diagnóstico.

## 19. Checklist de validação

- [ ] Toda execução deixa registro
- [ ] Versão do ffmpeg fixada e declarada
- [ ] Um áudio cortado é reprovado sem humano
- [ ] Nenhum falso positivo em 20 vídeos do histórico
- [ ] Tempo de render medido antes e depois da poda
- [ ] Nenhum vídeo publicado sem passar por todos os sinais de sucesso

## 20. Recomendação final

**Prioridade: executar agora — mas só as Fases 1 a 3.**

Impacto alto, esforço baixo, risco baixo. São ~3,5 dias que atacam o gargalo real (ausência de verificação) sem tocar na arquitetura.

A Fase 4 (retomabilidade) fica **condicionada** ao volume alvo, que hoje é desconhecido. É a decisão de maior valor pendente neste projeto e depende de uma resposta do dono, não de mais análise.

Não faça a extração do orquestrador agora. Ela só se justifica se os projetos 01 e 04 avançarem — e o 01 ainda é protótipo. Reavaliar em 90 dias.

## 21. Modelo de IA indicado para executar

**Modelo barato.** As Fases 1 a 3 são tarefas bem definidas, com sinal de sucesso explícito e checklist — exatamente o perfil de execução mecânica.

Suba para o intermediário na Fase 4, se ela acontecer: retomabilidade exige decisão de arquitetura sobre onde guardar o estado.
