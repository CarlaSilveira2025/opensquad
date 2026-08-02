---
task: "Pesquisar Fontes"
order: 1
input: |
  - briefing_item: output/briefing-item.md (assunto, etapa de funil, formato, plataforma)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (nicho, dores, público)
output: |
  - secao_fontes: dados, estatísticas, exemplos e perguntas frequentes sobre o assunto
---

# Pesquisar Fontes

Coleta a matéria-prima do conteúdo: dados com fonte, estatísticas que dão autoridade,
exemplos concretos e as perguntas que o público realmente faz sobre o assunto.

## Process

1. **Montar três ângulos de busca** a partir do assunto e das dores do perfil. Exemplo para
   "orçamento manual repetitivo": (a) dado sobre tempo gasto em tarefa repetitiva em PME,
   (b) casos de automação desse processo, (c) o que dá errado quando se automatiza mal.

2. **Executar as buscas com `web_search`** e abrir as fontes mais relevantes com
   `web_fetch`. Confirmar o número e o contexto na página — título de resultado não é fonte.

3. **Rastrear a fonte primária.** Quando um dado aparecer citado em vários lugares, buscar a
   origem. Registrar a fonte primária, não a republicação.

4. **Coletar perguntas frequentes reais.** Buscas relacionadas, comentários em posts do tema
   e dúvidas recorrentes em comunidades. Registrar onde cada uma foi observada. Nunca supor.

5. **Selecionar os dados âncora** — os 3 a 5 números mais fortes, candidatos a abrir o
   conteúdo. Priorizar o específico, o datado e o contraintuitivo.

6. **Marcar a confiança de cada achado**: `ALTA` (fonte primária verificada), `MÉDIA` (fonte
   secundária confiável), `BAIXA` (citação sem origem rastreada — usar com ressalva).

## Output Format

```markdown
## Fontes e Dados

### Dados âncora
| Dado | Número | Fonte | Data | Confiança |

### Dados de apoio
| Dado | Número | Fonte | Data | Confiança |

### Exemplos e casos concretos
- **{caso}**: {descrição em 2 linhas} — fonte: {origem}

### Perguntas frequentes do público
| Pergunta | Onde foi observada |

### Dores e desejos relacionados ao tema
- {dor do perfil} → {como este assunto se conecta a ela}

### Limitações da coleta
- {o que não foi encontrado ou não pôde ser verificado}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
## Fontes e Dados

### Dados âncora
| Dado | Número | Fonte | Data | Confiança |
|---|---|---|---|---|
| Tempo semanal em tarefas administrativas repetitivas em PME de serviço | 11h | pesquisa setorial citada e verificada na publicação original | 2025-11 | ALTA |
| Empresas que abandonam automação no primeiro trimestre | 4 em 10 | relatório de fornecedor de software | 2026-02 | MÉDIA |

### Exemplos e casos concretos
- **Escritório de arquitetura com 6 pessoas**: padronizou 80% dos orçamentos em template
  automatizado e reduziu o retorno ao cliente de 3 dias para o mesmo dia — fonte: estudo de
  caso publicado pelo fornecedor (viés declarado: material comercial)

### Perguntas frequentes do público
| Pergunta | Onde foi observada |
|---|---|
| "Preciso saber programar pra automatizar orçamento?" | buscas relacionadas + comentários em 2 posts do tema |
| "Quanto custa manter isso rodando por mês?" | comentários recorrentes em posts de concorrentes |

### Dores e desejos relacionados ao tema
- "Faz orçamento manual e repete o mesmo texto 20x por semana" → o assunto endereça
  exatamente esta dor; o dado de 11h/semana quantifica o custo dela
- "Parecer maior do que é" → resposta no mesmo dia é sinal de estrutura

### Limitações da coleta
- Não foi encontrado dado brasileiro específico para o setor; os números são internacionais
  e isso precisa ser dito no conteúdo se forem usados.
```

## Quality Criteria

- [ ] Mínimo de 3 buscas com ângulos diferentes
- [ ] Todo dado com número, fonte e data
- [ ] Fontes principais abertas com `web_fetch`
- [ ] Mínimo de 3 dados com confiança ALTA ou MÉDIA
- [ ] Perguntas frequentes com indicação de onde foram observadas
- [ ] Conexão explícita entre o assunto e ao menos uma dor do perfil
- [ ] Limitações declaradas

## Veto Conditions

Rejeitar e refazer se:
1. Algum dado está sem número, sem fonte ou sem data
2. Alguma pergunta frequente foi suposta em vez de observada
3. Nenhum dado tem confiança ALTA ou MÉDIA
4. Foi proposto ângulo ou gancho — isso é das Fases 3.2 e 3.3
