# Resumo Geral — Comparação dos 4 projetos

> Exemplo fictício. Saída do prompt mestre após a rodada de revisão.

## 1. Ranking geral

| # | Projeto | Impacto | Esforço | Risco | Prioridade |
|---|---|---|---|---|---|
| 1º | **04** — Automação de relatórios | Médio | Baixo | Baixo | Executar agora |
| 2º | **02** — Pipeline de vídeos | Alto | Médio | Baixo | Executar agora (fases 1-3) |
| 3º | **01** — Chat com tour guiado | Alto | Alto | Alto | Estudar melhor |
| 4º | **03** — Área de membros | Alto | Alto | Alto | Pausar |

O ranking não segue o entusiasmo. O projeto mais interessante do portfólio (03) é o último; o mais chato (04) é o primeiro, porque é o único que devolve tempo já na primeira semana — e é esse tempo que paga os outros.

## 2. Maior potencial

**Projeto 03 (área de membros).** É o único com receita recorrente. Também é o único que ainda não existe fora da cabeça do dono — potencial alto e evidência zero.

## 3. Menor esforço

**Projeto 04.** Dois dias. Já roda; só é frágil.

## 4. Maior risco

**Projeto 03.** Não por complexidade técnica, mas porque nada foi validado: não se sabe se alguém paga. Um risco de premissa é mais caro que um risco de implementação — você descobre tarde e o gasto já foi feito.

Em segundo, o **01**: depende de qualidade de conversa, que é o tipo de coisa que só se mede com visitante real.

## 5. Retorno mais rápido

**Projeto 04.** Devolve ~3h por semana a partir do primeiro dia útil depois de pronto.

## 6. Mais complexo / mais fácil de executar

- **Mais complexo:** 01. Frontend, modelo, banco, segurança e qualidade de conversa, cada um com seu modo de falha, todos acoplados.
- **Mais fácil:** 04. Uma automação linear com um único ponto de falha conhecido.

## 7. O que fazer primeiro

**04, depois 02.**

O motivo não é o ranking em si — é sequência. O 04 devolve tempo; o tempo devolvido é o que financia o 02. Fazer o 02 antes significa gastar 3,5 dias que você não tem, na semana em que os relatórios ainda comem 3h.

## 8. O que pausar

**Projeto 03.** Não por ser ruim — por ser cedo. Pausar aqui significa: nada de código até que a pergunta "alguém paga por isso?" tenha uma resposta que não venha de dentro de casa.

Custo de pausar: zero. Não há nada construído.

## 9. O que abandonar

Nada, ainda. Mas o **01** vira candidato se, em 90 dias, os testes de conversa continuarem sem visitante real. Um protótipo que não é exposto a usuário não amadurece — só envelhece.

## 10. Projetos que compartilham recursos

- **02 e 01** compartilham o render HTML→MP4 (o 01 usaria para o tour narrado).
- **02 e 04** compartilham o mesmo padrão de falha: etapas encadeadas sem verificação. A correção do 02 é reaproveitável.
- **01 e 03** compartilham autenticação e banco — se ambos avançarem, a decisão de auth deve ser tomada uma vez só, e antes dos dois.

## 11. Possíveis integrações

- O chat do **01** é o canal natural de venda do **03**. Mas isso é uma armadilha de sequência: só integrar depois que os dois existirem separadamente. Acoplar agora faz dois projetos incertos virarem um projeto incerto e maior.
- Os relatórios do **04** poderiam alimentar as métricas do **02** (taxa de re-execução, volume publicado). Barato e útil — é como o 02 ganharia o número que hoje falta.

## 12. Dependências e gargalos em comum

**O gargalo comum é a falta de verificação.** Aparece nos projetos 02 e 04 com a mesma cara: o processo termina sem saber se deu certo, e o humano vira o validador.

Corrigir isso duas vezes é aceitável. Na terceira ocorrência (se o 01 avançar), extraia o padrão — não antes.

**A dependência comum de decisão** é o volume alvo de publicação, que trava a Fase 4 do 02 e a viabilidade inteira do 03. É uma pergunta só, e destrava dois projetos.

## 13. Plano recomendado — próximos 30 dias

| Semana | O quê |
|---|---|
| 1 | Projeto 04, fases 1-2. Sai frágil, entra confiável. Devolve 3h/semana. |
| 2-3 | Projeto 02, fases 1-3 (enxergar, verificar, podar). Não passar da 3. |
| 4 | Projeto 03: **uma** conversa de validação com 5 pessoas que pagariam. Zero código. |

Ao fim dos 30 dias você deve ter: dois sistemas que avisam quando quebram, ~5h/semana devolvidas, e uma resposta sobre o 03 vinda de fora de casa.

## 14. Plano recomendado — próximos 90 dias

Depende inteiramente do que a semana 4 responder.

- **Se o 03 validar:** ele passa a ser prioridade 1, e a decisão de auth (comum com o 01) deve ser tomada antes de qualquer código.
- **Se o 03 não validar:** arquive e coloque o 01 na frente — com um limite duro: se em 90 dias o chat não tiver conversado com visitante real, abandone.
- **Independente disso:** a Fase 4 do 02 só acontece se o volume alvo tiver sido respondido e for maior que o atual.

## 15. A decisão que destrava tudo

Uma pergunta, dois projetos: **qual é o volume alvo de publicação?**

Está no ledger desde a primeira rodada e continua sem resposta. Nenhuma análise adicional resolve — é uma decisão do dono, não um problema de informação.

Enquanto ela não vier, o 02 para na Fase 3 e o 03 fica pausado. Isso não é um bloqueio da análise; é o resultado dela.
