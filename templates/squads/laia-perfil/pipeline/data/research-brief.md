# Research Brief — Perfil de Cliente LAIA

## Origem deste brief

Este squad **não** foi gerado pelo fluxo padrão de pesquisa do Architect. Ele foi construído
diretamente a partir do documento de escopo **"Sistema de Produção de Conteúdo com IA —
LAIA, Escopo Operacional Final (v3)"**, fornecido pela operadora do sistema.

Registrar isso importa: as decisões abaixo têm como fonte o escopo do cliente, não pesquisa
web. Nenhuma estatística de mercado é citada aqui porque nenhuma foi coletada — inventar
fonte seria pior que não ter fonte.

---

## 1. O que o escopo determina para a Fase 1.1

> "Questionário inteligente que coleta e armazena tudo sobre o negócio. Feito uma única vez
> por cliente, atualizado quando algo mudar."
>
> "Saída: perfil estruturado salvo (JSON ou documento) que alimenta TODAS as fases seguintes
> automaticamente."

Duas consequências de arquitetura:

1. **O perfil é contrato, não documento.** Se ele alimenta todas as fases automaticamente,
   precisa de schema estável e tipos previsíveis. Daí o `perfil.json` versionado.
2. **O ciclo de vida é "uma vez + atualizações".** Daí o arquivamento em `historico/` e o
   suporte a resposta `manter` por bloco.

---

## 2. Os cinco blocos vêm do escopo

O escopo lista literalmente cinco grupos de informação: Identidade, Público-alvo,
Comunicação, Objetivos e Assets visuais. O pipeline preserva essa divisão em cinco
checkpoints, um por bloco, em vez de um questionário único.

**Razão:** um bloco por checkpoint permite retomar o onboarding no ponto em que parou e
permite a resposta `manter` em atualizações parciais.

---

## 3. Onde o escopo é omisso e o squad decidiu

| Ponto | O escopo diz | Decisão tomada | Justificativa |
|---|---|---|---|
| Formato de saída | "JSON ou documento" | Os dois: `perfil.json` + `brand-book.md` | JSON para máquina, markdown para o cliente conferir |
| Local de armazenamento | não especifica | `_opensquad/_memory/clientes/{slug}/` | isola por cliente e já sustenta o modelo agência (V2) |
| O que é "inteligente" | não define | Detecção de lacunas + perguntas de aprofundamento | é o que diferencia de um formulário estático |
| Validação | não menciona | Gate de 9 bloqueadores antes de publicar | evita que perfil incompleto contamine as Camadas 2 e 3 |

---

## 4. Princípios operacionais derivados

1. **Nunca inventar dado do negócio do cliente.** É o princípio mais caro de violar: um
   campo inventado só é descoberto depois de semanas de conteúdo publicado.
2. **Adjetivo não é dado.** "Premium", "descontraído" e "clean" precisam de exemplo concreto
   para virar instrução acionável para os criadores da Camada 3.
3. **Dor precisa ser situação.** O escopo pede "dores principais"; a operacionalização exige
   que sejam situações observáveis, porque é delas que saem os temas do calendário.
4. **Cor precisa de hex.** A Fase 3.5 gera HTML/CSS; nome de cor não é renderizável de forma
   determinística.
5. **Ausência é informação.** Pendência registrada e visível é melhor que campo silenciosamente
   vazio ou preenchido por suposição.

---

## 5. Interfaces com os demais squads

| Consumidor | O que lê do perfil | Efeito de campo ausente |
|---|---|---|
| `laia-calendario` | `publico.dores`, `objetivos.*`, `identidade.ofertas` | sem dores, temas genéricos; sem histórico, roda sem feedback loop |
| `laia-conteudo` | perfil inteiro, com destaque para `comunicacao.*` e `visual.*` | sem tom, voz genérica; sem paleta, visual quebrado |

---

## 6. Referências internas do framework consultadas

- `_opensquad/core/best-practices/strategist.md` — planejamento editorial e segmentação
- `_opensquad/core/best-practices/copywriting.md` — vocabulário de dor, oferta e prova social
- `_opensquad/core/best-practices/review.md` — estrutura de veredito APROVADO/REPROVADO
- `_opensquad/core/best-practices/image-design.md` — exigência de hex para geração visual
