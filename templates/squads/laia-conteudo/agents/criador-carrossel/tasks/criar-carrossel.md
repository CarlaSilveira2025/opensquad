---
task: "Criar Carrossel"
order: 1
input: |
  - ganchos_selecionados: output/ganchos-selecionados.yaml
  - angulos_selecionados: output/angulos-selecionados.yaml
  - pesquisa: output/pesquisa.md
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json
  - tom: pipeline/data/tone-of-voice.md
output: |
  - carrossel: carrossel completo slide a slide com legenda (output/carrossel.md)
---

# Criar Carrossel

Escreve o carrossel completo de Instagram: o texto exato de cada slide em duas camadas,
a legenda com hashtags e a indicação de elemento visual. O texto vai literalmente dentro
da imagem.

O Pipeline Runner injeta o arquivo `instagram-feed` de `_opensquad/core/best-practices/`
neste step. **Ele é a autoridade sobre o formato** — esta task o operacionaliza, nunca o
contradiz.

## Process

1. **Escolher o formato do carrossel** entre os sete canônicos, conforme a lente do ângulo
   aprovado:

   | Lente do ângulo | Formato indicado |
   |---|---|
   | contraintuitivo, erro-comum | Mito vs Realidade ou Problema → Solução |
   | numeros, revelador | Editorial / Tese |
   | historia | Storytelling ou Antes e Depois |
   | passo-a-passo | Tutorial |
   | pergunta-incomoda | Problema → Solução |

   Declarar o formato escolhido no topo do arquivo e seguir o fluxo de slides dele.

2. **Montar 8 a 10 slides** conforme o fluxo do formato escolhido. O gancho aprovado vai
   literal no slide 1, em até 20 palavras — não reescrever o que passou pelo checkpoint.

3. **Escrever cada slide em duas camadas:**
   - **Headline** — a afirmação principal, corpo grande
   - **Texto de apoio** — dado, contexto ou elaboração, corpo menor
   O apoio precisa acrescentar informação. Se ele só reformula a headline, o slide está raso.

4. **Respeitar a faixa de 40 a 80 palavras por slide** (headline + apoio somados). Contar
   antes de fechar cada slide. Abaixo de 40, o slide é superficial; acima de 80, ilegível.
   Exceção única: o perfil do cliente pedir slides curtos explicitamente — nesse caso,
   registrar a exceção no topo do arquivo.

5. **Marcar as palavras-chave de destaque** de cada headline, que o designer vai colorir com
   a cor de acento do perfil.

6. **Alternar os fundos** entre claro, escuro e acento ao longo dos slides, criando ritmo
   visual e evitando fadiga.

7. **Citar dados com fonte.** Todo número vem do relatório de pesquisa. Fonte internacional
   ou comercial precisa ser declarada no slide de apoio ou na legenda.

8. **Fechar com síntese e CTA** conforme o formato: o penúltimo slide entrega a conclusão ou
   a reflexão, e o último traz o CTA específico mais a assinatura com logo.

9. **Escrever a legenda como peça própria:** os primeiros 125 caracteres funcionam sozinhos
   como gancho (é o que aparece antes do "mais"); depois o corpo expande o argumento; fecha
   com pergunta aberta. De 5 a 15 hashtags, misturando nicho, médio alcance e amplas.
   Nunca incluir link — o Instagram não torna links clicáveis na legenda.

## Output Format

