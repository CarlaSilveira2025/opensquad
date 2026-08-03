---
step: "08"
name: "Criação do Post LinkedIn"
type: agent
execution: subagent
model_tier: powerful
agent: criador-linkedin
format: linkedin-post
optional: true
tasks:
  - criar-post-linkedin
depends_on: step-06
inputFile: squads/laia-conteudo/output/ganchos-selecionados.yaml
outputFile: squads/laia-conteudo/output/linkedin.md
---

# Step 08: Luna LinkedIn — Criação do Post (Fase 3.4 · LinkedIn)

## Condição de execução

Este step roda **apenas** se `ganchos-selecionados.yaml` contiver ao menos uma entrada com
`formato_destino: post-linkedin`. Se não houver, pular para o Step 09 sem executar e
registrar no log que o formato não foi solicitado para este item.

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/ganchos-selecionados.yaml` — gancho final para LinkedIn
- `squads/laia-conteudo/output/angulos-selecionados.yaml` — ângulo, resumo e risco
- `squads/laia-conteudo/output/pesquisa.md` — dados com número e fonte
- `squads/laia-conteudo/output/briefing-item.md` — etapa de funil e oferta, se de fundo
- `squads/laia-conteudo/output/carrossel.md` — se existir, para garantir texto distinto
- `_opensquad/_memory/clientes/{slug}/perfil.json` — tom, palavras, público
- `squads/laia-conteudo/pipeline/data/tone-of-voice.md` — calibragem de registro

O Pipeline Runner injeta automaticamente o formato `linkedin-post` de
`_opensquad/core/best-practices/linkedin-post.md`.

## Instructions

### Process

1. **Colocar o gancho aprovado literal na primeira linha** e conferir que as três primeiras
   linhas cabem em ~210 caracteres — é o que aparece antes do "ver mais".

2. **Abrir com cena concreta**, não com tese. A conclusão vem depois que o leitor se
   reconheceu na situação.

3. **Desenvolver em blocos de 1 a 3 linhas**, separados por quebra dupla.

4. **Usar especificidade**: número, nome de ferramenta, prazo, valor. Todo dado vem do
   relatório de pesquisa.

5. **Escrever o insight explícito** antes do CTA — a frase que o leitor levaria para uma
   reunião. Sem ela, o post não é compartilhado.

6. **Fechar com CTA específico.** Em item de fundo de funil, o CTA se liga à oferta nomeada
   no briefing.

7. **Adicionar 3 a 5 hashtags** e sugerir a peça visual com tipo, conteúdo e dimensão.

8. **Se o carrossel já existir, escrever texto distinto.** Mesmo ângulo, execução diferente
   — texto de slide colado vira post picotado.

## Output Format

```markdown
# Post LinkedIn — {assunto}

**Ângulo:** {título} · **Gancho:** {id}
**Primeiras 3 linhas:** {caracteres} (limite ~210)

## Texto

{texto completo com as quebras reais}

## Hashtags
{3 a 5}

## Peça visual sugerida
**Tipo:** imagem única | carrossel PDF
**Conteúdo:** {descrição}
**Dimensão:** 1200×627 | 1080×1080
```

## Output Example

```markdown
# Post LinkedIn — O orçamento que você reescreve 20 vezes por semana

**Ângulo:** Os 20% que ninguém resolve · **Gancho:** 3c
**Primeiras 3 linhas:** 104 caracteres (limite ~210)

## Texto

Comprei a ferramenta, configurei tudo, e três meses depois estava fazendo orçamento no Word
de novo.

Não foi preguiça. Foi que a automação dava conta de 80% dos casos, e os outros 20% eram
justamente os orçamentos grandes — os que pagavam a conta.

Aí acontece o previsível: você mantém dois processos em paralelo. O automático para o
simples, o manual para o que importa. E manter dois é mais caro que manter um.

Foi só quando parei de tentar automatizar os 20% que a coisa funcionou.

O que fiz: separei o orçamento em duas partes. A estrutura — escopo, prazos, condições,
termos — virou template automático. O que exige julgamento continuou manual, mas passou a
chegar num documento já 70% pronto.

Tempo de resposta: de 2 dias para o mesmo dia.
Tempo de escrita por orçamento grande: de 50 minutos para 15.

O insight que eu levaria pra qualquer processo: automação não é sobre eliminar o julgamento
humano. É sobre tirar dele tudo que não exige julgamento.

Quem tentou automatizar orçamento e voltou pro manual: em qual parte travou?

## Hashtags
#automacao #processos #pequenosnegocios #gestao

## Peça visual sugerida
**Tipo:** imagem única
**Conteúdo:** comparação em duas colunas — "Estrutura (automática)" com 4 itens à esquerda,
"Julgamento (manual)" com 2 itens à direita, na paleta da marca
**Dimensão:** 1200×627
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. O gancho aprovado foi reescrito, ou não cabe antes do "ver mais"
2. O post abre com tese abstrata em vez de cena concreta
3. Algum bloco tem mais de 3 linhas
4. Algum dado citado não existe no relatório de pesquisa
5. Não há insight explícito antes do CTA
6. Menos de 3 ou mais de 5 hashtags
7. O texto é o carrossel reformatado

## Quality Criteria

- [ ] Gancho literal na primeira linha, com contagem de caracteres declarada
- [ ] Estrutura completa: gancho → contexto → desenvolvimento → insight → CTA
- [ ] Blocos de no máximo 3 linhas
- [ ] Números e nomes específicos presentes
- [ ] Peça visual sugerida com tipo, conteúdo e dimensão
- [ ] Texto distinto do carrossel, quando os dois existem
- [ ] Nenhuma palavra proibida nem corporativês
