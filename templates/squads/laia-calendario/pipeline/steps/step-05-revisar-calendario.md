---
step: "05"
name: "Revisão do Calendário"
type: agent
execution: inline
agent: revisor
tasks:
  - revisar-calendario
depends_on: step-04
on_reject: step-04
inputFile: squads/laia-calendario/output/calendario.yaml
outputFile: squads/laia-calendario/output/revisao-calendario.md
---

# Step 05: Vera Veredito — Revisão do Calendário

## Context Loading

Carregar antes de executar:

- `squads/laia-calendario/output/calendario.yaml` — calendário a auditar
- `squads/laia-calendario/output/calendario.md` — versão em tabela, para conferir consistência
- `_opensquad/_memory/clientes/{slug}/perfil.json` — dores, ofertas, plataformas, frequência
- `squads/laia-calendario/output/pesquisa-mensal.md` — para verificar rastreabilidade das
  justificativas e uso de temas saturados
- `squads/laia-calendario/output/ajustes-pesquisa.md` — lista de descarte do usuário
- `squads/laia-calendario/pipeline/data/quality-criteria.md` — critérios canônicos

## Instructions

### Process

1. **Contar os itens por etapa e calcular a distribuição efetiva** em números absolutos e
   percentuais. Comparar com a meta 40/35/25 e a tolerância de ±5 pontos. Verificar se
   qualquer desvio tem justificativa registrada e ligada à meta principal do perfil.

2. **Conferir o volume total** contra a frequência do perfil e a faixa de 16 a 20 itens.

3. **Auditar item a item a rastreabilidade da justificativa**, com o perfil e a pesquisa
   abertos. Classificar cada uma como rastreável, circular ou vazia.

4. **Verificar as restrições rígidas**: plataformas dentro de `objetivos.plataformas`,
   ofertas dos itens de fundo existentes em `identidade.ofertas`, nenhum tema da lista de
   descarte do usuário, nenhum assunto repetido.

5. **Verificar cadência e variedade** — máximo 2 itens de fundo por semana, sem fundo em
   dias consecutivos, variedade de formato dentro de cada etapa. Estes são ressalvas.

6. **Emitir o veredito na primeira linha** e listar todos os apontamentos, cada um
   identificando o item pelo número e pela data. Gravar em
   `squads/laia-calendario/output/revisao-calendario.md`. Não corrigir nada.

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

```markdown
# VEREDITO: APROVADO

**Bloqueadores:** 0 · **Ressalvas:** 3 · **Ciclo:** 2 de 2

## Distribuição
| Etapa | Itens | % efetivo | % meta | Situação |
|---|---|---|---|---|
| Topo | 6 | 33% | 40% (±5) | dentro (ajuste declarado) |
| Meio | 6 | 33% | 35% (±5) | dentro |
| Fundo | 6 | 34% | 25% (±5) | dentro (ajuste declarado) |

**Total de itens:** 18 (frequência do perfil: 4 por semana — coerente com 4,5 semanas)

O desvio de topo para fundo está registrado e ligado à meta principal `leads`, dentro da
tolerância de ±5 pontos aplicada sobre a etapa de origem.

## Bloqueadores
Nenhum.

## Ressalvas
- Itens 14 e 15 (24/08 e 25/08): dois itens de fundo em dias consecutivos — risco de
  fadiga de oferta. Sugestão: mover o 15 para 27/08.
- Item 7 (14/08): tema próximo ao do item 2, ambos sobre resposta a lead. Ângulos e
  formatos diferentes, então não bloqueia, mas vale distanciar as datas.
- Formato: 13 dos 18 itens são carrossel. Dentro do aceitável porque carrossel teve o
  melhor desempenho em julho, mas vale monitorar fadiga de formato no próximo mês.

## Verificações aprovadas
- Todos os 18 itens têm justificativa rastreável a dor, achado datado ou objetivo
- Todos os 6 itens de fundo nomeiam oferta existente em `identidade.ofertas`
- Nenhuma plataforma fora de `objetivos.plataformas`
- Nenhum assunto repetido
- Nenhum tema da lista de descarte do usuário foi incluído
- Tema saturado "IA vai substituir empregos" não foi usado
- Gancho sazonal de 15/08 aproveitado no item 6
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. A distribuição efetiva não foi calculada em números absolutos e percentuais
2. O veredito é APROVADO havendo pelo menos um bloqueador listado
3. O veredito é REPROVADO tendo apenas ressalvas
4. Algum item do calendário não foi verificado
5. A auditora alterou o calendário em vez de apenas apontar

## Quality Criteria

- [ ] Veredito explícito na primeira linha
- [ ] Tabela de distribuição com efetivo, meta e situação por etapa
- [ ] Todos os itens auditados individualmente
- [ ] Cada apontamento identifica item por número e data
- [ ] Bloqueadores e ressalvas separados e contados
- [ ] Cada bloqueador traz correção acionável
- [ ] Seção de verificações aprovadas lista o que efetivamente passou
