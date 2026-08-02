---
step: "01"
name: "Identificação do Cliente"
type: checkpoint
outputFile: squads/laia-perfil/output/cliente.md
---

# 🛑 Checkpoint: Identificação do Cliente

## Para o Pipeline Runner

Antes de qualquer pergunta, listar os clientes já cadastrados lendo os diretórios de
`_opensquad/_memory/clientes/`. Se o diretório não existir, informar que este é o primeiro
cadastro.

## Formato de Apresentação ao Usuário

```
🧬 LAIA — Perfil do Cliente

Clientes já cadastrados: {lista de slugs, ou "nenhum ainda"}

Este perfil é para:
1️⃣ Um cliente novo
2️⃣ Atualizar um cliente existente

Se for novo, me diz o nome da marca/empresa.
Se for atualização, me diz qual cliente e o que mudou.
```

## Ação do Pipeline Runner após Resposta

1. Derivar o `slug` a partir do nome: minúsculas, sem acentos, espaços viram hífen
   (ex.: "Authentic Studio" → `authentic-studio`). Confirmar o slug com o usuário em uma
   linha antes de seguir.
2. Se for atualização, confirmar que `_opensquad/_memory/clientes/{slug}/perfil.json`
   existe. Se não existir, tratar como cadastro novo e avisar o usuário.
3. Escrever a resposta em `squads/laia-perfil/output/cliente.md` no formato:

```markdown
# Cliente

**Nome:** {nome informado}
**Slug:** {slug}
**Tipo:** novo | atualização
**O que mudou:** {apenas em atualização}
**Data:** {YYYY-MM-DD}
```

4. Avançar para o Step 02 (Bloco 1 — Identidade).

## Opções Especiais

- **Atualização parcial** → se o usuário quer mudar só um bloco, registrar em
  "O que mudou" e informar que os demais blocos podem ser respondidos com "manter" para
  reaproveitar o perfil existente.
- **"cancelar"** → encerrar o pipeline sem escrever nada no registro de clientes.
