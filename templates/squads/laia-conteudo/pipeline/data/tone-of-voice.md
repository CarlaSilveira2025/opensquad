# Tone of Voice — Produção de Conteúdo LAIA

O tom base vem sempre de `comunicacao.tom_de_voz` do `perfil.json` do cliente e da amostra
de voz real que ele forneceu no onboarding. Este documento define as **variações** possíveis
dentro desse tom e como escolher entre elas.

**Regra de precedência:** perfil do cliente > tom escolhido aqui > preferência do agente.
Nenhum tom pode violar `palavras_evitar`.

---

## Os 6 tons

### 1. Didático
Explica com clareza, sempre do concreto para o abstrato. Exemplo antes da definição.

- **Quando usar:** topo de funil, tema técnico, público iniciante
- **Marca registrada:** "na prática, isso significa…"
- **Risco:** soar professoral se o público já domina o assunto

> Automação não é robô. É você escrever uma vez o que hoje reescreve vinte.

---

### 2. Direto
Vai ao ponto, frases curtas, zero rodeio. Sem preâmbulo.

- **Quando usar:** público sem tempo, LinkedIn, meio de funil
- **Marca registrada:** afirmação seguida de evidência, sem transição
- **Risco:** parecer seco quando o tema exige acolhimento

> Você não precisa de mais uma ferramenta. Precisa saber o que repete toda semana.

---

### 3. Provocativo
Contraria o consenso e força reposicionamento. Usa tensão declarada.

- **Quando usar:** ângulos de provocação 4-5, tema saturado, construção de autoridade
- **Marca registrada:** nega uma crença antes de apresentar a alternativa
- **Risco:** soar como acusação a quem já fez a escolha criticada — o texto precisa acolher
  quem errou, não humilhar

> A ferramenta que você comprou não falhou. Você a instalou em cima de uma bagunça.

---

### 4. Narrativo
Conta um caso com começo, virada e consequência. Primeira pessoa quando possível.

- **Quando usar:** ângulos de lente "história", prova social, meio de funil, LinkedIn
- **Marca registrada:** abre em cena, não em tese
- **Risco:** perder o insight no meio da história — a conclusão precisa ser explícita

> Comprei a ferramenta, configurei tudo, e três meses depois estava fazendo orçamento
> no Word de novo.

---

### 5. Analítico
Ancora tudo em número e mostra o raciocínio. Trabalha com comparação e proporção.

- **Quando usar:** ângulos de lente "números", público cético, tema com dado forte
- **Marca registrada:** o número vem primeiro, a interpretação depois
- **Risco:** virar relatório — todo dado precisa de uma implicação prática ao lado

> 11 horas por semana. É o que uma empresa de serviço gasta em tarefa administrativa
> repetitiva. Em um ano, isso é um funcionário e meio.

---

### 6. Próximo
Fala como quem já passou pelo mesmo. Admite erro próprio, usa a linguagem do público.

- **Quando usar:** fundo de funil, tema sensível, público que desconfia de especialista
- **Marca registrada:** vulnerabilidade específica, nunca genérica
- **Risco:** virar autodepreciação e enfraquecer a autoridade

> Levei dois anos pra entender que eu estava automatizando o passo errado.

---

## Como escolher

| Situação | Tom recomendado |
|---|---|
| Ângulo de lente "números" | Analítico |
| Ângulo de lente "história" | Narrativo |
| Ângulo de lente "contraintuitivo" ou "erro comum" | Provocativo ou Direto |
| Ângulo de lente "passo a passo" | Didático |
| Topo de funil, público iniciante | Didático |
| Meio de funil, LinkedIn | Direto ou Narrativo |
| Fundo de funil, oferta | Próximo ou Direto |
| Público cético ou técnico | Analítico |
| Tema saturado no nicho | Provocativo |

---

## Combinações que funcionam

- **Analítico + Direto** — dado forte sem rodeio; o padrão para carrossel de topo com número
- **Narrativo + Próximo** — case pessoal; o padrão para LinkedIn de meio de funil
- **Provocativo + Didático** — contraria o consenso e depois ensina a alternativa; evita que
  a provocação fique sem saída

## Combinações que não funcionam

- **Provocativo + Próximo** — confronta e se desculpa na mesma peça; o leitor não sabe qual
  é a posição
- **Analítico + Narrativo** na mesma peça curta — dois ritmos disputando o mesmo espaço
- **Didático + Provocativo** invertidos (provocar depois de ensinar) — a provocação chega
  quando o leitor já concordou e soa gratuita

---

## Aplicação obrigatória do perfil

Antes de escrever qualquer peça, ler do `perfil.json`:

- `comunicacao.tom_de_voz` — a base, que este documento apenas modula
- `comunicacao.palavras_usar` — incorporar naturalmente, sem forçar
- `comunicacao.palavras_evitar` — **restrição rígida**, vale para toda peça
- A amostra de voz do cliente — referência literal de ritmo e vocabulário
- `publico.linguagem` — o registro que o público usa

Divergência entre o tom escolhido e o perfil resolve-se **sempre** a favor do perfil.
