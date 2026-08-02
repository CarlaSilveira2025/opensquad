---
task: "Analisar Concorrentes"
order: 3
input: |
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (nicho, referências, plataformas)
  - briefing_mes: output/briefing-mes.md (concorrentes indicados pelo usuário, se houver)
  - secao_contexto: saída da task anterior (para cruzar saturação)
output: |
  - pesquisa_mensal: relatório mensal consolidado (output/pesquisa-mensal.md)
---

# Analisar Concorrentes

Mapeia o que perfis concorrentes e de referência publicaram no período, para achar lacuna
temática e confirmar saturação. Fecha o relatório mensal consolidando as três frentes.

## Process

1. **Montar a lista de perfis a analisar.** Usar os concorrentes citados no briefing do mês
   e as `comunicacao.referencias` do perfil. Limitar a 5 perfis — mais que isso gera volume
   sem ganho de sinal.

2. **Coletar os posts do período.** Preferir `apify` para extração estruturada de Instagram e
   LinkedIn. Se a skill não estiver disponível ou a extração falhar, usar `web_fetch` nas
   páginas públicas e registrar no relatório que a coleta foi parcial — nunca simular dados
   de post.

3. **Classificar cada post coletado** por tema, formato e etapa de funil aparente. Registrar
   as métricas públicas visíveis (curtidas, comentários) quando existirem.

4. **Identificar padrões de repetição.** Tema presente em 3 ou mais perfis no período é
   confirmado como saturado e cruzado com a seção de saturação da task anterior.

5. **Identificar lacunas.** Dores do perfil do cliente que nenhum concorrente endereçou no
   período — é onde há espaço editorial. Esta é a saída de maior valor da task.

6. **Consolidar o relatório mensal** unindo as três frentes (performance, contexto,
   concorrência) em `output/pesquisa-mensal.md`, na ordem em que a Estrategista vai usá-las.

## Output Format

```markdown
# Pesquisa Mensal — {cliente} · {mês de referência}

**Período pesquisado:** {janela} · **Perfis analisados:** {N} · **Posts coletados:** {N}
**Método de coleta:** apify | web_fetch (parcial)

## 1. Performance do mês anterior
{seção da task analisar-performance, ou "sem dados de performance"}

## 2. Contexto do nicho
{seção da task pesquisar-contexto}

## 3. Concorrência

### Perfis analisados
| Perfil | Posts no período | Formato dominante | Tema dominante |

### Temas saturados confirmados
| Tema | Nº de perfis que publicaram | Cruzamento com seção 2 |

### Lacunas editoriais
| Dor do público sem cobertura | Nenhum concorrente abordou | Oportunidade |

### Limitações desta coleta
- {o que não foi possível coletar e por quê}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Pesquisa Mensal — laia · 2026-08

**Período pesquisado:** 01/07 a 31/07 · **Perfis analisados:** 4 · **Posts coletados:** 63
**Método de coleta:** apify (Instagram) + web_fetch parcial (LinkedIn)

## 3. Concorrência

### Perfis analisados
| Perfil | Posts no período | Formato dominante | Tema dominante |
|---|---|---|---|
| @concorrente-a | 22 | Reels | Ferramentas de IA |
| @concorrente-b | 18 | Carrossel | Futuro do trabalho |
| @concorrente-c | 15 | Carrossel | Prompts prontos |
| @referencia-d | 8 | Post longo | Casos de implantação |

### Temas saturados confirmados
| Tema | Nº de perfis que publicaram | Cruzamento com seção 2 |
|---|---|---|
| "IA vai substituir empregos" | 3 de 4 | confirma a saturação apontada na seção 2 |
| Listas de prompts prontos | 3 de 4 | novo — não havia aparecido na seção 2 |

### Lacunas editoriais
| Dor do público sem cobertura | Nenhum concorrente abordou | Oportunidade |
|---|---|---|
| "Faz orçamento manual e repete o mesmo texto 20x por semana" | 0 de 4 perfis | espaço claro: caso concreto de automação de tarefa repetitiva de rotina |
| "Testou IA e parou no ChatGPT" | 1 de 4, superficialmente | espaço para conteúdo de meio de funil sobre passar da ferramenta ao processo |

### Limitações desta coleta
- LinkedIn: coleta parcial via web_fetch; métricas de alcance não são públicas, então só
  curtidas e comentários foram registrados.
- @concorrente-e citado no briefing não foi analisado: perfil privado.
```

## Quality Criteria

- [ ] Máximo de 5 perfis analisados
- [ ] Método de coleta declarado, incluindo quando foi parcial
- [ ] Nenhum dado de post simulado ou estimado
- [ ] Saturação confirmada por presença em 3 ou mais perfis
- [ ] Lacunas mapeadas contra as dores do perfil do cliente
- [ ] Relatório final consolida as três frentes na ordem definida
- [ ] Limitações da coleta declaradas

## Veto Conditions

Rejeitar e refazer se:
1. Existe métrica ou post que não foi efetivamente coletado
2. O relatório final não contém as três seções
3. Perfil inacessível foi omitido em vez de declarado nas limitações
4. Alguma pauta foi recomendada — a decisão editorial é da Estrategista
