---
step: "11"
name: "Aprovação das Imagens"
type: checkpoint
depends_on: step-10
---

# 🛑 Checkpoint: Aprovação das Imagens

## Para o Pipeline Runner

Apresentar as imagens renderizadas para conferência visual antes da revisão final. Este é o
último ponto barato para ajustar design — depois daqui, o conteúdo vai para entrega.

## Formato de Apresentação ao Usuário

Ler o relatório do Step 10 e apresentar as imagens usando a ferramenta Read, na ordem de
publicação:

```
🎨 Davi Design renderizou {N} peças.

📁 Pasta: squads/laia-conteudo/output/{run_id}/slides/rendered/

Sistema visual aplicado:
Fundo {hex} · Texto {hex} · Destaque {hex} · Fonte {nome}

--- Carrossel ({N} slides, 1080×1440) ---
{apresentar cada imagem na ordem, com o resumo do slide}

--- LinkedIn ({dimensão}) ---
{apresentar a peça}

--- Restrições registradas ---
{lista de restrições e falhas do relatório}

As imagens estão boas?
1️⃣ Sim, seguir pra revisão final
2️⃣ Quero ajustar o visual de algum slide
3️⃣ Refazer o sistema visual inteiro
4️⃣ Voltar e ajustar o texto
```

## Ação do Pipeline Runner após Resposta

1. **Opção 1** → avançar para o Step 12 (Revisão Final).
2. **Opção 2** → coletar o ajuste indicando o slide e o que mudar (cor, tamanho, composição),
   e voltar ao Step 10 apenas para os slides afetados. O texto permanece intocado.
3. **Opção 3** → voltar ao Step 10 desde a definição do sistema visual, registrando o que
   motivou a rejeição. Máximo de 2 retornos.
4. **Opção 4** → voltar ao Step 09. Mudança de texto invalida os slides já renderizados, que
   serão regerados depois.

## Opções Especiais

- **Slide reportado como problemático no Step 10** → destacar em uma linha qual é e o que
  falhou, para o usuário decidir se aceita ou pede correção.
- **Conteúdo sem logo** → se `visual.logo` estava ausente, lembrar que os slides saíram sem
  assinatura visual e que isso se resolve enviando o arquivo para
  `_opensquad/_memory/clientes/{slug}/assets/` e atualizando o perfil.
- **Pedido de ajuste que exige cortar texto** → recusar o corte e oferecer alternativas de
  design (corpo menor dentro da escala, mais slides, composição diferente). Texto aprovado
  não é alterado por limitação de layout.
