---
task: "Publicar Calendário"
order: 2
input: |
  - calendario_yaml: output/calendario.yaml
  - calendario_md: output/calendario.md
  - controle: output/controle.csv
  - briefing_mes: output/briefing-mes.md (slug e mês de referência)
output: |
  - publicacao_report: relatório da publicação (output/publicacao-report.md)
---

# Publicar Calendário

Publica o pacote do mês no registro do cliente, onde o squad `laia-conteudo` vai buscar os
itens a produzir e onde o próximo ciclo de calendário vai buscar a performance.

## Process

1. **Resolver o diretório de destino:**
   `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/`. Cada mês tem diretório
   próprio — nunca sobrescrever o mês anterior.

2. **Verificar se o mês já existe.** Se existir, é republicação: copiar os arquivos atuais
   para `{YYYY-MM}/historico/{arquivo}-{timestamp}` antes de sobrescrever, preservando
   qualquer métrica que o usuário já tenha preenchido.

3. **Proteger métricas já preenchidas.** Se o `controle.csv` de destino já tem células de
   métrica preenchidas, **não** sobrescrever o arquivo cegamente: manter os valores das
   colunas de métrica das linhas cujo `n` e `data` coincidem, e reportar quantas linhas
   foram preservadas.

4. **Escrever os três arquivos** com a ferramenta Write, que cria os diretórios pais
   automaticamente: `calendario.yaml`, `calendario.md` e `controle.csv`. Nunca usar `mkdir`.

5. **Gerar o relatório** com caminhos completos, o que foi preservado, os itens que dependem
   de asset do cliente e as instruções de preenchimento manual.

6. **Indicar o próximo comando** ao usuário.

## Output Format

```markdown
# Publicação do Calendário — {cliente} · {YYYY-MM}

**Itens no calendário:** {N} · **Tipo:** primeira publicação | republicação

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
Depois de publicar cada conteúdo, abrir o `controle.csv` e preencher:
`data_postagem`, `alcance`, `impressoes`, `curtidas`, `comentarios`, `salvamentos`,
`compartilhamentos`, `cliques_link`, `seguidores_ganhos`.
Deixar em branco o que não foi medido — **nunca preencher com zero**.

## Próximo passo
Rodar `/opensquad run laia-conteudo` para produzir o item {n} do calendário.
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Publicação do Calendário — laia · 2026-08

**Itens no calendário:** 18 · **Tipo:** primeira publicação

## Arquivos publicados
- `_opensquad/_memory/clientes/laia/calendario/2026-08/calendario.yaml`
- `_opensquad/_memory/clientes/laia/calendario/2026-08/calendario.md`
- `_opensquad/_memory/clientes/laia/calendario/2026-08/controle.csv`

## Preservação
Não aplicável — primeira publicação deste mês.

## Itens que dependem de asset do cliente
- Item 3 (2026-08-07) — "Como o cliente X passou de 2 dias para 4 minutos" — precisa de:
  autorização do cliente X e print do painel antes/depois
- Item 12 (2026-08-21) — "O que 3 clientes disseram depois de 60 dias" — precisa de:
  depoimentos em texto ou vídeo

## Preenchimento manual (v1)
Depois de publicar cada conteúdo, abrir o `controle.csv` e preencher as colunas de métrica.
Deixar em branco o que não foi medido — **nunca preencher com zero**. Célula vazia é lida
como "não medido"; zero é lido como "desempenho nulo" e distorce o calendário do mês seguinte.

## Próximo passo
Rodar `/opensquad run laia-conteudo` para produzir o item 1 do calendário
("O orçamento que você reescreve 20 vezes por semana", 03/08).
```

## Quality Criteria

- [ ] Diretório do mês próprio, sem sobrescrever meses anteriores
- [ ] Em republicação, métricas já preenchidas preservadas e o total reportado
- [ ] Em republicação, versão anterior arquivada antes da sobrescrita
- [ ] Todos os caminhos escritos listados no relatório
- [ ] Itens dependentes de asset listados com o asset necessário
- [ ] Instrução explícita de nunca preencher métrica com zero
- [ ] Próximo comando indicado

## Veto Conditions

Rejeitar e refazer se:
1. Um mês anterior foi sobrescrito
2. Em republicação, métricas preenchidas pelo usuário foram perdidas
3. Foi usado `mkdir` via Bash em vez da ferramenta Write
4. O relatório omite algum arquivo efetivamente escrito
