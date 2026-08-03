---
step: "13"
name: "Entrega e Atualização de Status"
type: checkpoint
depends_on: step-12
outputFile: squads/laia-conteudo/output/entrega.md
---

# 🛑 Checkpoint: Entrega e Atualização de Status

## Para o Pipeline Runner

Fecha o ciclo do item: entrega o pacote pronto para postar e atualiza o status na planilha
de controle do mês, que é a base do feedback loop.

## Formato de Apresentação ao Usuário

```
✅ Conteúdo pronto — item #{n} do calendário de {mês}.

Revisão da Vera Veredito: {APROVADO | REPROVADO} — nota {X,X}/10

📁 Pacote completo: squads/laia-conteudo/output/{run_id}/

Para postar:
· Carrossel Instagram — {N} imagens em `slides/rendered/`, na ordem 01 a {NN}
· Legenda do carrossel — em `carrossel.md`, seção "Legenda"
· Post LinkedIn — texto em `linkedin.md` + imagem `linkedin-01.png`

{ressalvas da revisão, se houver}

Quer que eu marque este item como "pronto" na planilha de controle?
1️⃣ Sim, marcar como pronto
2️⃣ Já postei — marcar como postado e registrar a data
3️⃣ Não marcar agora
```

## Ação do Pipeline Runner após Resposta

1. **Opção 1** → abrir
   `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/controle.csv`, localizar a linha
   pelo `n` e pela `data`, e alterar `status` de `planejado` para `pronto`. Preservar todas
   as demais colunas, inclusive as de métrica.
2. **Opção 2** → alterar `status` para `postado` e preencher `data_postagem` com a data
   informada. **Não** preencher nenhuma coluna de métrica — elas ficam vazias até medição
   real. Lembrar o usuário de voltar à planilha depois de alguns dias para preencher.
3. **Opção 3** → não tocar na planilha e registrar isso no relatório de entrega.
4. Em qualquer caso, escrever
   `squads/laia-conteudo/output/entrega.md`:

```markdown
# Entrega — {assunto}

**Item:** #{n} do calendário {YYYY-MM} | avulso
**Cliente:** {slug}
**Veredito:** {APROVADO | REPROVADO} — nota {X,X}
**Data:** {YYYY-MM-DD}

## Arquivos para postar
### Carrossel Instagram
- Imagens: {lista na ordem}
- Legenda: `carrossel.md`, seção "Legenda"
- Hashtags: {N}

### Post LinkedIn
- Texto: `linkedin.md`
- Imagem: `linkedin-01.png` ({dimensão})

## Status na planilha
- Ação: pronto | postado ({data}) | não atualizado
- Arquivo: `_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/controle.csv`

## Ressalvas da revisão
- {ressalva}

## Lembrete do feedback loop
Depois de publicar, preencher as colunas de métrica no `controle.csv`. Deixar em branco o
que não foi medido — **nunca preencher com zero**.
```

5. Encerrar o pipeline apresentando o caminho do pacote e o próximo item do calendário.

## Opções Especiais

- **Item avulso** → não há linha na planilha para atualizar; registrar `Origem: avulso` e
  pular a etapa de status.
- **Veredito REPROVADO** → confirmar uma vez se o usuário quer mesmo entregar, listando os
  bloqueadores em aberto. Se confirmado, registrar a decisão no relatório.
- **Planilha do mês inexistente** → avisar que o status não pôde ser atualizado e sugerir
  rodar `/opensquad run laia-calendario` para o mês em questão.
