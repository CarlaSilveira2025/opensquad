# Anti-Patterns — Produção de Conteúdo LAIA

Erros por fase, com sintoma observável, causa e correção.

---

## Fase 3.1 — Pesquisa

### 1.1 Citar número sem abrir a fonte
**Sintoma:** o conteúdo é corrigido nos comentários e o cliente perde autoridade justamente
no post que deveria construí-la.
**Correção:** `web_fetch` na fonte, confirmação do número e do contexto, antes de registrar.

### 1.2 Dado sem data
**Sintoma:** estatística de 2019 apresentada como atual; o conteúdo nasce velho.
**Correção:** número, fonte **e** data. Falta um dos três, o achado é rebaixado.

### 1.3 Inventar pergunta frequente
**Sintoma:** o conteúdo responde uma dúvida que ninguém tem.
**Correção:** observar em buscas relacionadas e comentários; registrar onde foi observada.

### 1.4 Simular post de concorrente
**Sintoma:** lacuna apontada onde há cobertura densa, e vice-versa.
**Correção:** declarar a coleta parcial. Parcial declarada vale mais que completa inventada.

### 1.5 Propor ângulo na pesquisa
**Sintoma:** a Fase 3.2 gera cinco variações do ângulo que o pesquisador sugeriu.
**Correção:** o relatório descreve cenário; a lente é da Ângela.

---

## Fase 3.2 — Ângulos

### 2.1 Gerar cinco pautas em vez de cinco ângulos
**Sintoma:** o usuário escolhe um "ângulo" e percebe que escolheu outro assunto.
**Causa:** confundir subtema com lente emocional.
**Correção:** todos os ângulos partem da mesma tensão central. Se o assunto muda, é pauta.

### 2.2 Repetir o mesmo ângulo com sinônimos
**Sintoma:** cinco opções que na prática são três.
**Correção:** teste de distinção — se dois aceitam o mesmo slide 1, refazer um.

### 2.3 Ângulo sem lastro em dado
**Sintoma:** o criador chega na escrita sem material e preenche com generalidade.
**Correção:** `ancora_pesquisa` obrigatória em todo ângulo.

### 2.4 Inflacionar a provocação
**Sintoma:** tudo classificado como 4 ou 5, e a escala perde a função de informar risco.
**Correção:** distribuir os níveis conforme o que cada ângulo realmente confronta.

### 2.5 Omitir o risco de ângulo agressivo
**Sintoma:** o usuário aprova sem saber e descobre nos comentários.
**Correção:** risco declarado e específico em todo ângulo ≥ 4.

---

## Fase 3.3 — Ganchos

### 3.1 Três ganchos do mesmo tipo
**Sintoma:** o usuário acha que escolhe entre três opções e escolhe entre três redações.
**Correção:** três tipos diferentes entre os cinco canônicos.

### 3.2 Inventar número no gancho
**Sintoma:** a primeira frase que o público lê é a mais fácil de checar — e está errada.
**Correção:** conferir contra o relatório; mesma grandeza, mesmo recorte.

### 3.3 Gancho longo
**Sintoma:** no carrossel sai ilegível; no LinkedIn é cortado no meio pelo "ver mais".
**Correção:** máximo 2 linhas; contar caracteres nos de LinkedIn.

### 3.4 Fórmula batida
**Sintoma:** "você sabia que" é reconhecido como ruído e ignorado antes de ser lido.
**Correção:** abrir pela tensão, não pelo anúncio de que há tensão.

### 3.5 Promessa que o ângulo não cumpre
**Sintoma:** salvamento sem leitura, comentário irritado, e o algoritmo aprende a mostrar o
conteúdo para quem vai abandoná-lo.
**Correção:** campo `promessa` conferido contra o resumo do ângulo.

---

## Fase 3.4 — Conteúdo

### 4.1 Reescrever o gancho aprovado
**Sintoma:** o texto não corresponde ao que o usuário aprovou no checkpoint.
**Correção:** o gancho entra literal. Ajuste, só via checkpoint 06.

### 4.2 Slide com parágrafo
**Sintoma:** corpo minúsculo na imagem; o leitor pula e a entrega dos slides seguintes cai.
**Correção:** ~30 palavras por slide, contadas antes de fechar.

### 4.3 Slides sem progressão
**Sintoma:** o carrossel podia terminar no slide 4 sem perda.
**Teste:** se dois slides trocam de lugar sem prejuízo, falta progressão.

### 4.4 CTA genérico
**Sintoma:** o slide de maior intenção não gera ação.
**Correção:** CTA que cita o tema — "salva pra quando alguém te disser que X".

### 4.5 Terminar sem reflexão
**Sintoma:** conteúdo lido e esquecido, sem salvamento.
**Correção:** slide de reflexão obrigatório antes do CTA.

### 4.6 LinkedIn abrindo com tese abstrata
**Sintoma:** "A IA está mudando o trabalho" não faz ninguém parar.
**Correção:** cena concreta primeiro; a tese depois.

### 4.7 Copiar o carrossel para o LinkedIn
**Sintoma:** post picotado, sem fluxo, com cara de texto reaproveitado.
**Correção:** mesmo ângulo, execução diferente.

### 4.8 Ignorar `palavras_evitar`
**Sintoma:** a voz da marca quebra no conteúdo mais visível dela.
**Correção:** conferir a lista antes de fechar cada peça.

---

## Fase 3.5 — Visual

### 5.1 Inventar cor fora da paleta
**Sintoma:** o cliente percebe na hora que o conteúdo não é dele.
**Correção:** apenas hex de `visual.paleta`; neutros puros permitidos. Sem paleta válida,
parar e reportar.

### 5.2 Cortar texto para caber
**Sintoma:** some justamente a palavra que passou por aprovação.
**Correção:** ajustar o design — corpo menor dentro da escala, mais área, outra composição.

### 5.3 Fonte pequena demais
**Sintoma:** slide ilegível no feed; o carrossel inteiro é descartado.
**Correção:** mínimo 32px em peça de 1080px.

### 5.4 Estilo variando entre slides
**Sintoma:** o carrossel parece montado por pessoas diferentes.
**Correção:** sistema visual definido uma vez, aplicado a todos.

### 5.5 Dimensão errada
**Sintoma:** o Instagram corta a imagem, geralmente decepando texto.
**Correção:** 1080×1350 no carrossel; conferir cada PNG renderizado.

### 5.6 Renderizar sem inspecionar
**Sintoma:** imagem em branco ou com texto transbordando chega à entrega.
**Correção:** abrir cada PNG com a ferramenta Read antes de entregar.

### 5.7 HTML com referência externa
**Sintoma:** fonte ou imagem não carrega no headless e o slide sai quebrado.
**Correção:** CSS inline, fontes com fallback de sistema, imagens locais.

---

## Revisão

### 6.1 Aprovar com dado sem lastro
**Sintoma:** informação falsa publicada no nome do cliente.
**Correção:** veracidade é eliminatória — nota abaixo de 8 reprova sozinha.

### 6.2 Nota geral sem notas por eixo
**Sintoma:** o criador não sabe o que corrigir no ciclo de rejeição.
**Correção:** cinco notas, com o cálculo da ponderação explicitado.

### 6.3 Auditar só o texto
**Sintoma:** copy excelente em slide ilegível chega ao público.
**Correção:** inspecionar as imagens renderizadas, sempre.
