---
task: "Analisar Performance"
order: 1
input: |
  - briefing_mes: output/briefing-mes.md (cliente, mês de referência, foco)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json
  - controle_anterior: _opensquad/_memory/clientes/{slug}/calendario/{ano-mes-anterior}/controle.csv
output: |
  - feedback_brief: leitura de performance do mês anterior (output/feedback-brief.md)
---

# Analisar Performance

Lê a planilha de controle do mês anterior e extrai o que a Estrategista precisa saber para
não repetir o que falhou e ampliar o que funcionou. Esta é a perna interna do feedback loop
na versão manual (v1).

## Process

1. **Localizar a planilha do mês anterior** em
   `_opensquad/_memory/clientes/{slug}/calendario/{ano-mes-anterior}/controle.csv`. Se não
   existir, ou existir sem nenhuma métrica preenchida, produzir um brief declarando
   "sem dados de performance" e encerrar a task — nunca estimar números.

2. **Separar as linhas medidas das não medidas.** Só entram na análise linhas com status
   `postado` e ao menos uma coluna de métrica preenchida. Célula vazia é ausência de medição,
   nunca zero.

3. **Calcular a taxa de engajamento por linha**:
   `(curtidas + comentarios + salvamentos + compartilhamentos) / alcance`. Onde `alcance`
   estiver vazio, marcar a linha como não comparável e excluir dos rankings.

4. **Ranquear por três cortes**: por formato, por etapa de funil e por plataforma. Em cada
   corte, registrar média, melhor e pior desempenho, com o número de linhas que sustenta
   cada média.

5. **Marcar a confiança de cada leitura.** `ALTA` com 5 ou mais linhas comparáveis, `MÉDIA`
   com 3 a 4, `BAIXA` com 1 a 2. Leitura de amostra pequena precisa vir rotulada como tal.

6. **Listar os aprendizados acionáveis**, no máximo 5, cada um com o dado que o sustenta.

## Output Format

```markdown
# Feedback Brief — {cliente} · {mês anterior}

**Linhas na planilha:** {N} · **Postadas:** {N} · **Com métrica:** {N}
**Status:** com dados | sem dados de performance

## Desempenho por formato
| Formato | Nº | Engaj. médio | Melhor | Pior | Confiança |

## Desempenho por etapa de funil
| Etapa | Nº | Engaj. médio | Confiança |

## Desempenho por plataforma
| Plataforma | Nº | Engaj. médio | Confiança |

## Aprendizados acionáveis
1. **{aprendizado}** — sustentado por: {dado} (confiança {NÍVEL})

## Não comparável
- {linha e motivo}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Feedback Brief — laia · 2026-07

**Linhas na planilha:** 18 · **Postadas:** 16 · **Com métrica:** 12
**Status:** com dados

## Desempenho por formato
| Formato | Nº | Engaj. médio | Melhor | Pior | Confiança |
|---|---|---|---|---|---|
| Carrossel IG | 7 | 6,8% | 11,2% | 3,1% | ALTA |
| Post LinkedIn | 5 | 4,2% | 7,0% | 1,9% | MÉDIA |

## Desempenho por etapa de funil
| Etapa | Nº | Engaj. médio | Confiança |
|---|---|---|---|
| Topo | 6 | 7,4% | ALTA |
| Meio | 4 | 5,1% | MÉDIA |
| Fundo | 2 | 2,3% | BAIXA |

## Aprendizados acionáveis
1. **Carrossel com print de resultado real supera carrossel conceitual** — os 2 melhores
   (11,2% e 9,8%) mostravam automação rodando; os 2 piores (3,1% e 3,4%) eram explicação
   conceitual (confiança ALTA).
2. **Fundo de funil só teve 2 itens no mês, ambos na última semana** — engajamento de 2,3%
   pode refletir a concentração, não o formato (confiança BAIXA — não usar para cortar
   fundo de funil).

## Não comparável
- Linha 14 (post LinkedIn, 12/07): alcance vazio, engajamento não calculável
- Linhas 17 e 18: status `pronto`, ainda não postadas
```

## Quality Criteria

- [ ] Nenhuma métrica foi estimada ou preenchida com zero
- [ ] Célula vazia tratada como ausência de medição
- [ ] Cada média informa o número de linhas que a sustenta
- [ ] Confiança marcada em todos os cortes
- [ ] Máximo de 5 aprendizados, cada um com dado de sustentação
- [ ] Linhas não comparáveis listadas com motivo

## Veto Conditions

Rejeitar e refazer se:
1. Alguma métrica ausente foi tratada como zero
2. Existe aprendizado sem dado que o sustente
3. Leitura de amostra com 1 ou 2 linhas foi rotulada como confiança ALTA ou MÉDIA
4. A planilha não existia e mesmo assim o brief apresenta números
