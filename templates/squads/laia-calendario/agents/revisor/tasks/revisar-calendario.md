---
task: "Revisar Calendário"
order: 1
input: |
  - calendario: output/calendario.yaml
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json
  - pesquisa: output/pesquisa-mensal.md
  - criterios: pipeline/data/quality-criteria.md
output: |
  - revisao: veredito e lista de correções (output/revisao-calendario.md)
---

# Revisar Calendário

Audita o calendário item a item contra critérios objetivos e emite APROVADO ou REPROVADO.
Não reescreve nada — aponta com precisão suficiente para a Estrategista corrigir em um ciclo.

## Process

1. **Contar os itens por etapa** e calcular a distribuição efetiva em percentual. Comparar
   com a meta 40/35/25 e a tolerância de ±5 pontos. Este é o cálculo mais importante e o mais
   frequentemente omitido.

2. **Verificar o volume total** contra a frequência declarada no perfil e contra a faixa de
   16 a 20 itens.

3. **Auditar a rastreabilidade de cada justificativa**, com o perfil e a pesquisa abertos.
   Classificar cada uma como rastreável, circular ou vazia. Justificativa circular é
   bloqueador.

4. **Verificar plataformas** — todas presentes em `objetivos.plataformas` do perfil.

5. **Verificar itens de fundo** — cada um nomeia uma oferta existente em
   `identidade.ofertas`.

6. **Verificar repetição temática** — nenhum assunto repetido; assuntos próximos com ângulo
   e formato distintos.

7. **Verificar variedade de formato e cadência** — sem mais de 2 itens de fundo por semana,
   sem dois itens de fundo em dias consecutivos. Isto é ressalva, não bloqueador.

8. **Emitir o veredito na primeira linha** e listar todos os apontamentos identificando cada
   item pelo número e pela data.

## Output Format

```markdown
# VEREDITO: APROVADO | REPROVADO

**Bloqueadores:** {N} · **Ressalvas:** {N} · **Ciclo:** {N} de 2

## Distribuição
| Etapa | Itens | % efetivo | % meta | Situação |

**Total de itens:** {N} (frequência do perfil: {valor})

## Bloqueadores
### Item {n} — {data} — {assunto}
**Problema:** {defeito}
**Correção esperada:** {ação}

## Ressalvas
- Item {n} ({data}): {observação}

## Verificações aprovadas
- {checagem que passou}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# VEREDITO: REPROVADO

**Bloqueadores:** 2 · **Ressalvas:** 3 · **Ciclo:** 1 de 2

## Distribuição
| Etapa | Itens | % efetivo | % meta | Situação |
|---|---|---|---|---|
| Topo | 10 | 56% | 40% (±5) | fora da faixa |
| Meio | 5 | 28% | 35% (±5) | dentro |
| Fundo | 3 | 17% | 25% (±5) | fora da faixa |

**Total de itens:** 18 (frequência do perfil: 4 por semana — coerente)

## Bloqueadores
### Distribuição de funil fora da faixa
**Problema:** topo em 56% (meta 40%, teto 45%) e fundo em 17% (meta 25%, piso 20%).
A meta principal do perfil é `leads`, o que pediria deslocamento **para** fundo, não o
contrário.
**Correção esperada:** converter 3 itens de topo em fundo, chegando a 7/5/6 (39/28/33).

### Item 11 — 2026-08-19 — "Dicas de produtividade com IA"
**Problema:** justificativa circular — "conteúdo educativo sobre produtividade porque o
público quer produtividade". Não aponta dor do perfil, achado datado nem objetivo. O
assunto também é rótulo genérico, não tema específico.
**Correção esperada:** substituir por tema ligado a uma dor de `publico.dores` ainda não
coberta no mês, ou reescrever a justificativa citando o achado que o sustenta.

## Ressalvas
- Itens 14 e 15 (2026-08-24 e 2026-08-25): dois itens de fundo em dias consecutivos —
  risco de fadiga de oferta
- Item 7 (2026-08-14): tema próximo ao do item 2, ambos sobre resposta a lead. Ângulos são
  diferentes e formatos também, então não é bloqueador, mas vale distanciar as datas
- Nenhum item usa o gancho sazonal de 15/08 identificado na pesquisa

## Verificações aprovadas
- Todas as plataformas usadas existem em `objetivos.plataformas`
- Todos os 3 itens de fundo nomeiam oferta existente em `identidade.ofertas`
- Nenhum assunto repetido literalmente
- Nenhum tema saturado da pesquisa foi usado sem ângulo diferenciador
```

## Quality Criteria

- [ ] Veredito na primeira linha
- [ ] Distribuição efetiva calculada em números e percentuais
- [ ] Todos os itens auditados, não uma amostra
- [ ] Cada apontamento identifica item por número e data
- [ ] Bloqueadores e ressalvas separados e contados
- [ ] Cada bloqueador traz correção acionável
- [ ] Nenhuma correção aplicada pela auditora

## Veto Conditions

Rejeitar e refazer se:
1. A distribuição efetiva não foi calculada em números
2. O veredito é APROVADO havendo bloqueador listado
3. O veredito é REPROVADO tendo apenas ressalvas
4. Algum item do calendário não foi verificado
