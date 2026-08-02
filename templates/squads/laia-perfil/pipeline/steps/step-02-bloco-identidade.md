---
step: "02"
name: "Bloco 1 — Identidade"
type: checkpoint
depends_on: step-01
outputFile: squads/laia-perfil/output/respostas/identidade.md
---

# 🛑 Checkpoint: Bloco 1 — Identidade

## Para o Pipeline Runner

Coletar as cinco informações de identidade da marca. Apresentar as perguntas de uma vez —
o usuário pode responder em texto corrido, e o Entrevistador organiza depois. Se a resposta
deixar alguma pergunta em branco, perguntar apenas as que faltaram, uma vez, antes de seguir.

## Formato de Apresentação ao Usuário

```
📋 Bloco 1 de 5 — Identidade

1. Nome da marca/empresa e o que ela é em uma frase
2. Nicho de atuação
3. O que vende — produtos e serviços, com preço e promessa de cada um
4. Diferenciais — o que te separa de quem faz parecido
5. Como quer ser percebida (autoridade, acessível, premium, provocativa…)
   → me dá um exemplo de marca que tem a percepção que você quer

Pode responder tudo de uma vez, do seu jeito.
```

## Ação do Pipeline Runner após Resposta

1. Escrever a resposta integral em
   `squads/laia-perfil/output/respostas/identidade.md`, preservando as palavras do usuário:

```markdown
# Bloco 1 — Identidade

**Resposta do usuário:**
{texto integral, sem reescrever}

**Perguntas não respondidas:** {lista, ou "nenhuma"}
```

2. Não interpretar, resumir nem completar a resposta — isso é trabalho do Step 07.
3. Avançar para o Step 03 (Bloco 2 — Público-Alvo).

## Opções Especiais

- **"manter"** (em atualização) → gravar `manter` como resposta; o Entrevistador reaproveita
  o bloco correspondente do perfil existente.
- **"não sei"** em alguma pergunta → gravar literalmente; vira lacuna no Step 07, não
  suposição.
