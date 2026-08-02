# Quality Criteria — Produção de Conteúdo LAIA

Critérios usados pela Vera Veredito no Step 12 e pelos vetos de cada step.

---

## 1. Eixos de avaliação e pesos

| Eixo | Peso | O que mede |
|---|---|---|
| **Scroll-stop** | 1,5 | O slide 1 / a 1ª linha param o polegar? |
| **Aderência ao perfil** | 1,0 | Tom, palavras e paleta conferem com o `perfil.json`? |
| **Veracidade** | 1,0 | Todo dado tem lastro no relatório de pesquisa? |
| **Estrutura do formato** | 1,0 | Os limites do formato foram respeitados? |
| **Execução visual** | 1,0 | As imagens são legíveis, consistentes e corretas? |

```
nota = (scroll_stop × 1,5 + aderencia + veracidade + estrutura + visual) / 5,5
```

**Aprovação:** nota ≥ 7,0 **e** veracidade ≥ 8,0.

**Veracidade é eliminatória:** um dado sem lastro reprova sozinho, independentemente do resto.

---

## 2. Limites por formato

### Carrossel Instagram
- [ ] Entre 6 e 10 slides
- [ ] Máximo ~30 palavras e 5 linhas visíveis por slide
- [ ] Slide 1 com o gancho aprovado, literal
- [ ] Uma ideia por slide, com progressão
- [ ] Slide de reflexão antes do CTA
- [ ] CTA específico e conectado ao tema
- [ ] Legenda como peça própria, com 5 a 15 hashtags
- [ ] Indicação de elemento visual em todos os slides

### Post LinkedIn
- [ ] Gancho aprovado, literal, na primeira linha
- [ ] Três primeiras linhas ≤ ~200 caracteres, com sentido isoladas
- [ ] Abre com cena concreta, não com tese
- [ ] Blocos de no máximo 3 linhas
- [ ] Insight explícito antes do CTA
- [ ] Entre 3 e 5 hashtags
- [ ] Peça visual sugerida com tipo, conteúdo e dimensão
- [ ] Texto distinto do carrossel, quando ambos existem

---

## 3. Critérios de pesquisa (Fase 3.1)

- [ ] Mínimo de 3 buscas com ângulos diferentes
- [ ] Todo dado com número, fonte identificável e data
- [ ] Mínimo de 3 dados com confiança ALTA ou MÉDIA
- [ ] Fontes principais abertas com `web_fetch`
- [ ] Perguntas frequentes observadas, com origem registrada
- [ ] Saturação declarada por contagem (3+ peças), com exemplo concreto
- [ ] Recortes ausentes cruzados com dores do perfil
- [ ] Limitações da coleta declaradas
- [ ] Nenhum ângulo ou gancho proposto

---

## 4. Critérios de ângulos (Fase 3.2)

- [ ] Mínimo de 5 ângulos, todos sobre o mesmo assunto
- [ ] Lentes distintas; nenhum par aceita a mesma abertura
- [ ] `ancora_pesquisa` preenchida em todos
- [ ] Provocação distribuída, não concentrada em 4 e 5
- [ ] Risco declarado em todo ângulo com provocação ≥ 4
- [ ] `diferenciador` presente em ângulo de lente saturada
- [ ] Recomendação justificada pelo perfil

---

## 5. Critérios de ganchos (Fase 3.3)

- [ ] Exatamente 3 por ângulo, de 3 tipos diferentes
- [ ] Texto final, não esboço
- [ ] Máximo de 2 linhas visíveis
- [ ] Ganchos de LinkedIn ≤ ~200 caracteres
- [ ] Gancho de dado com número existente na pesquisa
- [ ] Nenhuma palavra de `comunicacao.palavras_evitar`
- [ ] Abertura visual e promessa preenchidas
- [ ] Nenhuma fórmula batida ("você sabia que", "neste post vou te contar")

---

## 6. Critérios visuais (Fase 3.5)

- [ ] Todas as cores de `visual.paleta` (neutros puros permitidos)
- [ ] Sistema visual definido antes do primeiro slide
- [ ] Nenhuma fonte abaixo de 32px
- [ ] Margem externa ≥ 80px em peça de 1080px
- [ ] Nenhuma palavra do texto aprovado alterada
- [ ] HTML autocontido, sem referência de rede
- [ ] Dimensões corretas por plataforma
- [ ] Nenhuma imagem em branco, cortada ou transbordando
- [ ] Contraste verificado em todos os slides
- [ ] Ordem de publicação listada

---

## 7. Escala de nota por eixo

| Faixa | Leitura |
|---|---|
| 9-10 | Exemplar — serve de referência para os próximos |
| 7-8 | Aprovado — pode ter ressalva de baixa gravidade |
| 5-6 | Insuficiente — reprova o eixo |
| 0-4 | Defeito grave — reprova a entrega |

---

## 8. Regras do ciclo de revisão

- Máximo de **2 ciclos** de `on_reject` entre Step 12 e Step 07.
- No terceiro, apresentar ao usuário para decisão manual.
- Ajustes pedidos pelo usuário nos checkpoints 09 e 11 **não** contam nesse limite.
- A auditora nunca corrige: aponta slide ou trecho, problema e correção esperada.
