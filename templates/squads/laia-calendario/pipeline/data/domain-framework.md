# Domain Framework — Calendário Editorial LAIA

Framework operacional das Fases 2.1 (calendário) e 2.2 (controle).

---

## 1. Distribuição de funil

| Etapa | Meta | Tolerância | Função | Formatos típicos |
|---|---|---|---|---|
| **Topo** | 40% | ±5 p.p. | Atração — alcançar quem ainda não conhece | educativo, curiosidade, tendência |
| **Meio** | 35% | ±5 p.p. | Consideração — construir confiança | bastidor, autoridade, case, prova social |
| **Fundo** | 25% | ±5 p.p. | Conversão — pedir a ação | oferta, CTA direto, depoimento, lançamento |

### Ajuste pela meta principal do perfil

| `objetivos.meta_principal` | Ajuste permitido |
|---|---|
| `vendas` · `leads` | desloca até 5 p.p. de topo → fundo |
| `autoridade` · `seguidores` | desloca até 5 p.p. de fundo → topo |
| `engajamento` | mantém 40/35/25 |

Todo ajuste é registrado no campo `ajuste_aplicado`, com o motivo ligado à meta.

---

## 2. Volume do mês

```
volume = frequencia_semanal × semanas_do_mes,  limitado à faixa [16, 20]
```

Fora da faixa, ajustar para o limite mais próximo e registrar a razão. A faixa vem do
escopo do sistema (~16-20 conteúdos/mês) e representa o que um cliente pequeno sustenta.

---

## 3. Regras de cadência

- Máximo **2 itens de fundo por semana**
- Nunca **dois itens de fundo em dias consecutivos**
- Variedade de formato dentro de cada etapa
- Nenhum assunto repetido no mês; assuntos próximos exigem ângulo **e** formato distintos
- Nenhuma plataforma fora de `objetivos.plataformas` do perfil

---

## 4. Fontes de tema, em ordem de prioridade

1. **Lacunas editoriais** — dor do perfil que nenhum concorrente cobriu. Maior valor.
2. **Dores do perfil** ainda não endereçadas no mês.
3. **Tendências** com confiança ALTA ou MÉDIA e data dentro da janela.
4. **Ganchos sazonais** com conexão concreta ao negócio.
5. **Formatos vencedores** apontados pelo feedback brief.

**Nunca:** tema saturado sem ângulo diferenciador declarado; tema da lista de descarte do
usuário; rótulo genérico ("dica do dia", "conteúdo educativo").

---

## 5. Anatomia do item de calendário

| Campo | Obrigatório | Observação |
|---|---|---|
| `n` | sim | número sequencial |
| `data` | sim | `YYYY-MM-DD` |
| `assunto` | sim | tema específico, nunca rótulo |
| `etapa` | sim | `topo` · `meio` · `fundo` |
| `formato` | sim | `carrossel` · `post-linkedin` |
| `plataforma` | sim | dentro de `objetivos.plataformas` |
| `oferta_promovida` | só em fundo | precisa existir em `identidade.ofertas` |
| `depende_de_asset` | sim | `true` para depoimento, case, foto |
| `justificativa` | sim | cita dor, achado datado ou objetivo |
| `status` | sim | inicia em `planejado` |

### Teste de justificativa rastreável

- ✅ "Lacuna editorial: 0 de 4 concorrentes abordaram a dor X no período"
- ✅ "Tendência confiança ALTA de 07/2026: PMEs adotando agentes antes de CRM"
- ✅ "Meta `leads`; carrossel com print real teve melhor desempenho de julho (11,2%)"
- ❌ "Conteúdo educativo sobre precificação porque precificação é importante" (circular)
- ❌ "Para engajar o público" (vazia)

---

## 6. Cabeçalho canônico da planilha de controle (Fase 2.2)

Contrato entre meses — não muda sem incremento de versão:

```
n,data,assunto,etapa,formato,plataforma,oferta_promovida,depende_de_asset,justificativa,
status,data_postagem,alcance,impressoes,curtidas,comentarios,salvamentos,
compartilhamentos,cliques_link,seguidores_ganhos,observacoes
```

20 colunas. Valores fechados de `status`: `planejado` · `em producao` · `pronto` · `postado`.

**Regra crítica:** colunas de métrica nascem **vazias**. Vazio = não medido. Zero = medido e
deu zero. Confundir os dois corrompe o feedback loop do mês seguinte.

---

## 7. Feedback loop (v1 — manual)

```
Mês N:   calendário → produção → publicação → usuário preenche métricas no CSV
Mês N+1: Tiago Tendência lê o CSV do mês N → feedback-brief → Estela usa na montagem
```

Cálculo de engajamento: `(curtidas + comentarios + salvamentos + compartilhamentos) / alcance`.
Linha sem `alcance` é marcada como não comparável e fica fora dos rankings.

Confiança da leitura: `ALTA` ≥ 5 linhas comparáveis · `MÉDIA` 3-4 · `BAIXA` 1-2.

**V2 (futuro):** as mesmas colunas preenchidas automaticamente via API Meta/LinkedIn. O
cabeçalho não muda — é por isso que ele é contrato.

---

## 8. Estrutura publicada no registro do cliente

```
_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/
├── calendario.yaml    ← lido pelo squad laia-conteudo
├── calendario.md      ← leitura humana
├── controle.csv       ← planilha de acompanhamento e métricas
└── historico/         ← versões anteriores em caso de republicação
```

Um diretório por mês. Nunca sobrescrever mês anterior — o histórico é o insumo do feedback loop.
