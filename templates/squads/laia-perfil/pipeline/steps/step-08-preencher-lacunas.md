---
step: "08"
name: "Preenchimento de Lacunas"
type: checkpoint
depends_on: step-07
outputFile: squads/laia-perfil/output/respostas/lacunas-respondidas.md
---

# 🛑 Checkpoint: Preenchimento de Lacunas

## Para o Pipeline Runner

Apresentar as perguntas de aprofundamento geradas pelo Otávio Onboarding no Step 07 e
coletar as respostas. O usuário pode responder tudo, parte ou nada — lacuna não respondida
segue como pendência registrada no perfil, não vira suposição.

## Formato de Apresentação ao Usuário

Ler `squads/laia-perfil/output/lacunas.md` e apresentar no formato:

```
🎤 Otávio Onboarding revisou tudo e encontrou {N} pontos que valem aprofundar.

⚠️ Críticos (bloqueiam a produção):
1. {pergunta}
   → {por que importa}

📌 Importantes (melhoram a qualidade):
2. {pergunta}
   → {por que importa}

🔀 Inconsistências pra resolver:
- {campo A} vs {campo B}: {pergunta de desempate}

Responde o que conseguir agora. O que ficar sem resposta entra como pendência
no perfil e pode ser preenchido depois com uma atualização.
```

## Ação do Pipeline Runner após Resposta

1. Escrever em `squads/laia-perfil/output/respostas/lacunas-respondidas.md`:

```markdown
# Respostas às Lacunas

**Data:** {YYYY-MM-DD}

## Respondidas
### {campo}
**Pergunta:** {pergunta}
**Resposta:** {texto integral do usuário}

## Não respondidas
- `{campo}` ({criticidade}) — segue como pendência no perfil
```

2. Se todas as lacunas críticas ficarem sem resposta, avisar em uma linha que o perfil vai
   ser publicado incompleto e que a validação do Step 10 provavelmente vai reprovar — mas
   seguir mesmo assim, porque a decisão é do usuário.
3. Avançar para o Step 09 (Estruturação do Perfil).

## Opções Especiais

- **"pular"** → gravar todas as lacunas como não respondidas e seguir.
- **"não sei" em lacuna crítica** → gravar literalmente como não respondida; nunca converter
  em valor plausível.
