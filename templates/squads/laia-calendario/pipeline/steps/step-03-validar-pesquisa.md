---
step: "03"
name: "Validação da Pesquisa"
type: checkpoint
depends_on: step-02
outputFile: squads/laia-calendario/output/ajustes-pesquisa.md
---

# 🛑 Checkpoint: Validação da Pesquisa

## Para o Pipeline Runner

Apresentar o resumo da pesquisa e coletar direcionamento antes de montar o calendário.
Este é o momento mais barato para corrigir rumo: ajustar aqui custa uma resposta; ajustar
depois custa refazer 18 itens.

## Formato de Apresentação ao Usuário

Ler `squads/laia-calendario/output/pesquisa-mensal.md` e apresentar:

```
🔍 Tiago Tendência terminou a pesquisa de {mês}.

📄 Relatório completo: squads/laia-calendario/output/{run_id}/v1/pesquisa-mensal.md

--- Performance de {mês anterior} ---
{status: com dados / sem dados}
{até 3 aprendizados acionáveis, com confiança}

--- O que está em alta ---
{até 4 achados com data e confiança}

--- O que evitar (saturado) ---
{lista de temas saturados}

--- Lacunas: onde ninguém está falando ---
{lacunas editoriais — é daqui que sai o melhor conteúdo do mês}

--- Ganchos sazonais ---
{datas com conexão concreta}

Antes de eu montar o calendário:
1️⃣ Pode seguir assim
2️⃣ Quero priorizar ou descartar algum tema
3️⃣ Faltou alguma coisa — quero que pesquise mais
```

## Ação do Pipeline Runner após Resposta

1. Escrever em `squads/laia-calendario/output/ajustes-pesquisa.md`:

```markdown
# Ajustes à Pesquisa

**Decisão:** seguir | priorizar/descartar | pesquisar mais
**Temas a priorizar:** {lista, ou "nenhum"}
**Temas a descartar:** {lista, ou "nenhum"}
**Observações do usuário:** {texto integral}
**Data:** {YYYY-MM-DD}
```

2. **Opção 1** → avançar para o Step 04.
3. **Opção 2** → registrar as prioridades e descartes e avançar para o Step 04. A
   Estrategista trata a lista de descarte como restrição rígida.
4. **Opção 3** → voltar ao Step 02 com o escopo adicional pedido pelo usuário, registrando
   o que precisa ser pesquisado a mais. Máximo de 1 retorno; no segundo, seguir com o que há.

## Opções Especiais

- **Pesquisa sem dados de performance** (primeiro mês) → informar em uma linha que o
  calendário vai rodar em modo exploratório e que o feedback loop começa a valer no mês
  seguinte, depois que a planilha for preenchida.
- **Coleta de concorrentes parcial ou falha** → informar a limitação e perguntar se o
  usuário quer indicar outros perfis antes de seguir.
