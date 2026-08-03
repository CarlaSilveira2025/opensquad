# Domain Framework — Produção de Conteúdo LAIA

Framework operacional das Fases 3.1 a 3.5.

---

## 1. A linha de montagem

| Fase | Step | Agente | Entrega |
|---|---|---|---|
| 3.1 Pesquisa | 02 | Pedro Pesquisa | dados com fonte, saturação, recortes ausentes |
| 3.2 Ângulos | 03 | Ângela Ângulo | 5+ lentes sobre o mesmo assunto |
| 3.3 Ganchos | 05 | Gabriel Gancho | 3 ganchos por ângulo, de tipos diferentes |
| 3.4 Conteúdo | 07 / 08 | Carlos Carrossel / Luna LinkedIn | texto completo por formato |
| 3.5 Visual | 10 | Davi Design | imagens renderizadas na identidade da marca |

Cada fase tem um checkpoint depois dela quando há decisão criativa a tomar.

---

## 2. Definição de ângulo (Fase 3.2)

**Ângulo é a lente emocional pela qual UM assunto é contado.** Cinco ângulos = cinco formas
de contar a mesma coisa. Cinco assuntos diferentes = cinco pautas, não ângulos.

### Lentes canônicas

| Lente | Mecanismo | Quando funciona |
|---|---|---|
| **Revelador** | mostra o que está acontecendo e ninguém percebeu | há dado surpreendente |
| **Erro comum** | o que a maioria faz errado | há prática difundida e equivocada |
| **Contraintuitivo** | o oposto do senso comum do nicho | há consenso a contrariar com lastro |
| **História** | caso concreto com virada e consequência | há caso real disponível |
| **Números** | a dimensão que só aparece quando se mede | há dado quantitativo forte |
| **Passo a passo** | o método | o valor está na execução |
| **Pergunta incômoda** | a dúvida que o público evita fazer | há objeção não endereçada |

### Teste de distinção (obrigatório)
Escrever mentalmente o slide 1 de cada ângulo. **Se dois aceitam a mesma abertura sem
estranheza, são o mesmo ângulo.**

### Escala de provocação

| Nível | Descrição | Risco |
|---|---|---|
| 1-2 | educativo, sem confronto | baixo |
| 3 | reenquadra sem acusar | médio |
| 4 | contraria consenso do nicho | risco declarado obrigatório |
| 5 | confronta diretamente | risco declarado + confirmação no checkpoint |

---

## 3. Tipos canônicos de gancho (Fase 3.3)

| Tipo | Mecanismo | Exemplo de estrutura |
|---|---|---|
| **Pergunta provocativa** | abre um loop que exige fechamento | "Quantas horas por semana você…?" |
| **Afirmação chocante** | quebra expectativa | "Pare de fazer isso hoje." |
| **História** | ativa identificação imediata | "Perdi meu maior cliente por…" |
| **Dado/estatística** | ancora em número específico | "4 em 10 empresas abandonam…" |
| **Contraintuitivo** | contraria o senso comum | "Você não tem problema de ferramenta." |

**Regra:** 3 ganchos por ângulo, os 3 de tipos diferentes. Máximo de 2 linhas visíveis. No
LinkedIn, ~210 caracteres — o corte do "ver mais".

---

## 4. Estrutura por formato (Fase 3.4)

### Carrossel Instagram — 8 a 10 slides

> **Autoridade:** `_opensquad/core/best-practices/instagram-feed.md`, injetado
> automaticamente pelo Runner no step de criação. Em qualquer divergência, ele prevalece.

| Slide | Função | Limite |
|---|---|---|
| 1 | Capa com o gancho aprovado, literal | até 20 palavras |
| 2 a N-2 | Desenvolvimento, uma ideia por slide, em progressão | 40-80 palavras cada |
| N-1 | Síntese ou reflexão — implicação, pergunta ou virada | 40-80 palavras |
| N | CTA específico + assinatura com logo | 40-80 palavras |

