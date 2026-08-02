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

Escreve o carrossel completo de Instagram: texto exato de cada slide, legenda com hashtags e
indicação de elemento visual por slide. O texto vai literalmente dentro da imagem.

## Process

1. **Ler o gancho aprovado e o ângulo correspondente.** O gancho vai literal no slide 1 —
   não reescrever o que passou pelo checkpoint.

2. **Definir a estrutura em 6 a 10 slides:**
   - Slide 1 — capa com o gancho aprovado
   - Slides 2 a N-2 — desenvolvimento, uma ideia por slide, em progressão
   - Slide N-1 — reflexão (implicação, pergunta ou virada)
   - Slide N — CTA específico + assinatura com logo

3. **Escrever cada slide com no máximo 4 a 5 linhas visíveis** (~30 palavras). Frases
   curtas. Contar as palavras antes de fechar cada slide.

4. **Garantir progressão.** Cada slide é consequência do anterior. Teste: se dois slides
   puderem trocar de lugar sem prejuízo, falta progressão.

5. **Citar dados com fonte.** Todo número vem do relatório de pesquisa. Quando o dado for
   internacional ou de fonte comercial, declarar no slide ou na legenda.

6. **Escrever a legenda como peça própria:** retoma o gancho, expande o contexto que não
   coube nos slides, repete o CTA e traz de 5 a 15 hashtags relevantes. Não é resumo dos
   slides.

7. **Indicar o elemento visual de cada slide** — número grande, lista, citação, comparação,
   imagem de apoio — para orientar o Davi Design.

8. **Aplicar a voz do cliente**: `tom_de_voz`, `palavras_usar`, `palavras_evitar` e a amostra
   de voz do perfil como referência de calibragem.

## Output Format

```markdown
# Carrossel — {assunto}

**Ângulo:** {título} · **Gancho:** {id} · **Slides:** {N}

## Slide 1 — Capa
> {texto exato}

**Visual:** {elemento visual}
**Palavras:** {contagem}

## Slide 2 — {função}
> {texto exato}

**Visual:** {elemento visual}
**Palavras:** {contagem}

## Legenda

{texto completo da legenda}

{hashtags}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Carrossel — O orçamento que você reescreve 20 vezes por semana

**Ângulo:** Você não tem problema de ferramenta · **Gancho:** 3b · **Slides:** 8

## Slide 1 — Capa
> Você não tem problema de ferramenta.
> Tem problema de processo.

**Visual:** tipografia grande, segunda linha em verde sinal sobre fundo grafite, sem imagem
**Palavras:** 11

## Slide 2 — O dado
> 4 em 10 empresas abandonam a automação nos primeiros 3 meses.
>
> A ferramenta continua paga. Só ninguém usa.

**Visual:** "4 em 10" como número dominante, texto de apoio embaixo
**Palavras:** 21

## Slide 3 — A causa
> O motivo quase nunca é técnico.
>
> É que a ferramenta foi instalada em cima de um processo que ninguém tinha desenhado.

**Visual:** ícone de engrenagem sobre linha tracejada quebrada
**Palavras:** 26

## Slide 6 — Reflexão
> Automatizar um processo bagunçado não organiza a bagunça.
>
> Só faz ela acontecer mais rápido.

**Visual:** frase centralizada, muito espaço vazio, sem elemento gráfico
**Palavras:** 17

## Slide 7 — CTA
> Antes de comprar a próxima ferramenta: escreve num papel os 3 passos que você repete
> toda semana.
>
> Salva esse carrossel pra quando alguém te disser que o problema é falta de IA.

**Visual:** fundo em verde sinal, texto em grafite, ícone de salvar
**Palavras:** 34

## Legenda

Você não tem problema de ferramenta. Tem problema de processo.

4 em 10 empresas abandonam a automação nos primeiros três meses — e quase nunca por
limitação técnica. O que acontece é mais simples: a ferramenta chega antes do desenho do
processo, e aí ela automatiza a bagunça que já existia.

(Dado de relatório setorial de 2026, base internacional.)

O teste que eu faço com todo cliente antes de sugerir qualquer ferramenta: escrever os 3
passos que se repetem toda semana. Se não couber em 3 passos, não é hora de automatizar —
é hora de desenhar.

Salva pra quando alguém te disser que o problema é falta de IA.

#automacao #pequenosnegocios #processos #produtividade #gestao #inteligenciaartificial
#empreendedorismo #negocios
```

## Quality Criteria

- [ ] Entre 6 e 10 slides
- [ ] Slide 1 traz o gancho aprovado, literal
- [ ] Nenhum slide passa de ~30 palavras ou 5 linhas
- [ ] Uma ideia por slide, com progressão verificável
- [ ] Todo dado citado existe na pesquisa; fonte comercial ou internacional declarada
- [ ] Slide de reflexão antes do CTA
- [ ] CTA específico e conectado ao tema
- [ ] Legenda é peça própria, com 5 a 15 hashtags
- [ ] Indicação visual em todos os slides
- [ ] Nenhuma palavra de `palavras_evitar`

## Veto Conditions

Rejeitar e refazer se:
1. O gancho aprovado foi reescrito
2. Algum slide passa de 30 palavras
3. Algum dado citado não existe no relatório de pesquisa
4. Não há slide de reflexão antes do CTA
5. O CTA é genérico ("curte e compartilha", "segue pra mais")
6. Alguma palavra proibida do perfil aparece
