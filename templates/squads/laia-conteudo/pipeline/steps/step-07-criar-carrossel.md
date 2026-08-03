---
step: "07"
name: "Criação do Carrossel"
type: agent
execution: subagent
model_tier: powerful
agent: criador-carrossel
format: instagram-feed
optional: true
tasks:
  - criar-carrossel
depends_on: step-06
inputFile: squads/laia-conteudo/output/ganchos-selecionados.yaml
outputFile: squads/laia-conteudo/output/carrossel.md
---

# Step 07: Carlos Carrossel — Criação do Carrossel (Fase 3.4 · Instagram)

## Condição de execução

Este step roda **apenas** se `ganchos-selecionados.yaml` contiver ao menos uma entrada com
`formato_destino: carrossel`. Se não houver, pular para o Step 08 sem executar e registrar
no log que o formato não foi solicitado para este item.

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/ganchos-selecionados.yaml` — gancho final, literal
- `squads/laia-conteudo/output/angulos-selecionados.yaml` — ângulo, resumo e risco
- `squads/laia-conteudo/output/pesquisa.md` — dados com número e fonte
- `squads/laia-conteudo/output/briefing-item.md` — etapa de funil e oferta, se de fundo
- `_opensquad/_memory/clientes/{slug}/perfil.json` — tom, palavras, dores, ofertas
- `squads/laia-conteudo/pipeline/data/tone-of-voice.md` — calibragem de registro

O Pipeline Runner injeta automaticamente o formato `instagram-feed` de
`_opensquad/core/best-practices/instagram-feed.md`.

## Instructions

### Process

0. **O formato injetado é a autoridade.** O Pipeline Runner injeta
   `_opensquad/core/best-practices/instagram-feed.md` neste step. Em qualquer divergência
   entre este arquivo e o formato injetado, **o formato injetado prevalece**.

1. **Escolher e declarar o formato do carrossel** entre os sete canônicos (Editorial/Tese,
   Listicle, Tutorial, Mito vs Realidade, Antes e Depois, Storytelling, Problema → Solução),
   conforme a lente do ângulo aprovado, e seguir o fluxo de slides correspondente.

2. **Colocar o gancho aprovado literal no slide 1**, em até 20 palavras. Ele passou por
   checkpoint — não reescrever, não "melhorar".

3. **Estruturar em 8 a 10 slides**, escrevendo cada um em **duas camadas**: headline
   (afirmação principal) + texto de apoio (dado, contexto ou elaboração). Cada slide fica
   entre **40 e 80 palavras** somadas. Contar antes de fechar. Abaixo de 40 o slide é
   superficial; acima de 80 a legibilidade desaba. Exceção só quando o perfil do cliente
   pedir slides curtos explicitamente — e nesse caso registrar a exceção.

4. **Garantir progressão.** Cada slide é consequência do anterior. Se dois slides puderem
   trocar de lugar sem prejuízo, falta progressão.

5. **Citar dados com fonte.** Todo número vem do relatório. Fonte internacional ou comercial
   precisa ser declarada no slide ou na legenda.

6. **Escrever a reflexão** antes do CTA: implicação, pergunta ou virada. É o que gera
   salvamento.

7. **CTA específico e conectado ao tema.** Quando o item for de fundo de funil, o CTA promove
   a oferta nomeada no briefing.

8. **Escrever a legenda como peça própria** — retoma o gancho, expande contexto, repete o
   CTA, traz 5 a 15 hashtags. Não é resumo dos slides.

9. **Indicar o elemento visual de cada slide** para orientar o Davi Design.

## Output Format

```markdown
# Carrossel — {assunto}

**Formato:** {um dos sete canônicos}
**Ângulo:** {título} · **Gancho:** {id} · **Slides:** {N}

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
**Palavras:** {contagem, entre 40 e 80}

## Legenda

{gancho — primeiros 125 caracteres funcionam sozinhos}

{corpo expandido}

{pergunta aberta de fechamento}

## Hashtags
{5 a 15}
```

## Output Example

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

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. O gancho aprovado foi reescrito, ou passa de 20 palavras no slide 1
2. Algum slide está fora da faixa de 40 a 80 palavras, sem exceção registrada do perfil
3. Algum slide não tem hierarquia de duas camadas, ou o apoio só repete a headline
4. O carrossel tem menos de 8 ou mais de 10 slides
5. O formato do carrossel não foi declarado
6. Algum dado citado não existe no relatório de pesquisa
7. Não há slide de síntese ou reflexão antes do CTA
8. O CTA é genérico ("curte e compartilha", "segue pra mais"), ou há link na legenda
9. Alguma palavra de `comunicacao.palavras_evitar` aparece

## Quality Criteria

- [ ] Formato do carrossel declarado e fluxo seguido
- [ ] Entre 8 e 10 slides, com contagem de palavras por slide
- [ ] Slide 1 com o gancho literal, até 20 palavras
- [ ] Cada slide entre 40 e 80 palavras, em duas camadas
- [ ] Fundos alternando e palavras-chave de destaque marcadas
- [ ] Uma ideia por slide, com progressão verificável
- [ ] Fonte declarada em dados internacionais ou comerciais
- [ ] Reflexão presente antes do CTA
- [ ] CTA conectado ao tema; oferta nomeada se o item for de fundo
- [ ] Legenda como peça própria, com 5 a 15 hashtags
- [ ] Indicação visual em todos os slides
