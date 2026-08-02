---
step: "04"
name: "Bloco 3 — Comunicação"
type: checkpoint
depends_on: step-03
outputFile: squads/laia-perfil/output/respostas/comunicacao.md
---

# 🛑 Checkpoint: Bloco 3 — Comunicação

## Para o Pipeline Runner

Coletar tom de voz, vocabulário e referências. Adjetivo de tom sem exemplo concreto não é
utilizável pelos criadores de conteúdo — por isso a pergunta 1 pede explicitamente um
exemplo real de texto do usuário.

## Formato de Apresentação ao Usuário

```
📋 Bloco 3 de 5 — Comunicação

1. Tom de voz (formal, descontraído, provocativo, educativo, misto)
   → e me cola um post, áudio transcrito ou mensagem sua que representa bem como você fala
2. Palavras e expressões que você usa muito
3. Palavras e expressões que você NÃO quer ver no seu conteúdo
4. Referências — contas ou criadores que você admira, e o que especificamente admira
   em cada um (o jeito de escrever? o visual? a estrutura?)

Pode responder tudo de uma vez.
```

## Ação do Pipeline Runner após Resposta

1. Se o usuário informou tom mas não deu nenhum exemplo de texto próprio, pedir uma única
   vez: "Me manda um texto curto seu — qualquer post ou mensagem. É com ele que o sistema
   aprende sua voz."
2. Escrever em `squads/laia-perfil/output/respostas/comunicacao.md`:

```markdown
# Bloco 3 — Comunicação

**Resposta do usuário:**
{texto integral}

**Amostra de voz fornecida:** sim | não
**Perguntas não respondidas:** {lista, ou "nenhuma"}
```

3. Preservar a amostra de voz em bloco de citação, sem edição — ela é usada literalmente
   como calibragem pelos criadores da Camada 3.
4. Avançar para o Step 05 (Bloco 4 — Objetivos).

## Opções Especiais

- **Nenhuma palavra proibida** → gravar lista vazia explicitamente, não `PENDENTE`; ausência
  de proibições é uma resposta válida.
- **"manter"** (em atualização) → reaproveitar o bloco do perfil existente.