**Hierarquia de duas camadas obrigatória** em todo slide de conteúdo:
*headline* (afirmação principal, corpo grande) + *texto de apoio* (dado, contexto ou
elaboração, corpo menor). O apoio acrescenta informação; se só reformula a headline, o
slide está raso.

**Faixa de 40 a 80 palavras** por slide, somando headline e apoio. Abaixo de 40 o slide é
superficial; acima de 80 a legibilidade desaba. Exceção única: o perfil do cliente pedir
slides curtos explicitamente — e a exceção precisa ser registrada no arquivo do carrossel.

#### Os sete formatos canônicos de carrossel

| Formato | Quando usar | Lente do ângulo que combina |
|---|---|---|
| **Editorial / Tese** | argumentar uma tese com evidência | numeros, revelador |
| **Listicle** | valor escaneável e numerado | passo-a-passo |
| **Tutorial** | ensinar um processo | passo-a-passo |
| **Mito vs Realidade** | derrubar crenças equivocadas | contraintuitivo, erro-comum |
| **Antes e Depois** | mostrar transformação | historia |
| **Storytelling** | conexão emocional | historia |
| **Problema → Solução** | endereçar dor e apresentar saída | pergunta-incomoda, contraintuitivo |

O formato é escolhido e **declarado** no topo do arquivo, e o fluxo de slides dele é seguido.

Outras regras do formato: fundos alternando entre claro, escuro e acento para criar ritmo;
palavras-chave marcadas para destaque em cor de acento; legenda com os primeiros 125
caracteres funcionando sozinhos; 5-15 hashtags; **nunca link na legenda**.

Legenda como peça própria: retoma o gancho, expande o contexto, repete o CTA, 5-15 hashtags.

### Post LinkedIn

```
Gancho (1ª linha, ~210 caracteres — antes do "ver mais")
↓
Contexto — cena concreta, não tese
↓
Desenvolvimento — blocos de 1 a 3 linhas
↓
Insight explícito — a frase que o leitor leva para a reunião
↓
CTA específico
↓
3 a 5 hashtags
```

---

## 5. Especificação visual (Fase 3.5)

### Dimensões

| Peça | Viewport |
|---|---|
| Carrossel Instagram | 1080×1440 |
| Post/Feed quadrado | 1080×1080 |
| LinkedIn imagem única | 1200×627 |

### Limites duros

- Fonte mínima: **34px** em peça de 1080px de largura
- Margem externa mínima: **80px** em peça de 1080px
- Cores: **exclusivamente** de `visual.paleta` (neutros puros permitidos)
- HTML **autocontido** — nenhuma referência de rede
- **O texto aprovado é intocável.** Não coube? Ajusta o design.

### Escala tipográfica de referência (1080px)

| Uso | Faixa |
|---|---|
| Título de capa | 88-110px |
| Título de slide | 64-80px |
| Corpo | 40-52px |
| Rodapé | 32-36px |

---

## 6. Ponto de extensão: Reels (roadmap item 10)

Reels é da próxima fase e **não** está implementado. A arquitetura já o acomoda:

1. Adicionar `criador-reels` (ex.: "Rita Reels") com `format: instagram-reels` — o arquivo
   de best-practice já existe em `_opensquad/core/best-practices/instagram-reels.md`
2. Criar a task `criar-roteiro-reels.md`: roteiro com marcação de tempo, gancho de 3
   segundos, desenvolvimento com transições, CTA, sugestão de áudio e descrição de cena
3. Adicionar o step 08b com `optional: true`, condicionado a
   `formato_destino: reels` em `ganchos-selecionados.yaml`
4. Estender `definir-sistema-visual` com o tratamento de thumbnail 1080×1920 e cards de
   texto sobrepostos
5. Incluir `reels` em `formats_supported` no `squad.yaml`

Nada além disso precisa mudar: os ângulos e ganchos já saem classificados por formato, e o
checkpoint 04 já suporta distribuir ângulos diferentes para formatos diferentes.
