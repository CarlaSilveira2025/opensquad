# Research Brief — Calendário Editorial LAIA

## Origem deste brief

Squad construído diretamente a partir do documento **"Sistema de Produção de Conteúdo com
IA — LAIA, Escopo Operacional Final (v3)"**, e não pelo fluxo padrão de pesquisa do
Architect. Nenhuma estatística de mercado é citada aqui porque nenhuma foi coletada —
inventar fonte seria pior que não ter fonte.

---

## 1. O que o escopo determina para a Fase 2.1

> "Todo mês, o sistema lê o perfil e automaticamente monta o calendário inteiro. Você só
> aprova ou ajusta."

Processo especificado no escopo, em cinco entradas de pesquisa:

1. Tendências atuais no nicho (Instagram, LinkedIn, web)
2. Datas comemorativas e sazonais do mês
3. O que concorrentes estão postando
4. Assuntos em alta conectados ao negócio
5. Feedback de performance do mês anterior (quando disponível)

E uma distribuição de funil explícita: **topo ~40%, meio ~35%, fundo ~25%**, com
**~16-20 conteúdos** por mês.

Cada dia de postagem recebe: assunto, etapa do funil, formato sugerido, plataforma e
justificativa.

### Como isso virou arquitetura

As cinco entradas foram agrupadas em **três tasks** de um único pesquisador, porque
compartilham a mesma disciplina (coleta com fonte, data e confiança) e alimentam um único
relatório:

| Entrada do escopo | Task |
|---|---|
| 5. Feedback do mês anterior | `analisar-performance` |
| 1, 2 e 4. Tendências, datas, assuntos em alta | `pesquisar-contexto` |
| 3. Concorrentes | `analisar-concorrentes` |

A **justificativa por item** virou campo obrigatório com teste de rastreabilidade — é a
diferença entre um calendário e uma lista de temas.

---

## 2. O que o escopo determina para a Fase 2.2

> "V1 — planilha: calendário do mês, status de cada conteúdo (planejado > em produção >
> pronto > postado), coluna de métricas preenchida manualmente ou via API depois, separação
> por cliente (aba por cliente)."

### Decisões derivadas

| Ponto | Escopo | Decisão | Justificativa |
|---|---|---|---|
| Formato | "planilha" | CSV | abre em Sheets e Excel, é diffável e versionável em git |
| Separação por cliente | "aba por cliente" | diretório por cliente | abas exigem formato binário; diretório já sustenta o modelo agência (V2) |
| Métricas | manual na v1, API na v2 | mesmo cabeçalho nas duas versões | a v2 preenche as mesmas colunas sem migração |

O **cabeçalho como contrato** é a decisão de maior consequência: é o que permite comparar
meses e o que fará a integração de API da v2 ser aditiva, não disruptiva.

---

## 3. Princípios operacionais derivados

1. **Vazio não é zero.** A distinção mais importante de todo o feedback loop. Métrica não
   medida excluída dos rankings; zero só quando medido.
2. **Grade antes de tema.** Sem fechar a distribuição primeiro, o mês tende a topo por
   inércia — os temas de topo são os mais fáceis de pensar.
3. **Justificativa rastreável.** É o mecanismo que impede o calendário de virar lista de
   ideias soltas e o que dá direção à Camada 3.
4. **Lacuna vale mais que tendência.** O que nenhum concorrente cobriu e endereça uma dor
   real do público é a melhor fonte de tema disponível.
5. **Performance própria pesa mais que tendência externa.** Formato que funcionou para
   este cliente supera formato em alta no nicho.
6. **Coleta parcial declarada vale mais que coleta inventada.** Vale para métricas, posts
   de concorrentes e tendências.

---

## 4. Interfaces

| Direção | Squad | Artefato |
|---|---|---|
| Entrada | `laia-perfil` | `_opensquad/_memory/clientes/{slug}/perfil.json` |
| Entrada | ciclo anterior deste squad | `calendario/{mes-anterior}/controle.csv` |
| Saída | `laia-conteudo` | `calendario/{YYYY-MM}/calendario.yaml` |
| Saída | ciclo seguinte deste squad | `calendario/{YYYY-MM}/controle.csv` preenchido |

O squad é o único ponto do sistema que fecha o ciclo consigo mesmo: a planilha que gera
este mês é a entrada de performance do mês seguinte.

---

## 5. Referências internas do framework

Os arquivos abaixo pertencem ao framework e são relevantes para este squad. Os marcados
como **injetado** são carregados automaticamente pelo Pipeline Runner em tempo de execução,
via o campo `format:` dos steps — e, em qualquer divergência com este squad, **eles
prevalecem**.

- `_opensquad/core/best-practices/strategist.md` — planejamento editorial e funil
- `_opensquad/core/best-practices/researching.md` — disciplina de fonte, data e confiança
- `_opensquad/core/best-practices/data-analysis.md` — leitura de métricas e amostra pequena
- `_opensquad/core/best-practices/review.md` — estrutura de veredito APROVADO/REPROVADO
