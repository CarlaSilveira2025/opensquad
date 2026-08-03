---
task: "Mapear Saturação"
order: 2
input: |
  - briefing_item: output/briefing-item.md (assunto)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (referências, plataformas)
  - secao_fontes: saída da task anterior
output: |
  - pesquisa: relatório completo da Fase 3.1 (output/pesquisa.md)
---

# Mapear Saturação

Identifica como o assunto já vem sendo abordado — o que está funcionando e o que já está
exaurido. É o que impede a Fase 3.2 de propor o ângulo que todo mundo já usou.

## Process

1. **Coletar conteúdo recente sobre o assunto** no Instagram e no LinkedIn. Preferir `apify`
   para extração estruturada. Se falhar ou for parcial, usar `web_fetch` e declarar a
   limitação — nunca simular posts.

2. **Classificar as abordagens encontradas** por tipo de enquadramento: alarmista,
   educacional, case, lista, contraintuitivo, motivacional. Contar quantos usam cada um.

3. **Marcar como saturado** todo enquadramento presente em 3 ou mais peças no período.
   Registrar exemplo concreto de cada, para que a Ângela Ângulo reconheça o padrão.

4. **Identificar o que está funcionando.** Entre as peças com engajamento visivelmente acima
   das outras do mesmo perfil, registrar o que têm em comum — estrutura, tipo de abertura,
   formato. Marcar como observação, não como lei.

5. **Identificar o que ninguém abordou.** Recortes do assunto ausentes nas peças coletadas,
   especialmente os que se conectam às dores do perfil. É a saída de maior valor.

6. **Consolidar o relatório final** unindo as duas tasks em `output/pesquisa.md`.

## Output Format

```markdown
# Pesquisa — {assunto}

**Item do calendário:** #{n} · {data} · {etapa} · {formato} · {plataforma}
**Peças analisadas:** {N} · **Método:** apify | web_fetch (parcial)

## 1. Fontes e Dados
{seção da task pesquisar-fontes}

## 2. Panorama do Tema

### Enquadramentos saturados (evitar)
| Enquadramento | Nº de peças | Exemplo observado |

### O que está funcionando
| Padrão observado | Evidência | Ressalva |

### Recortes não abordados
| Recorte ausente | Dor do perfil que ele tocaria |

### Limitações da coleta
- {o que não pôde ser coletado}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Pesquisa — O orçamento que você reescreve 20 vezes por semana

**Item do calendário:** #1 · 2026-08-03 · topo · carrossel · Instagram
**Peças analisadas:** 31 · **Método:** apify (Instagram) + web_fetch parcial (LinkedIn)

## 2. Panorama do Tema

### Enquadramentos saturados (evitar)
| Enquadramento | Nº de peças | Exemplo observado |
|---|---|---|
| Lista de ferramentas ("10 IAs para automatizar") | 11 de 31 | carrossel de 10 slides, uma ferramenta por slide, sem contexto de uso |
| Alarmista ("automatize ou fique pra trás") | 7 de 31 | capa com texto grande e nenhum dado |

### O que está funcionando
| Padrão observado | Evidência | Ressalva |
|---|---|---|
| Peças que abrem com número de horas perdidas | as 3 de maior engajamento aparente do conjunto | métricas públicas parciais; observação, não conclusão estatística |
| Case com antes/depois concreto | 2 peças com comentários pedindo detalhe | amostra pequena |

### Recortes não abordados
| Recorte ausente | Dor do perfil que ele tocaria |
|---|---|
| O que fazer com os 20% de orçamentos que NÃO dá pra padronizar | "faz orçamento manual e repete o mesmo texto 20x por semana" — endereça a objeção real de quem já tentou |
| O custo de manter a automação rodando | "testou IA e parou no ChatGPT" — é a pergunta frequente #2 e ninguém responde |

### Limitações da coleta
- LinkedIn: coleta parcial, sem métricas de alcance públicas
- 4 perfis relevantes do nicho são privados e ficaram fora
```

## Quality Criteria

- [ ] Método de coleta declarado, incluindo parcialidade
- [ ] Nenhum post simulado ou estimado
- [ ] Saturação definida por contagem (3+ peças), não por impressão
- [ ] Cada enquadramento saturado com exemplo concreto observado
- [ ] Observações de performance marcadas com ressalva de amostra
- [ ] Recortes ausentes cruzados com dores do perfil
- [ ] Relatório final contém as duas seções

## Veto Conditions

Rejeitar e refazer se:
1. Existe peça ou métrica que não foi efetivamente coletada
2. Saturação foi declarada sem contagem
3. Observação de performance foi apresentada como conclusão sem ressalva
4. Foi proposto ângulo ou gancho
