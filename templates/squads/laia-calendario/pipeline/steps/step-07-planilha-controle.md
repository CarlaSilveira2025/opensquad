---
step: "07"
name: "Planilha de Controle e Publicação"
type: agent
execution: inline
agent: controlador
tasks:
  - gerar-planilha
  - publicar-calendario
depends_on: step-06
inputFile: squads/laia-calendario/output/calendario.yaml
outputFile: squads/laia-calendario/output/controle.csv
---

# Step 07: Cláudia Controle — Planilha de Controle e Publicação

## Context Loading

Carregar antes de executar:

- `squads/laia-calendario/output/calendario.yaml` — calendário aprovado no checkpoint 06
- `squads/laia-calendario/output/calendario.md` — versão em tabela, publicada junto
- `squads/laia-calendario/output/briefing-mes.md` — slug do cliente e mês de referência
- `squads/laia-calendario/output/revisao-calendario.md` — veredito, para registrar no relatório
- `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/controle.csv` — planilha existente
  do mesmo mês, apenas em caso de republicação
- `squads/laia-calendario/pipeline/data/domain-framework.md` — cabeçalho canônico da planilha

## Instructions

### Process

1. **Executar `gerar-planilha`.** Escrever o cabeçalho canônico de 20 colunas na ordem exata,
   uma linha por item do calendário, com `status` = `planejado` e todas as colunas de métrica
   e `data_postagem` vazias. Escapar todo campo de texto livre que contenha vírgula ou aspas.
   Salvar em `squads/laia-calendario/output/controle.csv`.

2. **Verificar a integridade do CSV.** Toda linha deve ter exatamente 20 campos após o parse.
   Divergência indica escape incorreto e precisa ser corrigida antes de publicar.

3. **Executar `publicar-calendario`.** Resolver o destino
   `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/` e verificar se já existe.

4. **Em republicação, preservar métricas.** Se o `controle.csv` de destino já tem células de
   métrica preenchidas, manter esses valores nas linhas cujo `n` e `data` coincidem, e
   arquivar a versão anterior em `{YYYY-MM}/historico/` antes de sobrescrever. Reportar
   quantas linhas tiveram métricas preservadas.

5. **Escrever os três arquivos** com a ferramenta Write — `calendario.yaml`, `calendario.md`
   e `controle.csv`. Nunca usar `mkdir` via Bash.

6. **Gerar o relatório de publicação** com caminhos completos, o que foi preservado, os itens
   que dependem de asset e as instruções de preenchimento manual. Apresentar ao usuário o
   próximo comando a rodar.

## Output Format

```markdown
# Publicação do Calendário — {cliente} · {YYYY-MM}

**Itens no calendário:** {N} · **Tipo:** primeira publicação | republicação
**Veredito da revisão:** APROVADO | REPROVADO (publicado por decisão do usuário)

## Arquivos publicados
- `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/calendario.yaml`
- `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/calendario.md`
- `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/controle.csv`

## Preservação
- Métricas preservadas em {N} linhas | Não aplicável
- Versão anterior arquivada em: {caminho} | Não aplicável

## Itens que dependem de asset do cliente
- Item {n} ({data}) — {assunto} — precisa de: {asset}

## Preenchimento manual (v1)
{instruções de preenchimento das colunas de métrica}

## Próximo passo
Rodar `/opensquad run laia-conteudo` para produzir o item {n}.
```

## Output Example

```markdown
# Publicação do Calendário — laia · 2026-08

**Itens no calendário:** 18 · **Tipo:** primeira publicação
**Veredito da revisão:** APROVADO (0 bloqueadores, 3 ressalvas)

## Arquivos publicados
- `_opensquad/_memory/clientes/laia/calendario/2026-08/calendario.yaml`
- `_opensquad/_memory/clientes/laia/calendario/2026-08/calendario.md`
- `_opensquad/_memory/clientes/laia/calendario/2026-08/controle.csv`

## Preservação
Não aplicável — primeira publicação deste mês.

## Itens que dependem de asset do cliente
- Item 3 (07/08) — "Como o cliente X passou de 2 dias para 4 minutos" — precisa de:
  autorização do cliente X e print do painel antes/depois
- Item 12 (21/08) — "O que 3 clientes disseram depois de 60 dias" — precisa de:
  depoimentos em texto ou vídeo

Sem esses materiais, os dois itens ficam bloqueados na produção. Vale providenciar antes
das datas.

## Preenchimento manual (v1)
Depois de publicar cada conteúdo, abrir o `controle.csv` e preencher `data_postagem` e as
colunas de métrica: `alcance`, `impressoes`, `curtidas`, `comentarios`, `salvamentos`,
`compartilhamentos`, `cliques_link`, `seguidores_ganhos`.

Deixar em branco o que não foi medido — **nunca preencher com zero**. Célula vazia é lida
como "não medido"; zero é lido como "desempenho nulo" e faz o calendário do mês que vem
evitar um formato que talvez tenha ido bem.

## Próximo passo
Rodar `/opensquad run laia-conteudo` para produzir o item 1
("O orçamento que você reescreve 20 vezes por semana", 03/08).
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Alguma coluna de métrica foi preenchida com `0`, `-` ou `n/a` em vez de vazia
2. Alguma linha do CSV tem número de campos diferente de 20
3. O cabeçalho difere do canônico em nome ou ordem das colunas
4. Um mês anterior foi sobrescrito, ou métricas preenchidas pelo usuário foram perdidas
5. Foi usado `mkdir` via Bash em vez da ferramenta Write

## Quality Criteria

- [ ] CSV com cabeçalho canônico e uma linha por item
- [ ] Campos com vírgula ou aspas escapados corretamente
- [ ] Colunas de métrica vazias e `status` = `planejado`
- [ ] Pacote publicado em diretório próprio do mês
- [ ] Em republicação, métricas preservadas e versão anterior arquivada
- [ ] Relatório com caminhos completos e itens dependentes de asset
- [ ] Instrução explícita de nunca preencher métrica com zero
