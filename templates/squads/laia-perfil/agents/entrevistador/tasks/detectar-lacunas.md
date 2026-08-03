---
task: "Detectar Lacunas"
order: 2
input: |
  - briefing_consolidado: output/briefing-consolidado.md
  - criterios: pipeline/data/quality-criteria.md (campos críticos e bloqueadores)
output: |
  - lacunas: lista priorizada de lacunas com perguntas de aprofundamento (output/lacunas.md)
---

# Detectar Lacunas

Audita o briefing consolidado e produz a lista de perguntas de aprofundamento que o cliente
precisa responder para o perfil ficar operável. Classifica cada lacuna por criticidade e
limita a rodada a no máximo 8 perguntas.

## Process

1. **Listar todos os campos marcados `PENDENTE`** no briefing consolidado.

2. **Listar campos preenchidos porém vagos.** Um campo é vago quando contém apenas adjetivo
   sem exemplo ("tom descontraído"), quantificador impreciso ("público jovem") ou lista com
   menos itens que o mínimo definido em `pipeline/data/quality-criteria.md` (ex.: menos de
   3 dores mapeadas).

3. **Listar inconsistências cruzadas** registradas na seção de observações do briefing, mais
   qualquer conflito adicional entre plataformas declaradas, objetivos e frequência.

4. **Classificar cada item** como:
   - `CRÍTICA` — bloqueia a Camada 2 ou 3 (ex.: nenhuma dor, nenhuma plataforma, sem meta)
   - `IMPORTANTE` — degrada a qualidade mas não impede produzir
   - `OPCIONAL` — refinamento

5. **Formular uma pergunta por lacuna**, em linguagem do cliente, explicando em uma linha o
   que muda na prática se ela for respondida. Ordenar por criticidade.

6. **Cortar em 8 perguntas.** Se houver mais, manter todas as `CRÍTICA`, completar com as
   `IMPORTANTE` mais impactantes e registrar o restante em "Fica para depois".

## Output Format

```markdown
# Lacunas Detectadas — {Nome do Cliente}

**Total:** {N} lacunas ({N} críticas, {N} importantes, {N} opcionais)
**Nesta rodada:** {N} perguntas

## Perguntas desta rodada

### 1. [{CRÍTICA|IMPORTANTE|OPCIONAL}] {campo}
**Pergunta:** {pergunta em linguagem do cliente}
**Por que importa:** {consequência prática de uma linha}

## Inconsistências a resolver
- **{campo A} vs {campo B}:** {os dois lados citados} → {pergunta de desempate}

## Fica para depois
- {campo}: {motivo de ter sido adiada}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Lacunas Detectadas — LAIA

**Total:** 6 lacunas (2 críticas, 3 importantes, 1 opcional)
**Nesta rodada:** 6 perguntas

## Perguntas desta rodada

### 1. [CRÍTICA] visual.paleta
**Pergunta:** Quais são as cores da marca? Se tiver os códigos hexadecimais (tipo #1A1A2E),
me manda; se não, descreve as cores e eu proponho os códigos pra você aprovar.
**Por que importa:** sem código de cor exato, todos os carrosséis saem com cor genérica.

### 2. [CRÍTICA] objetivos.historico_nao_funcionou
**Pergunta:** O que você já postou que claramente não funcionou?
**Por que importa:** sem isso o sistema pode repetir exatamente o formato que já falhou.

### 3. [IMPORTANTE] comunicacao.tom_de_voz
**Pergunta:** Você disse "tom descontraído". Me manda um post ou áudio seu que representa
bem como você fala?
**Por que importa:** "descontraído" varia muito — com um exemplo real o texto sai com a
sua voz, não com uma voz genérica de internet.

## Inconsistências a resolver
- **objetivos.plataformas vs publico.onde_estao:** o bloco 4 lista LinkedIn como ativo, o
  bloco 2 aponta o público só no Instagram e em grupos de WhatsApp → o LinkedIn é para o
  mesmo público ou para um segundo público (ex.: parceiros e clientes maiores)?

## Fica para depois
- visual.elementos_graficos: refinamento; os carrosséis funcionam sem isso na v1.
```

## Quality Criteria

- [ ] Toda lacuna `CRÍTICA` corresponde a um bloqueador de `quality-criteria.md`
- [ ] Máximo de 8 perguntas na rodada
- [ ] Cada pergunta está em linguagem do cliente, sem jargão de marketing
- [ ] Cada pergunta explica a consequência prática em uma linha
- [ ] Inconsistências citam os dois lados literalmente
- [ ] Lacunas adiadas estão registradas, não descartadas

## Veto Conditions

Rejeitar e refazer se:
1. A rodada tem mais de 8 perguntas
2. Alguma lacuna crítica foi omitida ou rebaixada para caber no limite
3. Alguma pergunta já tem resposta explícita no briefing consolidado
4. As perguntas não indicam o campo do schema a que se referem
