# Suposições

> Exemplo fictício. Estado depois de duas rodadas de análise.

Para cada suposição: projeto relacionado, suposição feita, motivo, impacto caso esteja errada, como verificar.

## Suposições registradas

### S-01
**Projeto:** 02
**Suposição:** as três falhas conhecidas (áudio cortado, memória no render, token expirado) são as principais causas de re-execução.
**Motivo:** são as únicas relatadas no briefing. Não há registro de execução que confirme.
**Impacto se errada:** **alto — derruba o plano inteiro.** As fases 1-3 estão desenhadas em cima desse diagnóstico. Se a causa dominante for outra, a verificação por etapa ataca o alvo errado.
**Como verificar:** a Fase 1 (registro de execução) confirma ou desmente em duas semanas. É por isso que ela vem primeiro.

### S-02
**Projeto:** 02
**Suposição:** o pós-processamento de cor é imperceptível no resultado final.
**Motivo:** ninguém soube dizer por que a etapa existe.
**Impacto se errada:** baixo e reversível. Se houver diferença visível, restaura-se a etapa.
**Como verificar:** comparação às cegas entre dois renders do mesmo vídeo.

### S-03
**Projeto:** 02
**Suposição:** a velocidade de fala do TTS é estável o suficiente para que a duração do áudio sirva de proxy do texto.
**Motivo:** é a hipótese mais barata de validação de áudio.
**Impacto se errada:** médio. Falso positivo reprova vídeo bom — pior que o problema original. Por isso o movimento tem condição de parada e caminho alternativo (transcrever e comparar).
**Como verificar:** calibrar contra 20 vídeos reais. Depende de B-03.

### S-04
**Projeto:** 03
**Suposição:** existe demanda por uma área de membros paga.
**Motivo:** convicção do dono. **Nenhuma evidência externa.**
**Impacto se errada:** **alto — o projeto inteiro deixa de existir.** É a suposição mais cara do portfólio e a única sustentada só por opinião interna.
**Como verificar:** 5 conversas com pessoas que pagariam. Semana 4 do plano de 30 dias. É a razão de o projeto estar pausado em vez de priorizado.

### S-05
**Projeto:** 01
**Suposição:** o volume de conversas caberia no tier mais barato do modelo.
**Motivo:** sem acesso ao analytics (B-07), estimou-se por porte de site comparável.
**Impacto se errada:** médio. Muda o custo operacional, não a viabilidade.
**Como verificar:** liberar B-07 e olhar o tráfego real.

### S-06
**Projeto:** 04
**Suposição:** os relatórios semanais consomem ~3h.
**Motivo:** estimativa do dono, de memória. Não foi cronometrado.
**Impacto se errada:** médio — é o número que coloca o 04 em primeiro lugar. Se forem 30 minutos, ele cai no ranking e o 02 assume a primeira posição.
**Como verificar:** cronometrar o próximo ciclo. Custa nada e deve ser feito **antes** da semana 1.

### S-07
**Todos**
**Suposição:** os quatro projetos disputam a mesma pessoa e o mesmo tempo.
**Motivo:** o contexto geral fala de um estúdio pequeno, mas não diz o tamanho da equipe.
**Impacto se errada:** **alto — refaz o sequenciamento.** Todo o plano de 30 dias é serial por causa disso. Com duas pessoas, 04 e 02 rodam em paralelo e o calendário encolhe pela metade.
**Como verificar:** perguntar quantas pessoas executam. É a segunda pergunta mais barata do portfólio, depois de S-06.
