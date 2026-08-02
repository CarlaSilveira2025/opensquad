---
step: "02"
name: "Pesquisa Mensal"
type: agent
execution: subagent
model_tier: powerful
agent: pesquisador
tasks:
  - analisar-performance
  - pesquisar-contexto
  - analisar-concorrentes
depends_on: step-01
inputFile: squads/laia-calendario/output/briefing-mes.md
outputFile: squads/laia-calendario/output/pesquisa-mensal.md
---

# Step 02: Tiago Tendência — Pesquisa Mensal

## Context Loading

Carregar antes de executar:

- `squads/laia-calendario/output/briefing-mes.md` — cliente, mês, janela e foco estratégico
- `_opensquad/_memory/clientes/{slug}/perfil.json` — nicho, dores, plataformas, referências
- `_opensquad/_memory/clientes/{slug}/calendario/{mes-anterior}/controle.csv` — planilha do
  mês anterior, se existir
- `squads/laia-calendario/pipeline/data/domain-framework.md` — método de pesquisa mensal
- `squads/laia-calendario/pipeline/data/anti-patterns.md` — erros de pesquisa a evitar

## Instructions

### Process

1. **Executar `analisar-performance`.** Ler a planilha do mês anterior, separar linhas
   medidas de não medidas, calcular taxa de engajamento e ranquear por formato, etapa e
   plataforma. Se não houver planilha ou métricas, declarar "sem dados de performance" e
   seguir — nunca estimar. Salvar em `squads/laia-calendario/output/feedback-brief.md`.

2. **Executar `pesquisar-contexto`.** No mínimo 3 buscas com ângulos diferentes, delimitadas
   à janela do briefing. Confirmar as fontes principais com `web_fetch`. Classificar em
   tendência, assunto em alta e saturado. Listar datas sazonais apenas com conexão concreta
   ao negócio.

3. **Executar `analisar-concorrentes`.** Até 5 perfis, preferindo `apify` para extração
   estruturada. Se a coleta falhar ou for parcial, declarar a limitação — nunca simular
   dados de post. Identificar temas saturados por presença em 3+ perfis e, sobretudo, as
   lacunas: dores do perfil que ninguém está cobrindo.

4. **Consolidar as três frentes** em `squads/laia-calendario/output/pesquisa-mensal.md`, na
   ordem: performance, contexto, concorrência.

5. **Não recomendar pauta.** O relatório descreve cenário; a decisão editorial é do Step 04.

## Output Format

```markdown
# Pesquisa Mensal — {cliente} · {mês de referência}

**Período pesquisado:** {janela} · **Perfis analisados:** {N} · **Posts coletados:** {N}
**Método de coleta:** apify | web_fetch (parcial)

## 1. Performance do mês anterior
{tabelas por formato, etapa e plataforma + aprendizados acionáveis}

## 2. Contexto do nicho
### Tendências
### Assuntos em alta
### Temas saturados (evitar)
### Ganchos sazonais do mês
### Frentes sem achado relevante

## 3. Concorrência
### Perfis analisados
### Temas saturados confirmados
### Lacunas editoriais
### Limitações desta coleta
```

## Output Example

```markdown
# Pesquisa Mensal — laia · 2026-08

**Período pesquisado:** 01/07 a 31/07 · **Perfis analisados:** 4 · **Posts coletados:** 63
**Método de coleta:** apify (Instagram) + web_fetch parcial (LinkedIn)

## 1. Performance do mês anterior
**Linhas na planilha:** 18 · **Postadas:** 16 · **Com métrica:** 12

| Formato | Nº | Engaj. médio | Melhor | Pior | Confiança |
|---|---|---|---|---|---|
| Carrossel IG | 7 | 6,8% | 11,2% | 3,1% | ALTA |
| Post LinkedIn | 5 | 4,2% | 7,0% | 1,9% | MÉDIA |

**Aprendizados acionáveis**
1. Carrossel com print de resultado real supera carrossel conceitual — os 2 melhores
   mostravam automação rodando (confiança ALTA).
2. Fundo de funil teve só 2 itens, ambos na última semana — o baixo engajamento pode
   refletir a concentração, não o formato (confiança BAIXA).

## 2. Contexto do nicho
### Tendências
| Achado | Fonte | Data | Confiança | Conexão com o público |
|---|---|---|---|---|
| PMEs adotando agentes de atendimento antes de CRM | 3 publicações do setor | 2026-07 | ALTA | dor "perde lead por demora" |

### Temas saturados (evitar)
| Tema | Por que | Fonte |
|---|---|---|
| "IA vai substituir empregos" | 6 de 8 perfis no mês | análise de concorrentes |

## 3. Concorrência
### Lacunas editoriais
| Dor sem cobertura | Concorrentes que abordaram | Oportunidade |
|---|---|---|
| "Faz orçamento manual e repete texto 20x/semana" | 0 de 4 | espaço claro para caso concreto |

### Limitações desta coleta
- LinkedIn: métricas de alcance não são públicas; só curtidas e comentários registrados.
- @concorrente-e citado no briefing não analisado: perfil privado.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Alguma métrica do mês anterior foi estimada, ou célula vazia foi tratada como zero
2. Algum achado de contexto está sem fonte, data ou nível de confiança
3. Alguma data sazonal foi listada sem conexão concreta com o negócio
4. Existe dado de post de concorrente que não foi efetivamente coletado
5. O relatório recomenda pauta ou tema de post
6. O relatório não contém as três seções

## Quality Criteria

- [ ] Mínimo de 3 buscas com ângulos diferentes na frente de contexto
- [ ] Máximo de 5 perfis na análise de concorrência
- [ ] Método de coleta declarado, incluindo parcialidade
- [ ] Temas saturados em seção separada dos temas em alta
- [ ] Lacunas editoriais cruzadas com as dores do perfil
- [ ] Frentes sem achado declaradas explicitamente
- [ ] Os dois arquivos de saída gravados
