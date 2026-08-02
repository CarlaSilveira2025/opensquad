---
step: "03"
name: "Bloco 2 — Público-Alvo"
type: checkpoint
depends_on: step-02
outputFile: squads/laia-perfil/output/respostas/publico.md
---

# 🛑 Checkpoint: Bloco 2 — Público-Alvo

## Para o Pipeline Runner

Coletar as seis informações de público. Este é o bloco mais determinante da qualidade do
conteúdo: sem dores concretas, todo o sistema produz conteúdo genérico. Se o usuário
responder com menos de 3 dores, pedir explicitamente mais uma vez antes de seguir.

## Formato de Apresentação ao Usuário

```
📋 Bloco 2 de 5 — Público-Alvo

1. Quem são (perfil, tipo de negócio, momento de vida ou de empresa)
2. Dores principais — no mínimo 3, em situações concretas
   Ex.: "perde cliente porque demora pra responder" é dor;
        "falta de organização" é adjetivo
3. Desejos e aspirações
4. Onde estão (redes, grupos, comunidades)
5. Faixa etária
6. Que linguagem usam — gíria, formalidade, termos que essa gente fala

Pode responder tudo de uma vez.
```

## Ação do Pipeline Runner após Resposta

1. Contar quantas dores concretas foram citadas. Se forem menos de 3, responder uma única
   vez: "Consegue me dar mais {N} dores em situação concreta? É o campo que mais muda a
   qualidade do conteúdo." Depois seguir com o que houver.
2. Escrever em `squads/laia-perfil/output/respostas/publico.md`:

```markdown
# Bloco 2 — Público-Alvo

**Resposta do usuário:**
{texto integral}

**Dores concretas identificadas:** {contagem}
**Perguntas não respondidas:** {lista, ou "nenhuma"}
```

3. Avançar para o Step 04 (Bloco 3 — Comunicação).

## Opções Especiais

- **Mais de um público** → registrar todos, marcando qual é o principal. O calendário da
  Camada 2 usa o principal como padrão e o secundário para conteúdo de LinkedIn quando
  aplicável.
- **"manter"** (em atualização) → reaproveitar o bloco do perfil existente.
