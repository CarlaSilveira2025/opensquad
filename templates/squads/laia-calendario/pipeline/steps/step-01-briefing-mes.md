---
step: "01"
name: "Briefing do Mês"
type: checkpoint
outputFile: squads/laia-calendario/output/briefing-mes.md
---

# 🛑 Checkpoint: Briefing do Mês

## Para o Pipeline Runner

Este checkpoint cumpre o papel do **Research Focus Checkpoint**: o Tiago Tendência roda como
subagente e não pode perguntar nada, então tudo que a pesquisa precisa é definido aqui.

Antes de perguntar, listar os clientes disponíveis lendo os diretórios de
`_opensquad/_memory/clientes/`. Se nenhum existir, informar que é preciso rodar
`/opensquad run laia-perfil` antes e encerrar o pipeline.

## Formato de Apresentação ao Usuário

```
🗓️ LAIA — Calendário Editorial

Clientes disponíveis: {lista de slugs}

1. Para qual cliente é este calendário?
2. Mês de referência (formato AAAA-MM, ex.: 2026-09)
3. Tem algum foco estratégico para o mês?
   Ex.: "lançamento da mentoria", "aquecer para a Black Friday", "sem foco especial"
4. Quer que eu analise algum concorrente específico?
   Me passa até 5 @ ou URLs. Se não passar, uso as referências do perfil.
```

## Ação do Pipeline Runner após Resposta

1. Confirmar que `_opensquad/_memory/clientes/{slug}/perfil.json` existe. Se não existir,
   informar e encerrar — o calendário não roda sem perfil.
2. Ler o perfil e conferir se há pendências de criticidade `CRITICA`. Se houver, avisar em
   uma linha quais são e perguntar se o usuário quer seguir mesmo assim.
3. Derivar o mês anterior a partir do mês de referência, para a análise de performance.
4. Escrever em `squads/laia-calendario/output/briefing-mes.md`:

```markdown
# Briefing do Mês

**Cliente:** {slug}
**Mês de referência:** {YYYY-MM}
**Mês anterior (performance):** {YYYY-MM}
**Janela de pesquisa:** {primeiro e último dia do mês anterior}
**Foco estratégico:** {texto do usuário, ou "sem foco especial"}
**Concorrentes a analisar:** {lista informada, ou "usar referências do perfil"}
**Pendências críticas do perfil:** {lista, ou "nenhuma"}
**Data:** {YYYY-MM-DD}
```

5. Avançar para o Step 02 (Pesquisa Mensal).

## Opções Especiais

- **Mês já publicado** → se `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/` já
  existir, avisar e perguntar se é para refazer. Em caso afirmativo, registrar como
  republicação; as métricas já preenchidas serão preservadas no Step 07.
- **Primeiro mês do cliente** → registrar que não há mês anterior; a análise de performance
  vai reportar "sem dados" e o calendário roda em modo exploratório.
