---
task: "Revisar Entrega"
order: 1
input: |
  - carrossel: output/carrossel.md
  - linkedin: output/linkedin.md
  - imagens: output/slides/rendered/
  - pesquisa: output/pesquisa.md (para checar lastro dos dados)
  - angulos_selecionados: output/angulos-selecionados.yaml (para checar promessa cumprida)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json
  - criterios: pipeline/data/quality-criteria.md
output: |
  - revisao: veredito com nota por eixo (output/revisao-final.md)
---

# Revisar Entrega

Avalia copy e visual contra cinco eixos e emite APROVADO ou REPROVADO com nota ponderada.
Veracidade é eliminatória.

## Process

1. **Eixo Veracidade (eliminatório).** Conferir **cada** dado citado no carrossel e no post
   contra o relatório de pesquisa: o número existe? a grandeza é a mesma? a fonte confere?
   Um dado sem lastro derruba a entrega independentemente dos outros eixos.

2. **Eixo Scroll-stop (peso 1,5).** Avaliar o slide 1 e a primeira linha do LinkedIn
   isoladamente, como o público os vê. O gancho aprovado está literal? Para o polegar?

3. **Eixo Aderência ao perfil.** Com o `perfil.json` aberto: nenhuma palavra de
   `palavras_evitar`; tom compatível com `tom_de_voz`; cores das imagens dentro de
   `visual.paleta`.

4. **Eixo Estrutura do formato.** Carrossel: 6 a 10 slides, ≤30 palavras por slide, reflexão
   antes do CTA, CTA específico, legenda com 5-15 hashtags. LinkedIn: gancho antes do "ver
   mais", blocos ≤3 linhas, insight explícito, 3-5 hashtags.

5. **Eixo Execução visual.** Inspecionar as imagens renderizadas: legibilidade, texto não
   cortado, consistência entre slides, dimensões corretas.

6. **Verificar a promessa do ângulo.** O conteúdo entrega o que o ângulo aprovado prometeu?
   Promessa não cumprida é defeito de scroll-stop, não de estrutura.

7. **Calcular a nota ponderada:**
   `(scroll_stop × 1,5 + aderencia + veracidade + estrutura + visual) / 5,5`
   Aprovar com nota ≥ 7,0 **e** veracidade ≥ 8,0. Abaixo disso, REPROVADO.

## Output Format

```markdown
# VEREDITO: APROVADO | REPROVADO — Nota {X,X}/10

**Ciclo:** {N} de 2

## Notas por eixo
| Eixo | Peso | Nota | Comentário |
| Scroll-stop | 1,5 | | |
| Aderência ao perfil | 1,0 | | |
| Veracidade (eliminatório) | 1,0 | | |
| Estrutura do formato | 1,0 | | |
| Execução visual | 1,0 | | |

**Cálculo:** ({nota}×1,5 + {nota} + {nota} + {nota} + {nota}) / 5,5 = **{X,X}**

## Problemas encontrados
### {Slide N | trecho do post} — eixo {eixo}
**Problema:** {defeito}
**Correção esperada:** {ação}

## Verificação de dados
| Dado citado | Existe na pesquisa? | Confere? |

## Verificações aprovadas
- {checagem que passou}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# VEREDITO: APROVADO — Nota 8,5/10

**Ciclo:** 1 de 2

## Notas por eixo
| Eixo | Peso | Nota | Comentário |
|---|---|---|---|
| Scroll-stop | 1,5 | 9 | Capa curta, contraintuitiva, alto contraste; gancho literal |
| Aderência ao perfil | 1,0 | 9 | Tom didático e direto, sem jargão; nenhuma palavra proibida |
| Veracidade | 1,0 | 9 | Todos os 2 dados com lastro; origem internacional declarada |
| Estrutura do formato | 1,0 | 8 | 8 slides, reflexão presente, CTA específico; slide 7 com 34 palavras |
| Execução visual | 1,0 | 7 | Consistente e legível; slide 7 com texto próximo da margem |

**Cálculo:** (9×1,5 + 9 + 9 + 8 + 7) / 5,5 = **8,5**

## Problemas encontrados
### Slide 7 — eixo Estrutura do formato
**Problema:** 34 palavras, acima do teto de 30. O CTA tem duas instruções ("escreve num
papel" e "salva esse carrossel") competindo pela mesma atenção.
**Correção esperada:** manter apenas o "salva", que é a ação de maior valor no formato, e
mover o exercício do papel para a legenda.

### Slide 7 — eixo Execução visual
**Problema:** o texto termina a 62px da margem inferior, contra os 96px do grid.
**Correção esperada:** reduzir o corpo de 46px para 42px, dentro da escala definida.

## Verificação de dados
| Dado citado | Existe na pesquisa? | Confere? |
|---|---|---|
| "4 em 10 empresas abandonam a automação nos primeiros 3 meses" | sim (2026-02, MÉDIA) | sim — grandeza e recorte idênticos |
| "11 horas semanais" (citado na legenda) | sim (2025-11, ALTA) | sim — origem internacional declarada na legenda |

## Verificações aprovadas
- Gancho aprovado 3b aparece literal no slide 1
- Promessa do ângulo cumprida: o conteúdo explica por que o problema é de processo
- Nenhuma palavra de `comunicacao.palavras_evitar` ("disruptivo", "revolucionário",
  "solução inovadora")
- Todas as cores das imagens vêm de `visual.paleta`
- 8 hashtags na legenda, dentro da faixa de 5-15
- 8 slides, dentro da faixa de 6-10
- Reflexão presente no slide 6, antes do CTA

**Observação:** os dois problemas são de baixa gravidade e não reprovam. Recomendo aplicar
antes de publicar, mas a entrega está aprovada.
```

## Quality Criteria

- [ ] Veredito e nota ponderada na primeira linha
- [ ] Cinco eixos com nota de 0 a 10
- [ ] Cálculo da ponderação explicitado
- [ ] Cada dado do conteúdo verificado contra a pesquisa, em tabela
- [ ] Aderência verificada com o `perfil.json` aberto
- [ ] Imagens renderizadas inspecionadas
- [ ] Cada problema identifica slide ou trecho e traz correção
- [ ] Nenhuma correção aplicada pela auditora

## Veto Conditions

Rejeitar e refazer se:
1. Veredito APROVADO com veracidade abaixo de 8,0
2. Veredito APROVADO com nota ponderada abaixo de 7,0
3. Algum dado do conteúdo não foi verificado contra a pesquisa
4. As imagens renderizadas não foram inspecionadas
5. A auditora reescreveu trechos do conteúdo em vez de apontar
