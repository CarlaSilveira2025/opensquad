# Research Brief — Produção de Conteúdo LAIA

## Origem deste brief

Squad construído diretamente a partir do documento **"Sistema de Produção de Conteúdo com
IA — LAIA, Escopo Operacional Final (v3)"**, e não pelo fluxo padrão de pesquisa do
Architect. Nenhuma estatística de mercado é citada aqui porque nenhuma foi coletada —
inventar fonte seria pior que não ter fonte.

---

## 1. O que o escopo determina, fase por fase

### Fase 3.1 — Pesquisa e Inteligência
Fontes: Instagram, LinkedIn, web geral e concorrentes. Identificar o que está funcionando,
o que está saturado, dados e estatísticas para dar autoridade, perguntas frequentes do
público e dores relacionadas.

**Decisão derivada:** "o que está saturado" virou seção obrigatória com contagem de peças,
não observação lateral — é o insumo que impede a Fase 3.2 de propor o ângulo já batido.

### Fase 3.2 — Ângulos (mínimo 5)
Cada ângulo com título, resumo de 2-3 linhas, formato mais adequado, nível de provocação de
1 a 5 e segmento do público. Ângulos diferentes podem virar formatos diferentes.

**Decisão derivada:** o **teste de distinção** (dois ângulos que aceitam o mesmo slide 1 são
o mesmo ângulo) foi acrescentado porque o erro mais comum e mais destrutivo desta fase é
entregar cinco pautas no lugar de cinco lentes.

### Fase 3.3 — Ganchos (3 por ângulo)
Cinco tipos: pergunta provocativa, afirmação chocante, história, dado/estatística,
contraintuitivo. Cada gancho com texto exato, tipo, formato indicado e sugestão de visual
de abertura.

**Decisão derivada:** obrigatoriedade de **três tipos diferentes** por ângulo. Sem essa
regra, os três ganchos convergem para o mesmo tipo e o usuário escolhe entre três redações
da mesma ideia.

### Fase 3.4 — Criação de Conteúdo
Carrossel (6-10 slides com texto exato por slide, legenda e indicação visual), Reels
(roteiro com marcação de tempo) e post LinkedIn (formato longo com storytelling).

**Decisão derivada:** um agente criador por formato, conforme a convenção do framework para
squads de conteúdo. Isso permite que rodem em paralelo e que cada um receba a injeção
automática do arquivo de best-practice da plataforma.

### Fase 3.5 — Criação Visual
Slides individuais respeitando logo, cores, fontes e estilo do perfil, com texto sobreposto
legível e hierarquia clara.

**Decisão derivada:** a etapa foi quebrada em três tasks — sistema visual, HTML, renderização
— porque definir o sistema antes de montar os slides é o que garante consistência entre eles.

---

## 2. Escopo entregue e escopo adiado

O documento tem uma tensão interna: a Fase 3.4 descreve Reels em detalhe, mas a seção
**"Ordem de Construção (roadmap)"** coloca Reels como item **10**, na "próxima fase", e a
"fase atual" vai até o item 9.

**Decisão:** seguir o roadmap, que é a instrução mais específica sobre ordem de construção.

| Formato | Status |
|---|---|
| Carrossel Instagram | implementado (Fases 3.4 e 3.5) |
| Post LinkedIn | implementado (Fases 3.4 e 3.5) |
| Reels | **não implementado** — roadmap item 10 |

O ponto de extensão para Reels está documentado em `domain-framework.md`, seção 6. A
arquitetura já o acomoda: ângulos e ganchos saem classificados por formato, e o checkpoint 04
já distribui ângulos diferentes para formatos diferentes.

---

## 3. Princípios operacionais derivados

1. **Nenhum dado sem lastro.** Veracidade é o eixo eliminatório da revisão. É o erro mais
   caro do sistema: o conteúdo é publicado no nome do cliente e corrigido em público.
2. **Gancho aprovado é imutável.** Passou por checkpoint, entra literal. Reescrever invalida
   a decisão do usuário e quebra a coerência com a abertura visual sugerida.
3. **Texto aprovado é intocável no visual.** Não coube no slide? Ajusta o design.
4. **Ângulo é lente, não subtema.** A distinção que define a Fase 3.2.
5. **Cada fase entrega opções, o usuário decide.** Seis checkpoints, um em cada bifurcação
   criativa.
6. **Saturação é entrega.** O que evitar vale tanto quanto o que usar.

---

## 4. Interfaces

| Direção | Origem/Destino | Artefato |
|---|---|---|
| Entrada | `laia-perfil` | `_opensquad/_memory/clientes/{slug}/perfil.json` |
| Entrada | `laia-calendario` | `calendario/{YYYY-MM}/calendario.yaml` |
| Saída | usuário | `output/{run_id}/` — textos e imagens prontos |
| Saída | `laia-calendario` | `controle.csv` com `status` atualizado |

---

## 5. Referências internas do framework consultadas

- `_opensquad/core/best-practices/copywriting.md` — ganchos, CTA, estrutura persuasiva
- `_opensquad/core/best-practices/instagram-feed.md` — injetado no step 07
- `_opensquad/core/best-practices/linkedin-post.md` — injetado no step 08
- `_opensquad/core/best-practices/researching.md` — disciplina de fonte, data e confiança
- `_opensquad/core/best-practices/image-design.md` — geração de HTML/CSS para render
- `_opensquad/core/best-practices/review.md` — veredito com nota por eixo
- `skills/image-creator/SKILL.md` — renderização HTML → PNG via Playwright
