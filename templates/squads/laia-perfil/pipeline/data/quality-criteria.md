# Quality Criteria — Perfil de Cliente LAIA

Checklist canônica usada pela Renata Revisão no Step 10. É fixa: não se reinterpreta a cada
execução. Só **bloqueador** reprova; pendência tolerável nunca soma para reprovação.

---

## 1. Bloqueadores (reprovam o perfil)

| # | Campo | Condição de aprovação |
|---|---|---|
| 1 | `identidade.nicho` | preenchido e específico (não "marketing", mas "marketing para clínicas") |
| 2 | `identidade.ofertas` | ≥ 1 oferta com `nome` e `promessa`; `preco` pode ser pendência |
| 3 | `publico.quem_sao` | preenchido com recorte identificável, nunca "público em geral" |
| 4 | `publico.dores` | ≥ 3 itens, cada um descrevendo situação concreta |
| 5 | `comunicacao.tom_de_voz` | preenchido |
| 6 | `objetivos.meta_principal` | exatamente uma meta dominante |
| 7 | `objetivos.plataformas` | ≥ 1 plataforma válida (`Instagram` e/ou `LinkedIn`) |
| 8 | `objetivos.frequencia` | preenchida no formato `N por semana` |
| 9 | `visual.paleta` | ≥ 2 cores com hex `#RRGGBB` válido |

### Teste de "situação concreta" para dores
Uma dor passa se descreve **o que acontece**, não como a pessoa se sente em abstrato.

- ✅ "Chega no fim do mês sem saber quanto lucrou"
- ✅ "Perde lead porque demora dois dias pra responder"
- ❌ "Desorganização"
- ❌ "Falta de tempo"

---

## 2. Integridade técnica (reprova antes de qualquer outra checagem)

- [ ] `perfil.json` faz parse como JSON válido
- [ ] Todas as chaves do schema existem, inclusive as de valor `null`
- [ ] Campos de lista são arrays, mesmo com um único elemento
- [ ] Todo hex segue o padrão `#RRGGBB` em maiúsculas
- [ ] `meta.slug` é minúsculo, sem acento e sem espaço
- [ ] Todo campo `null` ou array abaixo do mínimo tem entrada em `pendencias`

---

## 3. Consistência cruzada (achado, não necessariamente bloqueador)

| Verificação | Como avaliar |
|---|---|
| Plataformas × onde o público está | LinkedIn ativo mas público só no Instagram → questionar |
| Frequência × nº de plataformas | 5 por semana em 2 plataformas = 10 conteúdos/mês por canal |
| `palavras_evitar` × `palavras_usar` | nenhum termo pode estar nas duas listas |
| `objetivos.ofertas_atuais` × `identidade.ofertas` | toda oferta citada deve existir |
| Percepção desejada × preço | "premium" com ticket baixo é tensão a sinalizar |
| Brand book × `perfil.json` | nenhuma afirmação do documento fora do JSON |

---

## 4. Pendências toleráveis (aprovam com ressalva)

- `visual.logo` ausente — slides saem sem logo na assinatura
- `visual.elementos_graficos` vazio — não afeta a geração
- `visual.fotos_referencia` vazio — não afeta a geração
- `comunicacao.referencias` com menos de 2 itens
- `objetivos.historico_funcionou` / `historico_nao_funcionou` vazios — primeiro mês roda
  em modo exploratório, sem feedback loop
- `identidade.diferenciais` com 1 item
- `publico.faixa_etaria` ausente

---

## 5. Escala de completude (informativa, não decide aprovação)

| Faixa | Leitura |
|---|---|
| 0 bloqueadores, ≤ 2 pendências | Perfil forte — produção em capacidade total |
| 0 bloqueadores, 3-6 pendências | Perfil operável — produção com ressalvas |
| 0 bloqueadores, > 6 pendências | Operável, mas vale nova rodada de lacunas |
| ≥ 1 bloqueador | Não operável — reprovado |

---

## 6. Regras do ciclo de revisão

- Máximo de **2 ciclos** automáticos de `on_reject` entre Step 10 e Step 09.
- No terceiro, apresentar ao usuário para decisão manual em vez de manter o loop.
- Correção pedida pelo usuário no checkpoint 11 **não** conta para esse limite.
- A revisora nunca corrige: aponta o campo, o problema e a correção esperada.
