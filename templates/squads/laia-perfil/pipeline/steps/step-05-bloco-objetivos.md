---
step: "05"
name: "Bloco 4 — Objetivos"
type: checkpoint
depends_on: step-04
outputFile: squads/laia-perfil/output/respostas/objetivos.md
---

# 🛑 Checkpoint: Bloco 4 — Objetivos

## Para o Pipeline Runner

Coletar meta, ofertas atuais, histórico de performance, plataformas e frequência. O histórico
do que NÃO funcionou é o insumo mais valioso deste bloco: é o que impede o calendário de
repetir formatos já reprovados na prática.

## Formato de Apresentação ao Usuário

```
📋 Bloco 4 de 5 — Objetivos

1. Meta principal do conteúdo — escolhe a que mais importa hoje:
   seguidores · vendas · autoridade · leads · engajamento
2. Ofertas e produtos que você está vendendo AGORA
3. O que já funcionou no seu conteúdo (formato, tema, post específico)
4. O que já NÃO funcionou — e, se souber, por quê
5. Plataformas ativas: Instagram · LinkedIn · ambas
6. Quantos conteúdos por semana você quer publicar?

Pode responder tudo de uma vez.
```

## Ação do Pipeline Runner após Resposta

1. Se o usuário escolher mais de uma meta principal, pedir uma única vez que ordene por
   prioridade — a distribuição de funil do calendário depende de uma meta dominante.
2. Escrever em `squads/laia-perfil/output/respostas/objetivos.md`:

```markdown
# Bloco 4 — Objetivos

**Resposta do usuário:**
{texto integral}

**Meta principal declarada:** {valor}
**Plataformas declaradas:** {lista}
**Frequência declarada:** {valor}
**Perguntas não respondidas:** {lista, ou "nenhuma"}
```

3. Avançar para o Step 06 (Bloco 5 — Assets Visuais).

## Opções Especiais

- **"nunca publiquei nada"** → gravar literalmente; os campos de histórico ficam vazios e o
  primeiro mês do calendário roda em modo exploratório, sem feedback loop.
- **Frequência maior que 7 por semana** → registrar, mas sinalizar no Step 07 que a
  frequência declarada pode não ser sustentável para o volume de conteúdo do calendário.
- **"manter"** (em atualização) → reaproveitar o bloco do perfil existente.
