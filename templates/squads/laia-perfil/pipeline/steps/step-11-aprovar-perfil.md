---
step: "11"
name: "Aprovação do Perfil"
type: checkpoint
depends_on: step-10
---

# 🛑 Checkpoint: Aprovação do Perfil

## Para o Pipeline Runner

Último portão antes da escrita no registro de clientes. Apresentar o brand book e o veredito
da validação, e aguardar aprovação explícita. Nada é escrito em
`_opensquad/_memory/clientes/` antes deste checkpoint.

## Formato de Apresentação ao Usuário

Ler `squads/laia-perfil/output/brand-book.md` e
`squads/laia-perfil/output/validacao-perfil.md` e apresentar:

```
🗂️ Perfil de {nome} pronto pra revisão.

Validação da Renata Revisão: {APROVADO | REPROVADO}
Bloqueadores: {N} · Pendências toleráveis: {N}

📄 Brand book completo: squads/laia-perfil/output/{run_id}/v1/brand-book.md
📄 Perfil estruturado: squads/laia-perfil/output/{run_id}/v1/perfil.json

--- Resumo ---
{as seções "Quem é", "Para quem fala" e "Como aparece" do brand book}

--- O que ainda falta ---
{seção de pendências}

Posso publicar esse perfil no registro de clientes?
1️⃣ Sim, publicar
2️⃣ Quero corrigir alguma coisa antes
3️⃣ Cancelar sem publicar
```

## Ação do Pipeline Runner após Resposta

1. **Opção 1** → avançar para o Step 12 (Publicação).
2. **Opção 2** → coletar as correções em texto livre, gravá-las como ajustes do usuário e
   voltar ao Step 09 para a Perfiladora regerar o perfil com as correções. Este retorno não
   conta no limite de ciclos de revisão automática, porque é correção pedida pelo usuário.
3. **Opção 3** → encerrar o pipeline sem escrever nada no registro de clientes. Os arquivos
   do run permanecem em `squads/laia-perfil/output/{run_id}/` para retomada posterior.

## Opções Especiais

- **Veredito REPROVADO e usuário escolhe publicar mesmo assim** → confirmar uma vez,
  explicitando quais bloqueadores seguem abertos e que os squads seguintes vão operar com
  informação faltando. Se confirmado, seguir para o Step 12 e registrar a decisão no
  relatório de publicação.
- **Correção apenas de campo visual (cor, fonte)** → ainda assim volta ao Step 09; o
  `perfil.json` nunca é editado à mão fora do agente responsável.
