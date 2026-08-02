---
step: "09"
name: "Aprovação do Texto"
type: checkpoint
depends_on: step-08
---

# 🛑 Checkpoint: Aprovação do Texto

## Para o Pipeline Runner

Portão obrigatório antes da criação visual. Renderizar imagem de um texto que ainda vai
mudar é retrabalho garantido — e a Fase 3.5 é a mais cara do pipeline.

## Formato de Apresentação ao Usuário

Ler os arquivos de conteúdo que existirem e apresentar:

```
✍️ Conteúdo escrito pronto pra revisão.

📄 Carrossel: squads/laia-conteudo/output/{run_id}/v1/carrossel.md
📄 LinkedIn: squads/laia-conteudo/output/{run_id}/v1/linkedin.md

━━━ CARROSSEL ({N} slides) ━━━
Slide 1: "{texto}"
Slide 2: "{texto}"
...
Legenda: {primeiras 3 linhas}...
Hashtags: {N}

━━━ LINKEDIN ━━━
{primeiras 3 linhas — o que aparece antes do "ver mais"}
...
{insight}
{CTA}
Hashtags: {lista}
Peça visual sugerida: {tipo e conteúdo}

Aprova o texto pra eu partir pras imagens?
1️⃣ Sim, pode gerar as imagens
2️⃣ Quero ajustar algum slide ou trecho
3️⃣ Refazer o conteúdo (mesmo gancho, execução diferente)
4️⃣ Voltar e trocar o gancho
```

## Ação do Pipeline Runner após Resposta

1. **Opção 1** → avançar para o Step 10 (Criação Visual).
2. **Opção 2** → coletar os ajustes indicando slide ou trecho, aplicá-los ao arquivo
   correspondente e reapresentar para nova aprovação. Ajuste pontual não volta ao criador.
3. **Opção 3** → voltar ao Step 07 e/ou 08 mantendo o gancho e o ângulo aprovados, com a
   instrução do que motivou a rejeição. Máximo de 2 retornos.
4. **Opção 4** → voltar ao Step 06 para nova escolha de gancho. O conteúdo escrito é
   descartado, porque o texto inteiro é derivado do gancho.

## Opções Especiais

- **Item que depende de asset do cliente** → se o material ainda não chegou, avisar que o
  Step 10 vai gerar os slides sem ele e que a peça ficará incompleta. Oferecer pausar o
  pipeline aqui e retomar quando o asset estiver disponível.
- **Perfil sem paleta válida** → avisar antes de aprovar: o Step 10 vai parar por falta de
  cor definida. Oferecer rodar `/opensquad run laia-perfil` para atualizar o perfil.
- **Apenas um formato produzido** → normal quando o item previa só uma plataforma; informar
  em uma linha qual formato não foi gerado e por quê.
