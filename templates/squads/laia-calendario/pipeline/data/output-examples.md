# Output Examples — Calendário Editorial LAIA

Exemplos completos das saídas finais do squad. Referência de qualidade, nunca gabarito.

---

## Exemplo 1 — Calendário mensal completo (18 itens, meta `leads`)

```markdown
# Calendário Editorial — laia · 2026-08

**Total:** 18 itens · **Topo:** 6 (33%) · **Meio:** 6 (33%) · **Fundo:** 6 (34%)
**Ajuste aplicado:** meta principal `leads` — deslocados 5 p.p. de topo para fundo
(padrão 40/35/25 → efetivo 33/33/34), dentro da tolerância.

| # | Data | Assunto | Etapa | Formato | Plataforma | Asset? | Justificativa |
|---|---|---|---|---|---|---|---|
| 1 | 03/08 | O orçamento que você reescreve 20 vezes por semana | topo | carrossel | IG | não | Lacuna editorial: 0 de 4 concorrentes cobriram essa dor no período |
| 2 | 05/08 | Por que sua IA parou no ChatGPT e não virou processo | meio | post | LI | não | Dor "testou IA e parou no ChatGPT", coberta superficialmente por 1 de 4 |
| 3 | 07/08 | Como o cliente X saiu de 2 dias para 4 minutos no retorno | fundo | carrossel | IG | sim | Meta leads; carrossel com print real foi o melhor de julho (11,2%) — promove Implantação |
| 4 | 10/08 | Três tarefas da sua rotina que já dá pra automatizar | topo | carrossel | IG | não | Tendência ALTA 07/2026: PMEs adotando agentes antes de CRM |
| 5 | 12/08 | O custo real de implantar IA numa empresa de 5 pessoas | meio | carrossel | IG | não | Assunto em alta (MÉDIA, 07/2026) ligado à dor de investimento |
| 6 | 14/08 | Fechou o semestre sem saber quanto a operação custou? | fundo | post | LI | não | Gancho sazonal 15/08 (fechamento contábil PME) — promove Mentoria |
| 7 | 17/08 | O que muda quando o primeiro retorno sai em 4 minutos | topo | carrossel | IG | não | Dor "perde lead por demora"; ângulo distinto do item 3 (educativo, não case) |
| 8 | 19/08 | Bastidor: como eu mapeio o processo de um cliente novo | meio | carrossel | IG | não | Objetivo autoridade acessível de `percepcao_desejada` |
```

**Leitura:** os itens 3 e 7 tocam a mesma dor com etapas, ângulos e formatos diferentes —
permitido e declarado na justificativa. Nenhum item usa o tema saturado "IA vai substituir
empregos".

---

## Exemplo 2 — Planilha de controle correspondente

```csv
n,data,assunto,etapa,formato,plataforma,oferta_promovida,depende_de_asset,justificativa,status,data_postagem,alcance,impressoes,curtidas,comentarios,salvamentos,compartilhamentos,cliques_link,seguidores_ganhos,observacoes
1,2026-08-03,"O orçamento que você reescreve 20 vezes por semana",topo,carrossel,Instagram,,false,"Lacuna editorial: 0 de 4 concorrentes cobriram essa dor no período",planejado,,,,,,,,,,
2,2026-08-05,"Por que sua IA parou no ChatGPT e não virou processo",meio,post-linkedin,LinkedIn,,false,"Dor ""testou IA e parou no ChatGPT"", coberta superficialmente por 1 de 4",planejado,,,,,,,,,,
3,2026-08-07,"Como o cliente X saiu de 2 dias para 4 minutos no retorno",fundo,carrossel,Instagram,"Implantação de agentes de IA",true,"Meta leads; carrossel com print real foi o melhor de julho (11,2%)",planejado,,,,,,,,,,
```

**Pontos de atenção no exemplo:** aspas internas duplicadas na linha 2; vírgula decimal
protegida por aspas externas na linha 3; todas as colunas de métrica vazias.

---

## Exemplo 3 — Planilha do mês seguinte, já preenchida pelo usuário

É assim que o arquivo chega ao Tiago Tendência no ciclo seguinte:

```csv
n,data,assunto,...,status,data_postagem,alcance,impressoes,curtidas,comentarios,salvamentos,compartilhamentos,cliques_link,seguidores_ganhos,observacoes
1,2026-07-02,"5 sinais de que seu atendimento está travando vendas",...,postado,2026-07-02,4820,6110,312,28,96,14,,37,"Melhor carrossel do mês"
2,2026-07-04,"O que é um agente de IA, na prática",...,postado,2026-07-04,2140,2580,88,4,19,2,,6,
3,2026-07-08,"Case: 40h/mês devolvidas para o dono",...,postado,2026-07-09,3960,4870,254,31,140,22,18,29,"Postado 1 dia atrasado"
7,2026-07-16,"Post sobre futuro do trabalho",...,postado,2026-07-16,,,41,1,3,0,,,"Alcance não anotado"
9,2026-07-22,"Carrossel conceitual sobre automação",...,pronto,,,,,,,,,,"Não postado — sem espaço no feed"
```

**Como o feedback brief lê esta planilha:**
- Linhas 1, 2 e 3 são comparáveis → entram nos rankings
- Linha 7 tem alcance vazio → **não comparável**, fica fora do cálculo de engajamento, mas
  o registro em `observacoes` explica por quê
- Linha 9 tem status `pronto` → não postada, fora da análise
- Nenhuma célula vazia é convertida em zero

Engajamento da linha 1: `(312 + 28 + 96 + 14) / 4820 = 9,4%`
Engajamento da linha 3: `(254 + 31 + 140 + 22) / 3960 = 11,3%`

**Aprendizado derivado:** carrossel com case real (11,3%) supera carrossel conceitual — e a
linha 9, um carrossel conceitual, nem chegou a ser postada. Confiança MÉDIA: 3 linhas
comparáveis.

---

## Exemplo 4 — Relatório de revisão que reprova

```markdown
# VEREDITO: REPROVADO

**Bloqueadores:** 2 · **Ressalvas:** 1 · **Ciclo:** 1 de 2

## Distribuição
| Etapa | Itens | % efetivo | % meta | Situação |
|---|---|---|---|---|
| Topo | 10 | 56% | 40% (±5) | fora da faixa |
| Meio | 5 | 28% | 35% (±5) | dentro |
| Fundo | 3 | 17% | 25% (±5) | fora da faixa |

## Bloqueadores
### Distribuição de funil fora da faixa
**Problema:** topo em 56% (teto 45%) e fundo em 17% (piso 20%). A meta do perfil é `leads`,
que pediria deslocamento **para** fundo, não o contrário.
**Correção esperada:** converter 3 itens de topo em fundo → 7/5/6 (39/28/33).

### Item 11 — 19/08 — "Dicas de produtividade com IA"
**Problema:** justificativa circular e assunto genérico.
**Correção esperada:** substituir por dor não coberta, ou reescrever a justificativa
citando o achado que sustenta o tema.
```

**Leitura:** reprovação é o processo funcionando. Corrigir aqui custa uma resposta; corrigir
depois de produzir custa 18 conteúdos.
