---
step: "04"
name: "Montagem do Calendário"
type: agent
execution: inline
agent: estrategista
tasks:
  - distribuir-funil
  - montar-calendario
depends_on: step-03
inputFile: squads/laia-calendario/output/pesquisa-mensal.md
outputFile: squads/laia-calendario/output/calendario.yaml
---

# Step 04: Estela Estratégia — Montagem do Calendário

## Context Loading

Carregar antes de executar:

- `_opensquad/_memory/clientes/{slug}/perfil.json` — dores, ofertas, meta, plataformas,
  frequência
- `squads/laia-calendario/output/pesquisa-mensal.md` — as três frentes de pesquisa
- `squads/laia-calendario/output/feedback-brief.md` — performance detalhada do mês anterior
- `squads/laia-calendario/output/ajustes-pesquisa.md` — prioridades e descartes do usuário
- `squads/laia-calendario/output/briefing-mes.md` — mês de referência e foco estratégico
- `squads/laia-calendario/pipeline/data/domain-framework.md` — regras de funil e formato
- Em retorno por `on_reject`: `squads/laia-calendario/output/revisao-calendario.md`

## Instructions

### Process

1. **Executar `distribuir-funil` primeiro.** Fechar a grade — volume, distribuição por etapa,
   datas, formatos e plataformas — **antes** de pensar em tema. Aplicar o ajuste pela meta
   principal dentro da tolerância de ±5 pontos e registrar o desvio.

2. **Executar `montar-calendario`.** Preencher os slots na ordem fundo → meio → topo. Fundo
   primeiro porque é o mais restrito: cada item precisa nomear uma oferta específica.

3. **Respeitar as restrições do usuário.** Temas na lista de descarte de
   `ajustes-pesquisa.md` não entram sob nenhuma hipótese. Temas priorizados entram, desde
   que caibam na grade.

4. **Escrever justificativa rastreável para cada item**, citando dor do perfil, achado com
   data ou objetivo declarado. Justificativa que descreve o próprio tema é inválida.

5. **Gerar os dois arquivos**: `calendario.yaml` para o squad de produção e `calendario.md`
   em tabela para leitura humana. Os dois precisam ser consistentes entre si.

6. **Em retorno por `on_reject`**, tratar cada bloqueador da revisão como obrigatório e
   listar no resumo qual correção foi aplicada em cada item apontado.

## Output Format

`calendario.yaml` segue o schema literal da task `montar-calendario`. `calendario.md` segue
este template:

```markdown
# Calendário Editorial — {cliente} · {YYYY-MM}

**Total:** {N} itens · **Topo:** {N} ({%}) · **Meio:** {N} ({%}) · **Fundo:** {N} ({%})
**Ajuste aplicado:** {desvio e motivo, ou "nenhum"}

| # | Data | Assunto | Etapa | Formato | Plataforma | Asset? | Justificativa |
|---|---|---|---|---|---|---|---|
```

## Output Example

```markdown
# Calendário Editorial — laia · 2026-08

**Total:** 18 itens · **Topo:** 6 (33%) · **Meio:** 6 (33%) · **Fundo:** 6 (34%)
**Ajuste aplicado:** meta principal é `leads` — deslocados 5 pontos de topo para fundo
(padrão 40/35/25 → efetivo 33/33/34), dentro da tolerância.

| # | Data | Assunto | Etapa | Formato | Plataforma | Asset? | Justificativa |
|---|---|---|---|---|---|---|---|
| 1 | 03/08 | O orçamento que você reescreve 20 vezes por semana | topo | carrossel | Instagram | não | Lacuna editorial: 0 de 4 concorrentes abordaram essa dor no período |
| 2 | 05/08 | Por que sua IA parou no ChatGPT e não virou processo | meio | post | LinkedIn | não | Dor "testou IA e parou no ChatGPT", coberta superficialmente por 1 de 4 |
| 3 | 07/08 | Como o cliente X passou de 2 dias para 4 minutos no retorno | fundo | carrossel | Instagram | sim | Meta leads; carrossel com print real teve melhor desempenho de julho (11,2%) — promove "Implantação de agentes de IA" |
| 4 | 10/08 | Três tarefas da sua rotina que já dá pra automatizar hoje | topo | carrossel | Instagram | não | Tendência confiança ALTA de 07/2026: PMEs adotando agentes antes de CRM |
| 5 | 12/08 | O que ninguém te conta sobre o custo real de implantar IA | meio | carrossel | Instagram | não | Assunto em alta (confiança MÉDIA, 07/2026) ligado à dor de investimento |
| 6 | 14/08 | Fechou o semestre sem saber quanto a operação custou? | fundo | post | LinkedIn | não | Gancho sazonal 15/08 (fechamento contábil PME) — promove "Mentoria de automação" |
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. A distribuição efetiva está fora de 40/35/25 ±5 pontos sem justificativa registrada
2. Algum item tem justificativa circular, vazia ou que descreve o próprio tema
3. Algum item de fundo não nomeia oferta existente em `identidade.ofertas`
4. Existe assunto repetido dentro do mês
5. Existe item em plataforma fora de `objetivos.plataformas`
6. Algum tema da lista de descarte do usuário foi incluído
7. O total de itens está fora da faixa de 16 a 20

## Quality Criteria

- [ ] Grade fechada antes da escolha de temas
- [ ] Todos os slots preenchidos com assunto específico, não rótulo genérico
- [ ] Toda justificativa cita dor, achado datado ou objetivo
- [ ] Lacunas editoriais da pesquisa aproveitadas com prioridade
- [ ] Temas saturados evitados, ou com ângulo diferenciador declarado
- [ ] Itens dependentes de asset sinalizados
- [ ] Os dois arquivos gerados e consistentes entre si
