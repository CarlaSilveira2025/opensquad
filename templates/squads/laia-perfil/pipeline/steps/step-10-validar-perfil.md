---
step: "10"
name: "Validação do Perfil"
type: agent
execution: inline
agent: revisor
tasks:
  - validar-perfil
depends_on: step-09
on_reject: step-09
inputFile: squads/laia-perfil/output/perfil.json
outputFile: squads/laia-perfil/output/validacao-perfil.md
---

# Step 10: Renata Revisão — Validação do Perfil

## Context Loading

Carregar antes de executar:

- `squads/laia-perfil/output/perfil.json` — perfil estruturado a auditar
- `squads/laia-perfil/output/brand-book.md` — versão legível, para checar espelhamento
- `squads/laia-perfil/pipeline/data/quality-criteria.md` — checklist canônica de
  bloqueadores e mínimos por campo
- `squads/laia-perfil/pipeline/data/anti-patterns.md` — erros conhecidos de perfil

## Instructions

### Process

1. **Verificar integridade técnica.** Conferir que o JSON faz parse, que todas as chaves do
   schema existem e que os tipos batem — em especial que campos de lista são arrays.

2. **Rodar a checklist completa de bloqueadores**, sem interromper no primeiro erro. Os nove
   bloqueadores canônicos: `identidade.nicho`, `identidade.ofertas` (mín. 1),
   `publico.quem_sao`, `publico.dores` (mín. 3), `comunicacao.tom_de_voz`,
   `objetivos.meta_principal`, `objetivos.plataformas` (mín. 1), `objetivos.frequencia`,
   `visual.paleta` (mín. 2 cores com hex `#RRGGBB` válido).

3. **Verificar consistência cruzada.** Plataformas versus onde o público está; frequência
   versus número de plataformas; `palavras_evitar` sem colidir com `palavras_usar`; ofertas
   citadas em `objetivos.ofertas_atuais` existentes em `identidade.ofertas`.

4. **Verificar espelhamento com o brand book.** Qualquer afirmação do documento que não
   exista no JSON é achado.

5. **Classificar cada achado** como bloqueador ou pendência tolerável, contar cada grupo e
   emitir o veredito na primeira linha do arquivo. Gravar em
   `squads/laia-perfil/output/validacao-perfil.md`.

6. **Não corrigir nada.** Em caso de REPROVADO, o pipeline retorna ao Step 09 via
   `on_reject`, no máximo 2 ciclos; no terceiro, apresentar ao usuário para decisão manual.

## Output Format

```markdown
# VEREDITO: APROVADO | REPROVADO

**Bloqueadores:** {N} · **Pendências toleráveis:** {N}
**Ciclo de revisão:** {N} de 2

## Bloqueadores
### `{campo.em.ponto}`
**Problema:** {o que está errado}
**Correção esperada:** {o que precisa estar lá}

## Inconsistências cruzadas
- `{campo A}` vs `{campo B}`: {descrição} → {correção esperada}

## Pendências toleráveis
- `{campo}`: {descrição} — não bloqueia a produção

## Verificações aprovadas
- {checagem que passou}
```

## Output Example

```markdown
# VEREDITO: APROVADO

**Bloqueadores:** 0 · **Pendências toleráveis:** 3
**Ciclo de revisão:** 2 de 2

## Bloqueadores
Nenhum.

## Inconsistências cruzadas
Nenhuma. A frequência declarada (3 por semana) é compatível com as 2 plataformas ativas,
e todas as ofertas citadas em `objetivos.ofertas_atuais` existem em `identidade.ofertas`.

## Pendências toleráveis
- `visual.logo`: `null` — os carrosséis serão gerados sem logo até o arquivo ser enviado
  para `_opensquad/_memory/clientes/authentic-studio/assets/`
- `objetivos.historico_nao_funcionou`: lista vazia — o primeiro mês roda sem feedback loop
  e o calendário opera em modo exploratório
- `visual.elementos_graficos`: lista vazia — não afeta a geração de slides

## Verificações aprovadas
- JSON válido, 41 chaves do schema presentes, tipos corretos
- `publico.dores` com 3 dores concretas, todas em formato de situação
- `visual.paleta` com 2 cores em hex válido (#12233A, #C9A227)
- `comunicacao.tom_de_voz` acompanhado de amostra de voz real do cliente
- Brand book espelha o JSON sem contradições
- `palavras_evitar` não colide com `palavras_usar`
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. O veredito é APROVADO havendo pelo menos um bloqueador listado
2. O veredito é REPROVADO tendo apenas pendências toleráveis
3. A checklist foi interrompida ao encontrar o primeiro erro
4. Algum achado não indica o campo em notação de ponto
5. A revisora aplicou correção no `perfil.json` em vez de apenas apontar

## Quality Criteria

- [ ] Veredito explícito na primeira linha do arquivo
- [ ] Os nove bloqueadores canônicos foram todos verificados
- [ ] Bloqueadores e pendências toleráveis em seções separadas, com contagem
- [ ] Cada bloqueador traz correção acionável
- [ ] Seção de verificações aprovadas lista o que efetivamente passou
- [ ] Contador de ciclo de revisão presente e correto
