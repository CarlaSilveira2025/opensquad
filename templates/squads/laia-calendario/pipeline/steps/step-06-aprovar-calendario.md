---
step: "06"
name: "Aprovação do Calendário"
type: checkpoint
depends_on: step-05
---

# 🛑 Checkpoint: Aprovação do Calendário

## Para o Pipeline Runner

Portão antes de gerar a planilha e publicar no registro do cliente. Apresentar o calendário
completo em tabela e o veredito da revisão, e aguardar aprovação explícita.

## Formato de Apresentação ao Usuário

Ler `squads/laia-calendario/output/calendario.md` e
`squads/laia-calendario/output/revisao-calendario.md` e apresentar:

```
🗓️ Calendário de {mês} pronto — {N} conteúdos.

Revisão da Vera Veredito: {APROVADO | REPROVADO}
Bloqueadores: {N} · Ressalvas: {N}

Distribuição: Topo {N} ({%}) · Meio {N} ({%}) · Fundo {N} ({%})

📄 Calendário completo: squads/laia-calendario/output/{run_id}/v1/calendario.md
📄 Revisão: squads/laia-calendario/output/{run_id}/v1/revisao-calendario.md

--- Calendário ---
{tabela completa: # | data | assunto | etapa | formato | plataforma | asset?}

--- Ressalvas da revisão ---
{lista de ressalvas}

--- Itens que dependem de material seu ---
{itens com depende_de_asset: true, com o asset necessário}

Aprova esse calendário?
1️⃣ Sim — gerar planilha e publicar
2️⃣ Quero trocar ou ajustar itens específicos
3️⃣ Refazer o calendário inteiro
4️⃣ Cancelar
```

## Ação do Pipeline Runner após Resposta

1. **Opção 1** → avançar para o Step 07 (Planilha de Controle e Publicação).
2. **Opção 2** → coletar os ajustes em texto livre (ex.: "troca o item 7 por algo sobre
   precificação", "move o 15 pra 27/08"), registrar e voltar ao Step 04 para a Estrategista
   aplicar. Este retorno é correção pedida pelo usuário e **não** conta no limite de 2
   ciclos automáticos de revisão.
3. **Opção 3** → voltar ao Step 04 com instrução de refazer a montagem inteira, mantendo a
   pesquisa já feita. Coletar o que motivou a rejeição total.
4. **Opção 4** → encerrar o pipeline sem escrever no registro do cliente. Os arquivos do run
   permanecem em `squads/laia-calendario/output/{run_id}/` para retomada.

## Opções Especiais

- **Veredito REPROVADO e usuário aprova mesmo assim** → confirmar uma vez, explicitando quais
  bloqueadores seguem abertos e o efeito prático de cada um na produção. Se confirmado,
  seguir para o Step 07 e registrar a decisão no relatório de publicação.
- **Republicação de mês já existente** → lembrar em uma linha que as métricas já preenchidas
  na planilha serão preservadas e que a versão anterior será arquivada.
