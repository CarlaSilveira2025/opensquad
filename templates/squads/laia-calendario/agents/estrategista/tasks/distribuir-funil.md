---
task: "Distribuir Funil"
order: 1
input: |
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (frequência, plataformas, meta)
  - briefing_mes: output/briefing-mes.md (mês de referência)
  - pesquisa: output/pesquisa-mensal.md (performance, contexto, concorrência)
output: |
  - grade: grade de slots do mês com etapa de funil, formato e plataforma definidos
---

# Distribuir Funil

Define a estrutura do mês **antes** de escolher qualquer tema: quantos conteúdos, em que
dias, de qual etapa de funil, em qual formato e plataforma. Fechar a grade primeiro é o que
impede o calendário de virar 80% topo por inércia.

## Process

1. **Calcular o volume do mês.** `frequencia semanal × número de semanas do mês`, limitado à
   faixa de 16 a 20 itens. Se a frequência do perfil produzir número fora da faixa, ajustar
   para o limite mais próximo e registrar a razão.

2. **Calcular a distribuição alvo:** topo 40%, meio 35%, fundo 25%, arredondando para inteiro
   e ajustando o resto no topo. Para 18 itens: 7 topo, 6 meio, 5 fundo.

3. **Ajustar pela meta principal do perfil**, dentro da tolerância de ±5 pontos:
   - meta `vendas` ou `leads` → desloca até 5 pontos de topo para fundo
   - meta `autoridade` ou `seguidores` → desloca até 5 pontos de fundo para topo
   - meta `engajamento` → mantém a distribuição padrão
   Registrar o ajuste aplicado e o motivo.

4. **Distribuir os slots pelos dias úteis do mês**, evitando concentração: nenhuma semana
   pode ter mais de 2 itens de fundo, e nenhum par de itens de fundo em dias consecutivos.

5. **Atribuir formato e plataforma por slot**, variando dentro de cada etapa e respeitando
   `objetivos.plataformas` do perfil. Priorizar os formatos que o feedback brief apontou como
   de melhor desempenho.

6. **Marcar os slots que dependem de asset do cliente** (depoimento, case, foto), para que a
   Estrategista sinalize na montagem.

## Output Format

```yaml
mes_referencia: "YYYY-MM"
total_itens: 18
distribuicao_alvo:
  topo: { itens: 7, percentual: 39 }
  meio: { itens: 6, percentual: 33 }
  fundo: { itens: 5, percentual: 28 }
ajuste_aplicado: "descrição do desvio e motivo, ou 'nenhum'"
slots:
  - n: 1
    data: "YYYY-MM-DD"
    etapa: "topo|meio|fundo"
    formato: "carrossel|post-linkedin"
    plataforma: "Instagram|LinkedIn"
    depende_de_asset: false
```

## Output Example

> Referência de qualidade, não gabarito.

```yaml
mes_referencia: "2026-08"
total_itens: 18
distribuicao_alvo:
  topo: { itens: 6, percentual: 33 }
  meio: { itens: 6, percentual: 33 }
  fundo: { itens: 6, percentual: 34 }
ajuste_aplicado: >
  Meta principal do perfil é 'leads'. Deslocados 5 pontos de topo para fundo
  (padrão 40/35/25 → efetivo 33/33/34). Dentro da tolerância de ±5 pontos.
slots:
  - n: 1
    data: "2026-08-03"
    etapa: "topo"
    formato: "carrossel"
    plataforma: "Instagram"
    depende_de_asset: false
  - n: 2
    data: "2026-08-05"
    etapa: "meio"
    formato: "post-linkedin"
    plataforma: "LinkedIn"
    depende_de_asset: false
  - n: 3
    data: "2026-08-07"
    etapa: "fundo"
    formato: "carrossel"
    plataforma: "Instagram"
    depende_de_asset: true   # depoimento de cliente
  - n: 4
    data: "2026-08-10"
    etapa: "topo"
    formato: "carrossel"
    plataforma: "Instagram"
    depende_de_asset: false
```

## Quality Criteria

- [ ] Total entre 16 e 20 itens, coerente com a frequência do perfil
- [ ] Distribuição dentro de 40/35/25 com tolerância de ±5 pontos
- [ ] Qualquer desvio tem motivo registrado e ligado à meta principal
- [ ] Nenhuma semana com mais de 2 itens de fundo
- [ ] Nenhum par de itens de fundo em dias consecutivos
- [ ] Todas as plataformas usadas existem em `objetivos.plataformas`
- [ ] Formatos de melhor desempenho no feedback brief priorizados

## Veto Conditions

Rejeitar e refazer se:
1. A distribuição efetiva está fora da faixa de tolerância sem justificativa registrada
2. Existe slot em plataforma que o cliente não tem ativa
3. Todos os itens de fundo estão concentrados em uma única semana
4. O total de itens está fora da faixa de 16 a 20
