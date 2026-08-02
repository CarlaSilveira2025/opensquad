---
task: "Validar Perfil"
order: 1
input: |
  - perfil: output/perfil.json
  - brand_book: output/brand-book.md
  - criterios: pipeline/data/quality-criteria.md
  - anti_padroes: pipeline/data/anti-patterns.md
output: |
  - validacao: veredito e lista de correções (output/validacao-perfil.md)
---

# Validar Perfil

Audita o perfil estruturado contra a checklist fixa de bloqueadores e emite APROVADO ou
REPROVADO. Não corrige nada — aponta. A correção é responsabilidade da Perfiladora no ciclo
de rejeição.

## Process

1. **Verificar integridade técnica.** O `perfil.json` faz parse? Todas as chaves do schema
   existem? Tipos corretos (arrays onde o schema pede array)?

2. **Rodar a checklist de bloqueadores** de `pipeline/data/quality-criteria.md` por inteiro,
   sem parar no primeiro erro. Os bloqueadores canônicos são: `identidade.nicho`,
   `identidade.ofertas` (mín. 1), `publico.dores` (mín. 3), `publico.quem_sao`,
   `comunicacao.tom_de_voz`, `objetivos.meta_principal`, `objetivos.plataformas` (mín. 1),
   `objetivos.frequencia` e `visual.paleta` (mín. 2 cores com hex válido).

3. **Verificar consistência cruzada.** Plataformas declaradas coerentes com onde o público
   está; frequência compatível com o número de plataformas; palavras a evitar não colidindo
   com palavras a usar; ofertas citadas nos objetivos existentes em `identidade.ofertas`.

4. **Verificar espelhamento com o brand book.** Nenhum valor do documento pode contradizer
   o JSON.

5. **Classificar cada achado** como bloqueador ou pendência tolerável. Só bloqueador reprova.

6. **Emitir o veredito na primeira linha** e detalhar em seguida, com o caminho do campo em
   notação de ponto e a correção esperada.

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

> Referência de qualidade, não gabarito.

```markdown
# VEREDITO: REPROVADO

**Bloqueadores:** 2 · **Pendências toleráveis:** 3
**Ciclo de revisão:** 1 de 2

## Bloqueadores
### `visual.paleta`
**Problema:** a paleta tem apenas uma cor com hex válido (`#1A1A2E`); a segunda entrada
está como `{"nome": "verde", "hex": null}`.
**Correção esperada:** no mínimo 2 cores com hex `#RRGGBB` válido, ou registrar a cor
como pendência crítica e remover a entrada incompleta do array.

### `publico.dores`
**Problema:** apenas 2 dores mapeadas; o mínimo operável é 3.
**Correção esperada:** 3 dores concretas do público, cada uma descrevendo uma situação
real e não um adjetivo.

## Inconsistências cruzadas
- `objetivos.plataformas` vs `publico.onde_estao`: plataformas lista `["Instagram",
  "LinkedIn"]`, mas o público está mapeado apenas no Instagram e em grupos de WhatsApp →
  ou o LinkedIn atende um segundo público, ou deve sair da lista de plataformas.

## Pendências toleráveis
- `visual.elementos_graficos`: vazio — os slides funcionam sem elementos gráficos próprios
- `comunicacao.referencias`: apenas 1 referência — mais referências melhoram a calibragem
- `identidade.diferenciais`: 2 itens — aceitável, 3 seria ideal

## Verificações aprovadas
- JSON válido e com todas as chaves do schema
- Brand book espelha o JSON sem contradições
- `objetivos.frequencia` compatível com o número de plataformas
```

## Quality Criteria

- [ ] Primeira linha traz o veredito explícito
- [ ] Todos os 9 bloqueadores canônicos foram verificados, mesmo após achar um erro
- [ ] Cada achado cita o campo em notação de ponto
- [ ] Cada bloqueador traz correção acionável
- [ ] Bloqueadores e pendências toleráveis em seções separadas e contados
- [ ] Nenhuma correção foi aplicada pela revisora

## Veto Conditions

Rejeitar e refazer se:
1. O veredito é APROVADO com pelo menos um bloqueador listado
2. O veredito é REPROVADO apenas por pendências toleráveis
3. A checklist foi interrompida no primeiro erro encontrado
4. Algum achado não indica o campo correspondente
