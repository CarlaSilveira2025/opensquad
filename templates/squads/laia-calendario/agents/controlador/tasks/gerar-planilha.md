---
task: "Gerar Planilha"
order: 1
input: |
  - calendario: output/calendario.yaml (aprovado no checkpoint 06)
  - briefing_mes: output/briefing-mes.md (cliente e mês de referência)
output: |
  - controle: planilha de controle em CSV (output/controle.csv)
---

# Gerar Planilha

Converte o calendário aprovado na planilha de controle do mês: uma linha por conteúdo,
colunas de acompanhamento e colunas de métricas vazias para preenchimento manual. É esta
planilha que o Tiago Tendência vai ler no mês seguinte para fechar o feedback loop.

## Process

1. **Escrever o cabeçalho canônico**, exatamente nesta ordem e grafia — ele é contrato entre
   meses e não muda sem incremento de versão:

   `n,data,assunto,etapa,formato,plataforma,oferta_promovida,depende_de_asset,justificativa,status,data_postagem,alcance,impressoes,curtidas,comentarios,salvamentos,compartilhamentos,cliques_link,seguidores_ganhos,observacoes`

2. **Gerar uma linha por item do calendário**, na ordem de `n`. Dois conteúdos no mesmo dia
   em plataformas diferentes são duas linhas independentes.

3. **Escapar todo campo de texto livre.** `assunto`, `justificativa` e `observacoes` quase
   sempre contêm vírgula: envolver em aspas duplas e duplicar aspas internas. Remover quebras
   de linha da justificativa, substituindo por espaço.

4. **Preencher `status` com `planejado`** em todas as linhas.

5. **Deixar as colunas de métrica e `data_postagem` completamente vazias.** Nunca `0`, nunca
   `-`, nunca `n/a`. Vazio significa "não medido"; qualquer outro valor corrompe a análise
   do mês seguinte.

6. **Verificar a integridade do CSV**: contar que toda linha tem exatamente 20 campos após o
   parse. Uma linha com número diferente indica escape incorreto.

## Output Format

```csv
n,data,assunto,etapa,formato,plataforma,oferta_promovida,depende_de_asset,justificativa,status,data_postagem,alcance,impressoes,curtidas,comentarios,salvamentos,compartilhamentos,cliques_link,seguidores_ganhos,observacoes
1,2026-08-03,"Assunto do item",topo,carrossel,Instagram,,false,"Justificativa rastreável",planejado,,,,,,,,,,
```

## Output Example

> Referência de qualidade, não gabarito.

```csv
n,data,assunto,etapa,formato,plataforma,oferta_promovida,depende_de_asset,justificativa,status,data_postagem,alcance,impressoes,curtidas,comentarios,salvamentos,compartilhamentos,cliques_link,seguidores_ganhos,observacoes
1,2026-08-03,"O orçamento que você reescreve 20 vezes por semana",topo,carrossel,Instagram,,false,"Lacuna editorial: 0 de 4 concorrentes abordaram a dor de orçamento manual no período",planejado,,,,,,,,,,
2,2026-08-05,"Por que sua IA parou no ChatGPT e não virou processo",meio,post-linkedin,LinkedIn,,false,"Dor ""testou IA e parou no ChatGPT"" com cobertura superficial por 1 de 4 concorrentes",planejado,,,,,,,,,,
3,2026-08-07,"Como o cliente X passou de 2 dias para 4 minutos no primeiro retorno",fundo,carrossel,Instagram,"Implantação de agentes de IA",true,"Meta leads; carrossel com print real teve melhor desempenho de julho (11,2%)",planejado,,,,,,,,,,
4,2026-08-10,"Três tarefas da sua rotina que já dá para automatizar hoje",topo,carrossel,Instagram,,false,"Tendência confiança ALTA de 2026-07: PMEs adotando agentes antes de CRM",planejado,,,,,,,,,,
```

Observe a linha 2: a justificativa contém aspas internas, duplicadas corretamente
(`""testou IA e parou no ChatGPT""`). A linha 3 contém vírgula dentro do campo
(`11,2%`), protegida pelas aspas externas.

## Quality Criteria

- [ ] Cabeçalho idêntico ao canônico, na ordem exata
- [ ] Uma linha por item do calendário, sem omissão
- [ ] Todo campo com vírgula ou aspas devidamente escapado
- [ ] Toda linha tem exatamente 20 campos após o parse
- [ ] `status` = `planejado` em todas as linhas
- [ ] Colunas de métrica e `data_postagem` completamente vazias
- [ ] Nenhuma quebra de linha dentro de célula

## Veto Conditions

Rejeitar e refazer se:
1. Alguma coluna de métrica foi preenchida com `0`, `-` ou `n/a`
2. Alguma linha tem número de campos diferente de 20
3. O cabeçalho difere do canônico em nome ou ordem
4. Algum campo com vírgula ficou sem aspas
