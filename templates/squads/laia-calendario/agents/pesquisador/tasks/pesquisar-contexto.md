---
task: "Pesquisar Contexto"
order: 2
input: |
  - briefing_mes: output/briefing-mes.md (mês de referência e foco)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (nicho, público, dores)
output: |
  - secao_contexto: tendências, assuntos em alta e ganchos sazonais do mês
---

# Pesquisar Contexto

Levanta o cenário externo do mês: o que está em alta no nicho, quais assuntos conectados ao
negócio ganharam tração, e quais datas sazonais têm ligação real com o cliente. Saída
parcial — compõe o relatório final junto com as outras duas tasks.

## Process

1. **Montar três ângulos de busca a partir do nicho e das dores do perfil.** Exemplo para
   nicho de automação: (a) tendência do setor, (b) dúvida frequente do público, (c) mudança
   recente de ferramenta ou regulação. Nunca uma busca só.

2. **Executar as buscas com `web_search`** delimitando a janela temporal ao período definido
   no briefing do mês. Abrir com `web_fetch` as fontes mais relevantes para confirmar data e
   conteúdo — título de resultado de busca não é fonte verificada.

3. **Classificar cada achado** como tendência (ganhando tração), assunto em alta (volume
   alto agora) ou saturado (volume alto e já explorado à exaustão). Saturação vai para seção
   própria, porque serve para evitar tema, não para escolher.

4. **Levantar as datas do mês** — comemorativas, sazonais e do setor. Para cada uma,
   escrever a conexão concreta com o negócio do cliente em uma linha. Data sem conexão
   concreta **não entra na lista**.

5. **Atribuir confiança**: `ALTA` para 3 ou mais fontes independentes, `MÉDIA` para 2,
   `BAIXA` para 1.

6. **Declarar frentes vazias.** Se o nicho não tem sazonalidade relevante no mês, escrever
   isso explicitamente em vez de listar datas genéricas.

## Output Format

```markdown
## Contexto do Nicho

### Tendências
| Achado | Fonte | Data | Confiança | Conexão com o público |

### Assuntos em alta
| Assunto | Fonte | Data | Confiança | Dor que toca |

### Temas saturados (evitar)
| Tema | Por que está saturado | Fonte |

### Ganchos sazonais do mês
| Data | Evento | Conexão concreta com o negócio |

### Frentes sem achado relevante
- {frente pesquisada e resultado vazio}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
## Contexto do Nicho

### Tendências
| Achado | Fonte | Data | Confiança | Conexão com o público |
|---|---|---|---|---|
| Pequenas empresas adotando agentes de atendimento antes de CRM | 3 publicações do setor | 2026-07 | ALTA | toca a dor "perde lead por demora na resposta" |

### Assuntos em alta
| Assunto | Fonte | Data | Confiança | Dor que toca |
|---|---|---|---|---|
| Custo real de implantação de IA em PME | 2 fontes | 2026-07 | MÉDIA | "testou IA e não saiu do ChatGPT" |

### Temas saturados (evitar)
| Tema | Por que está saturado | Fonte |
|---|---|---|
| "IA vai substituir empregos" | presente em 6 dos 8 perfis analisados no mês | análise de concorrentes |

### Ganchos sazonais do mês
| Data | Evento | Conexão concreta com o negócio |
|---|---|---|
| 15/08 | Fechamento de semestre contábil de PME | momento em que o dono revisa custo operacional — janela natural para conteúdo de fundo sobre ROI de automação |

### Frentes sem achado relevante
- Mudança regulatória no período: nada encontrado com fonte confiável para o mês.
```

## Quality Criteria

- [ ] No mínimo 3 buscas com ângulos diferentes
- [ ] Todo achado tem fonte, data e confiança
- [ ] Fontes principais confirmadas com `web_fetch`, não só pelo título do resultado
- [ ] Temas saturados em seção separada dos temas em alta
- [ ] Toda data sazonal listada tem conexão concreta explicada
- [ ] Frentes vazias declaradas explicitamente

## Veto Conditions

Rejeitar e refazer se:
1. Algum achado não tem data ou janela temporal
2. Alguma data sazonal foi listada sem conexão concreta com o negócio
3. Tema saturado aparece misturado com tema em alta
4. Alguma pauta ou tema de post foi recomendado — isso é papel da Estrategista
