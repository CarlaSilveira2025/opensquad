---
step: "01"
name: "Seleção do Item"
type: checkpoint
outputFile: squads/laia-conteudo/output/briefing-item.md
---

# 🛑 Checkpoint: Seleção do Item

## Para o Pipeline Runner

Cumpre o papel do **Research Focus Checkpoint**: o Pedro Pesquisa roda como subagente e não
pode perguntar nada, então o assunto e o recorte são definidos aqui.

Antes de perguntar, listar os clientes em `_opensquad/_memory/clientes/` e, para o cliente
escolhido, ler o calendário do mês corrente em
`_opensquad/_memory/clientes/{slug}/calendario/{YYYY-MM}/calendario.yaml`, filtrando os
itens com `status: planejado`.

## Formato de Apresentação ao Usuário

```
🏭 LAIA — Produção de Conteúdo

Cliente: {slug} · Calendário de {mês}

Itens ainda não produzidos:
1️⃣ #{n} · {data} · {assunto} — {etapa} · {formato} · {plataforma}
2️⃣ #{n} · {data} · {assunto} — {etapa} · {formato} · {plataforma}
...

Qual item quer produzir agora?
Ou: digite "avulso" para produzir um conteúdo fora do calendário.
```

## Ação do Pipeline Runner após Resposta

1. Se o calendário do mês não existir, informar que é preciso rodar
   `/opensquad run laia-calendario` antes, e oferecer a opção "avulso".
2. Se o item escolhido tiver `depende_de_asset: true`, perguntar se o material já está
   disponível. Se não estiver, avisar que a produção segue mas o conteúdo ficará bloqueado
   na fase visual, e confirmar se o usuário quer continuar.
3. Escrever em `squads/laia-conteudo/output/briefing-item.md`:

```markdown
# Briefing do Item

**Cliente:** {slug}
**Origem:** calendário {YYYY-MM}, item #{n} | avulso
**Data prevista:** {YYYY-MM-DD}
**Assunto:** {assunto}
**Etapa de funil:** {topo|meio|fundo}
**Formato previsto:** {carrossel|post-linkedin|ambos}
**Plataforma:** {Instagram|LinkedIn|ambas}
**Oferta promovida:** {apenas em itens de fundo}
**Justificativa do calendário:** {texto integral}
**Depende de asset:** {sim, qual | não}
**Observações do usuário:** {texto livre, se houver}
**Data:** {YYYY-MM-DD}
```

4. Avançar para o Step 02 (Pesquisa e Inteligência).

## Opções Especiais

- **"avulso"** → pedir assunto, etapa de funil, formato e plataforma diretamente ao usuário
  e registrar `Origem: avulso`. O item não será marcado na planilha de controle no Step 13.
- **Múltiplos formatos** → se o item previr carrossel e LinkedIn, registrar `ambas` em
  plataforma. Os steps 07 e 08 rodarão os dois criadores.
- **Perfil com pendência crítica** → avisar em uma linha quais campos faltam e o efeito
  prático na produção antes de seguir.
