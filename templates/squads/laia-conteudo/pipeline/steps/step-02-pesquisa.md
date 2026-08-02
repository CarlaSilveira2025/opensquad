---
step: "02"
name: "Pesquisa e Inteligência"
type: agent
execution: subagent
model_tier: powerful
agent: pesquisador
tasks:
  - pesquisar-fontes
  - mapear-saturacao
depends_on: step-01
inputFile: squads/laia-conteudo/output/briefing-item.md
outputFile: squads/laia-conteudo/output/pesquisa.md
---

# Step 02: Pedro Pesquisa — Pesquisa e Inteligência (Fase 3.1)

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/briefing-item.md` — assunto, etapa, formato, plataforma
- `_opensquad/_memory/clientes/{slug}/perfil.json` — nicho, dores, público, referências
- `squads/laia-conteudo/pipeline/data/domain-framework.md` — método de pesquisa da Fase 3.1
- `squads/laia-conteudo/pipeline/data/anti-patterns.md` — erros de pesquisa a evitar

## Instructions

### Process

1. **Executar `pesquisar-fontes`.** Três buscas com ângulos diferentes a partir do assunto e
   das dores do perfil. Abrir as fontes principais com `web_fetch` e confirmar número e
   contexto. Rastrear a fonte primária de todo dado que circula republicado.

2. **Coletar perguntas frequentes reais** — buscas relacionadas, comentários, dúvidas
   recorrentes — registrando onde cada uma foi observada. Nunca supor a dúvida do público.

3. **Selecionar de 3 a 5 dados âncora**, priorizando o específico, o datado e o
   contraintuitivo, e marcar a confiança de cada achado.

4. **Executar `mapear-saturacao`.** Coletar conteúdo recente sobre o assunto preferindo
   `apify`; se a coleta falhar ou for parcial, usar `web_fetch` e declarar a limitação.
   Nunca simular posts.

5. **Classificar os enquadramentos** encontrados e marcar como saturado todo que apareça em
   3 ou mais peças. Registrar exemplo concreto de cada.

6. **Identificar os recortes ausentes** — o que ninguém abordou, cruzado com as dores do
   perfil. É a saída de maior valor do step.

7. **Consolidar em `squads/laia-conteudo/output/pesquisa.md`.** Não propor ângulo nem gancho.

## Output Format

```markdown
# Pesquisa — {assunto}

**Item do calendário:** #{n} · {data} · {etapa} · {formato} · {plataforma}
**Peças analisadas:** {N} · **Método:** apify | web_fetch (parcial)

## 1. Fontes e Dados
### Dados âncora
### Dados de apoio
### Exemplos e casos concretos
### Perguntas frequentes do público
### Dores e desejos relacionados ao tema
### Limitações da coleta

## 2. Panorama do Tema
### Enquadramentos saturados (evitar)
### O que está funcionando
### Recortes não abordados
### Limitações da coleta
```

## Output Example

```markdown
# Pesquisa — O orçamento que você reescreve 20 vezes por semana

**Item do calendário:** #1 · 2026-08-03 · topo · carrossel · Instagram
**Peças analisadas:** 31 · **Método:** apify (Instagram) + web_fetch parcial (LinkedIn)

## 1. Fontes e Dados

### Dados âncora
| Dado | Número | Fonte | Data | Confiança |
|---|---|---|---|---|
| Tempo semanal em tarefas administrativas repetitivas em PME de serviço | 11h | publicação setorial, verificada na origem | 2025-11 | ALTA |
| Empresas que abandonam automação no 1º trimestre | 4 em 10 | relatório de fornecedor | 2026-02 | MÉDIA |

### Perguntas frequentes do público
| Pergunta | Onde foi observada |
|---|---|
| "Preciso saber programar pra automatizar orçamento?" | buscas relacionadas + comentários em 2 posts |
| "Quanto custa manter isso rodando por mês?" | comentários recorrentes em posts de concorrentes |

### Limitações da coleta
- Não há dado brasileiro específico do setor; os números são internacionais e isso precisa
  ser declarado se forem usados no conteúdo.

## 2. Panorama do Tema

### Enquadramentos saturados (evitar)
| Enquadramento | Nº de peças | Exemplo observado |
|---|---|---|
| Lista de ferramentas | 11 de 31 | carrossel de 10 slides, uma ferramenta por slide |
| Alarmista | 7 de 31 | capa grande sem nenhum dado |

### Recortes não abordados
| Recorte ausente | Dor do perfil que ele tocaria |
|---|---|
| O que fazer com os 20% de orçamentos não padronizáveis | endereça a objeção de quem já tentou |
| O custo de manter a automação rodando | é a pergunta frequente #2 e ninguém responde |
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Algum dado está sem número, sem fonte identificável ou sem data
2. Nenhum dado tem confiança ALTA ou MÉDIA
3. Alguma pergunta frequente foi suposta em vez de observada
4. Existe peça ou métrica de concorrente que não foi efetivamente coletada
5. Saturação foi declarada sem contagem de peças
6. O relatório propõe ângulo ou gancho

## Quality Criteria

- [ ] Mínimo de 3 buscas com ângulos diferentes
- [ ] Fontes principais abertas com `web_fetch`
- [ ] De 3 a 5 dados âncora selecionados
- [ ] Perguntas frequentes com origem de observação
- [ ] Enquadramentos saturados com exemplo concreto
- [ ] Recortes ausentes cruzados com dores do perfil
- [ ] Limitações da coleta declaradas nas duas seções
