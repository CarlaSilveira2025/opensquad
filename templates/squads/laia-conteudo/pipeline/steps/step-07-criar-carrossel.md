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
- `squads/laia-conteudo/pipeline/data/quality-criteria.md` — limites do formato

O Pipeline Runner injeta automaticamente o formato `instagram-feed` de
`_opensquad/core/best-practices/instagram-feed.md`.

## Instructions

### Process

1. **Colocar o gancho aprovado literal no slide 1.** Ele passou por checkpoint — não
   reescrever, não "melhorar".

2. **Estruturar em 6 a 10 slides:** capa (gancho), desenvolvimento com uma ideia por slide,
   reflexão no penúltimo, CTA + assinatura no último.

3. **Escrever cada slide com no máximo ~30 palavras e 5 linhas visíveis.** Contar antes de
   fechar cada slide — é o limite físico do formato, não preferência.

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

**Ângulo:** {título} · **Gancho:** {id} · **Slides:** {N}

## Slide 1 — Capa
> {texto exato}

**Visual:** {elemento}
**Palavras:** {contagem}

## Slide N — {função}
> {texto exato}

**Visual:** {elemento}
**Palavras:** {contagem}

## Legenda

{texto completo}

{hashtags}
```

## Output Example

```markdown
# Carrossel — O orçamento que você reescreve 20 vezes por semana

**Ângulo:** Você não tem problema de ferramenta · **Gancho:** 3b · **Slides:** 8

## Slide 1 — Capa
> Você não tem problema de ferramenta.
> Tem problema de processo.

**Visual:** tipografia grande, segunda linha em verde sinal sobre grafite, sem imagem
**Palavras:** 11

## Slide 2 — O dado
> 4 em 10 empresas abandonam a automação nos primeiros 3 meses.
>
> A ferramenta continua paga. Só ninguém usa.

**Visual:** "4 em 10" como número dominante, texto de apoio embaixo
**Palavras:** 21

## Slide 6 — Reflexão
> Automatizar um processo bagunçado não organiza a bagunça.
>
> Só faz ela acontecer mais rápido.

**Visual:** frase centralizada, muito espaço vazio
**Palavras:** 17

## Slide 7 — CTA
> Antes da próxima ferramenta: escreve os 3 passos que você repete toda semana.
>
> Salva pra quando disserem que o problema é falta de IA.

**Visual:** fundo em verde sinal, texto em grafite, ícone de salvar
**Palavras:** 28

## Legenda

Você não tem problema de ferramenta. Tem problema de processo.

4 em 10 empresas abandonam a automação nos primeiros três meses — e quase nunca por
limitação técnica. A ferramenta chega antes do desenho do processo, e aí ela automatiza a
bagunça que já existia.

(Dado de relatório setorial de 2026, base internacional.)

O teste que eu faço antes de sugerir qualquer ferramenta: escrever os 3 passos que se
repetem toda semana. Se não couber em 3 passos, não é hora de automatizar — é hora de
desenhar.

Salva pra quando alguém te disser que o problema é falta de IA.

#automacao #pequenosnegocios #processos #produtividade #gestao #empreendedorismo
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. O gancho aprovado foi reescrito
2. Algum slide passa de 30 palavras
3. O carrossel tem menos de 6 ou mais de 10 slides
4. Algum dado citado não existe no relatório de pesquisa
5. Não há slide de reflexão antes do CTA
6. O CTA é genérico ("curte e compartilha", "segue pra mais")
7. Alguma palavra de `comunicacao.palavras_evitar` aparece

## Quality Criteria

- [ ] Entre 6 e 10 slides, com contagem de palavras por slide
- [ ] Slide 1 com o gancho literal
- [ ] Uma ideia por slide, com progressão verificável
- [ ] Fonte declarada em dados internacionais ou comerciais
- [ ] Reflexão presente antes do CTA
- [ ] CTA conectado ao tema; oferta nomeada se o item for de fundo
- [ ] Legenda como peça própria, com 5 a 15 hashtags
- [ ] Indicação visual em todos os slides