```markdown
# Carrossel — {assunto}

**Formato:** {Editorial | Listicle | Tutorial | Mito vs Realidade | Antes e Depois | Storytelling | Problema → Solução}
**Ângulo:** {título} · **Gancho:** {id} · **Slides:** {N}
**Exceção de tamanho:** {apenas se o perfil pedir slides curtos}

## Slide 1 — Capa
**Título:** {gancho aprovado, literal, até 20 palavras}
**Foto/fundo:** {direção visual}
**Destaques:** {palavras a colorir}
**Palavras:** {contagem}

## Slide N — {papel no fluxo do formato}
**Headline:** {afirmação principal}
**Apoio:** {dado, contexto ou elaboração}
**Foto:** {direção visual, se aplicável}
**Destaques:** {palavras a colorir}
**Fundo:** {claro | escuro | acento}
**Palavras:** {contagem}

## Legenda

{gancho — primeiros 125 caracteres funcionam sozinhos}

{corpo — argumento expandido, com quebras de linha}

{pergunta aberta de fechamento}

## Hashtags
{5 a 15}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Carrossel — O orçamento que você reescreve 20 vezes por semana

**Formato:** Problema → Solução
**Ângulo:** Você não tem problema de ferramenta · **Gancho:** 3b · **Slides:** 8

## Slide 1 — Capa
**Título:** Você não tem problema de ferramenta. Tem problema de processo.
**Foto/fundo:** fundo grafite sólido, sem imagem — só tipografia
**Destaques:** "processo"
**Palavras:** 11

## Slide 2 — Problema
**Headline:** 4 em 10 empresas abandonam a automação nos primeiros 3 meses.
**Apoio:** A assinatura continua sendo debitada, o login continua ativo, e ninguém abre.
O dinheiro não some de uma vez — some em parcelas que ninguém revisa. E quando alguém
revisa, a conclusão errada já virou consenso interno: "automação não funciona pra gente".
**Foto:** captura de painel de assinaturas com uso zerado
**Destaques:** "4 em 10", "conclusão errada"
**Fundo:** escuro
**Palavras:** 63

## Slide 3 — Problema
**Headline:** O motivo quase nunca é técnico.
**Apoio:** A ferramenta foi instalada em cima de um processo que ninguém tinha desenhado.
Ela passou a executar rápido exatamente aquilo que já estava confuso — e confusão acelerada
não vira eficiência, vira retrabalho com aparência de modernidade.
**Foto:** engrenagem sobre linha tracejada quebrada
**Destaques:** "nunca é técnico", "retrabalho"
**Fundo:** claro
**Palavras:** 52

## Slide 5 — Ponte
**Headline:** Existe um jeito mais simples, e ele não começa comprando nada.
**Apoio:** Começa separando o que se repete do que exige julgamento. Em orçamento, isso
costuma dividir em 80% de estrutura — escopo, prazos, condições, termos — e 20% de decisão
real, que é onde está o seu valor. Só o primeiro bloco deve ser automatizado.
**Destaques:** "não começa comprando nada", "80%"
**Fundo:** acento
**Palavras:** 61

## Slide 7 — Síntese
**Headline:** Automatizar um processo bagunçado não organiza a bagunça.
**Apoio:** Só faz ela acontecer mais rápido. Por isso o teste antes de qualquer compra é
escrever, num papel, os 3 passos que você repete toda semana. Se não couber em 3 passos,
o problema ainda não é de ferramenta — é de desenho.
**Destaques:** "mais rápido", "3 passos"
**Fundo:** escuro
**Palavras:** 58

## Slide 8 — CTA
**Headline:** Salva pra quando alguém te disser que o problema é falta de IA.
**Apoio:** E se você já tentou automatizar e voltou pro manual, comenta em qual parte
travou — é quase sempre o mesmo ponto, e vale demais comparar.
**Foto:** assinatura com logo
**Destaques:** "falta de IA"
**Fundo:** acento
**Palavras:** 45

## Legenda

Você não tem problema de ferramenta. Tem problema de processo — e a diferença custa caro.

4 em 10 empresas abandonam a automação nos primeiros três meses, e quase nunca por
limitação técnica. A ferramenta chega antes do desenho do processo, e aí ela automatiza a
bagunça que já existia.

(Dado de relatório setorial de 2026, base internacional.)

O teste que eu faço com todo cliente antes de sugerir qualquer ferramenta: escrever os 3
passos que se repetem toda semana. Se não couber em 3 passos, não é hora de automatizar —
é hora de desenhar.

Quem já tentou automatizar e voltou pro manual: em qual parte travou?

## Hashtags
#automacao #pequenosnegocios #processos #produtividade #gestao #empreendedorismo #pme
```

## Quality Criteria

- [ ] Formato do carrossel declarado e fluxo correspondente seguido
- [ ] Entre 8 e 10 slides
- [ ] Slide 1 com o gancho aprovado, literal, em até 20 palavras
- [ ] Cada slide entre 40 e 80 palavras (headline + apoio), com contagem declarada
- [ ] Todo slide com hierarquia de duas camadas; o apoio acrescenta, não repete
- [ ] Fundos alternando entre claro, escuro e acento
- [ ] Palavras-chave de destaque marcadas em cada slide
- [ ] Todo dado citado existe na pesquisa; fonte internacional ou comercial declarada
- [ ] Legenda com os primeiros 125 caracteres funcionando sozinhos
- [ ] Legenda fecha com pergunta aberta e traz de 5 a 15 hashtags
- [ ] Nenhum link na legenda
- [ ] CTA específico, nunca "me segue para mais"

## Veto Conditions

Rejeitar e refazer se:
1. O gancho aprovado foi reescrito
2. Algum slide está fora da faixa de 40 a 80 palavras, sem exceção registrada do perfil
3. Algum slide não tem hierarquia de duas camadas, ou o apoio só repete a headline
4. O formato do carrossel não foi declarado
5. Algum dado citado não existe no relatório de pesquisa
6. O CTA é genérico, ou existe link na legenda
