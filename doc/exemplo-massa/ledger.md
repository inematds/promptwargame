# Ledger de Bloqueios

> Exemplo fictício. Estado depois de duas rodadas de análise.

Registra: informação ausente, decisão pendente, acesso necessário, permissão ausente, dependência externa, risco não resolvido.

## Bloqueios encontrados

### B-01 · Volume alvo de publicação — DECISÃO PENDENTE
**Projetos:** 02, 03
**O que falta:** quantos vídeos por semana o canal quer publicar.
**Por que trava:** sem isso não se sabe se a Fase 4 do projeto 02 (retomabilidade) se paga, nem se o projeto 03 tem lastro de conteúdo.
**Quem resolve:** o dono. Não é falta de informação — é uma decisão que ninguém tomou.
**Status:** aberto desde a 1ª rodada. **É o bloqueio de maior alcance do portfólio.**

### B-02 · Taxa de re-execução do pipeline — INFORMAÇÃO AUSENTE
**Projeto:** 02
**O que falta:** quantos vídeos precisam ser refeitos hoje.
**Por que trava:** é o número que dimensiona o ganho da verificação por etapa. Sem ele, o benefício é argumentado, não medido.
**Como obter:** a Fase 1 (registro de execução) responde sozinha em duas semanas de uso.
**Status:** aberto — mas com data de validade. Não bloqueia o começo.

### B-03 · Histórico para calibrar a validação de áudio — INFORMAÇÃO AUSENTE
**Projeto:** 02
**O que falta:** 20 vídeos com roteiro **e** áudio preservados.
**Por que trava:** é a condição de parada do Movimento 2. Sem histórico, a margem é chute e o pipeline reprova vídeo bom.
**Como obter:** verificar se os áudios dos vídeos publicados foram guardados.
**Status:** aberto. **Verificar antes de começar a Fase 2** — se não existirem, o movimento muda para o caminho alternativo (transcrever e comparar).

### B-04 · Expiração do token de upload — INFORMAÇÃO AUSENTE
**Projeto:** 02
**O que falta:** de quanto em quanto tempo o token do canal expira.
**Por que trava:** define se o retry resolve o problema de upload ou se é preciso renovar credencial no meio da execução.
**Como obter:** documentação da API do canal.
**Status:** aberto, baixo impacto.

### B-05 · Versão do ffmpeg não fixada — RISCO NÃO RESOLVIDO
**Projeto:** 02
**O que falta:** nada — é uma correção, não uma informação.
**Por que está aqui:** uma atualização de sistema derruba o pipeline sem aviso, e ninguém saberia por quê.
**Status:** endereçado na Fase 1. Sai do ledger quando a versão estiver declarada.

### B-06 · Validação de demanda do projeto 03 — DECISÃO PENDENTE
**Projeto:** 03
**O que falta:** evidência, vinda de fora de casa, de que alguém paga.
**Por que trava:** é a premissa sobre a qual o projeto inteiro se apoia. Toda estimativa do 03 depende dela e nenhuma análise a substitui.
**Como obter:** 5 conversas. Está no plano de 30 dias, semana 4.
**Status:** aberto. **Enquanto não fechar, nenhum código do 03.**

### B-07 · Acesso ao painel de analytics do site — ACESSO NECESSÁRIO
**Projeto:** 01
**O que falta:** credencial de leitura.
**Por que trava:** sem tráfego real não dá para estimar volume de conversas nem custo do modelo no projeto 01.
**Status:** aberto.

---

## Resolvidos

### B-00 · Qual modelo usaria o chat do projeto 01 — RESOLVIDO na 2ª rodada
Estava marcado como bloqueio na 1ª rodada. O briefing já respondia — a informação existia, a análise é que não tinha lido com atenção. Removido.
