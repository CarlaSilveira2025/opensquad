---
step: "12"
name: "Revisão Final"
type: agent
execution: inline
agent: revisor
tasks:
  - revisar-entrega
depends_on: step-11
on_reject: step-10   # defeito visual recicla so o designer; defeito de texto o revisor aponta para o step-07
inputFile: squads/laia-conteudo/output/carrossel.md
outputFile: squads/laia-conteudo/output/revisao-final.md
---

# Step 12: Vera Veredito — Revisão Final

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/carrossel.md` — copy do carrossel, se existir
- `squads/laia-conteudo/output/linkedin.md` — copy do LinkedIn, se existir
- `squads/laia-conteudo/output/slides/rendered/` — imagens renderizadas, para inspeção
- `squads/laia-conteudo/output/pesquisa.md` — para verificar o lastro de cada dado
- `squads/laia-conteudo/output/angulos-selecionados.yaml` — para verificar a promessa
- `squads/laia-conteudo/output/ganchos-selecionados.yaml` — para verificar o gancho literal
- `_opensquad/_memory/clientes/{slug}/perfil.json` — aderência de tom, palavras e paleta
- `squads/laia-conteudo/pipeline/data/quality-criteria.md` — eixos e pesos

## Instructions

### Process

1. **Verificar veracidade primeiro (eixo eliminatório).** Conferir cada dado citado no
   carrossel e no post contra o relatório de pesquisa: o número existe? a grandeza é a
   mesma? a fonte confere? Montar a tabela de verificação dado a dado.

2. **Avaliar scroll-stop (peso 1,5).** Ler o slide 1 e a primeira linha do LinkedIn
   isoladamente, como o público os vê. Conferir que o gancho aprovado está literal.

3. **Avaliar aderência ao perfil** com o `perfil.json` aberto: nenhuma palavra de
   `palavras_evitar`, tom compatível, cores das imagens dentro de `visual.paleta`.

4. **Avaliar estrutura do formato** contra os limites, que vivem nos arquivos de formato do
   framework — `_opensquad/core/best-practices/instagram-feed.md` e `linkedin-post.md`.
   **Ler os dois antes de avaliar**; eles são a autoridade e prevalecem sobre qualquer
   número citado aqui. Em resumo: carrossel com 8-10 slides, 40-80 palavras por slide em
   duas camadas, formato canônico declarado, síntese antes do CTA, 5-15 hashtags;
   LinkedIn com gancho antes do "ver mais", blocos ≤3 linhas, 3-5 insights, 3-5 hashtags,
   sem link no corpo.

5. **Avaliar execução visual** inspecionando as imagens: legibilidade, texto não cortado,
   consistência entre slides, dimensões corretas.

6. **Verificar a promessa do ângulo.** O conteúdo entrega o que o ângulo aprovado prometeu?

7. **Calcular a nota ponderada** e emitir o veredito na primeira linha:
   `(scroll_stop × 1,5 + aderencia + veracidade + estrutura + visual) / 5,5`
   APROVADO com nota ≥ 7,0 **e** veracidade ≥ 8,0. Não corrigir nada.

## Output Format

```markdown
# VEREDITO: APROVADO | REPROVADO — Nota {X,X}/10

**Ciclo:** {N} de 2

## Notas por eixo
| Eixo | Peso | Nota | Comentário |

**Cálculo:** ({nota}×1,5 + {nota} + {nota} + {nota} + {nota}) / 5,5 = **{X,X}**

## Problemas encontrados
### {Slide N | trecho} — eixo {eixo}
**Problema:** {defeito}
**Correção esperada:** {ação}

## Verificação de dados
| Dado citado | Existe na pesquisa? | Confere? |

## Verificações aprovadas
- {checagem que passou}
```

## Output Example

```markdown
# VEREDITO: APROVADO — Nota 8,5/10

**Ciclo:** 1 de 2

## Notas por eixo
| Eixo | Peso | Nota | Comentário |
|---|---|---|---|
| Scroll-stop | 1,5 | 9 | Capa curta, contraintuitiva, alto contraste; gancho literal |
| Aderência ao perfil | 1,0 | 9 | Tom didático e direto; nenhuma palavra proibida |
| Veracidade | 1,0 | 9 | Os 2 dados com lastro; origem internacional declarada |
| Estrutura do formato | 1,0 | 8 | 8 slides, síntese presente; slide 7 com 34 palavras (abaixo do piso de 40) |
| Execução visual | 1,0 | 7 | Consistente e legível; slide 7 com texto perto da margem |

**Cálculo:** (9×1,5 + 9 + 9 + 8 + 7) / 5,5 = **8,5**

## Problemas encontrados
### Slide 7 — eixo Estrutura do formato
**Problema:** 34 palavras, abaixo do piso de 40. O texto de apoio só reformula a headline
em vez de acrescentar dado ou consequência — o slide fica raso.
**Correção esperada:** expandir o apoio com o dado que sustenta a afirmação, chegando à
faixa de 40 a 80 palavras sem alterar a headline.

### Slide 7 — eixo Execução visual
**Problema:** o texto termina a 62px da margem inferior, contra os 96px do grid.
**Correção esperada:** reduzir o corpo de 46px para 42px, dentro da escala definida.

## Verificação de dados
| Dado citado | Existe na pesquisa? | Confere? |
|---|---|---|
| "4 em 10 empresas abandonam nos primeiros 3 meses" | sim (2026-02, MÉDIA) | sim |
| "11 horas semanais" (na legenda) | sim (2025-11, ALTA) | sim — origem declarada |

## Verificações aprovadas
- Gancho aprovado 3b literal no slide 1
- Promessa do ângulo cumprida
- Nenhuma palavra de `comunicacao.palavras_evitar`
- Todas as cores das imagens vêm de `visual.paleta`
- 8 slides e 8 hashtags, ambos dentro das faixas
- Reflexão presente no slide 6, antes do CTA

**Observação:** os dois problemas são de baixa gravidade e não reprovam. Vale aplicar antes
de publicar.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Veredito APROVADO com veracidade abaixo de 8,0
2. Veredito APROVADO com nota ponderada abaixo de 7,0
3. Algum dado do conteúdo não aparece na tabela de verificação
4. As imagens renderizadas não foram inspecionadas
5. A auditora reescreveu trechos do conteúdo em vez de apontar

## Quality Criteria

- [ ] Veredito e nota ponderada na primeira linha
- [ ] Cinco eixos com nota e comentário
- [ ] Cálculo da ponderação explicitado
- [ ] Tabela de verificação com todos os dados citados
- [ ] Aderência verificada com o perfil aberto
- [ ] Copy e visual auditados
- [ ] Cada problema identifica slide ou trecho e traz correção
