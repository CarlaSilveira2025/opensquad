---
step: "04"
name: "Seleção de Ângulos"
type: checkpoint
depends_on: step-03
outputFile: squads/laia-conteudo/output/angulos-selecionados.yaml
---

# 🛑 Checkpoint: Seleção de Ângulos

## Para o Pipeline Runner

Apresentar os ângulos gerados e aguardar a escolha. O usuário pode escolher um ou mais —
ângulos diferentes podem virar formatos diferentes, e é aqui que essa distribuição é
definida.

## Formato de Apresentação ao Usuário

Ler `squads/laia-conteudo/output/angulos.yaml` e apresentar:

```
🎯 Ângela Ângulo gerou {N} ângulos sobre "{assunto}".

Tensão central: {tensao_central}

⭐ Recomendado: #{X} — {justificativa em uma linha}

---
1️⃣ {titulo} · lente {lente} · provocação {N}/5
{resumo}
📌 Melhor formato: {formato_indicado} · Segmento: {segmento}
✅ {forca}
⚠️ {risco}
📊 Ancorado em: {ancora_pesquisa}

---
2️⃣ ...

Qual ângulo quer desenvolver?
· Um número, para um único conteúdo
· Vários números, se quiser formatos diferentes (ex.: "3 pra carrossel, 2 pro LinkedIn")
· "nenhum" para gerar outros ângulos
```

## Ação do Pipeline Runner após Resposta

1. Registrar a escolha e a distribuição por formato. Se o usuário escolher mais de um ângulo
   sem indicar formato, usar o `formato_indicado` de cada um.
2. Conferir a coerência com o briefing do item: se o item previa só Instagram e o usuário
   destinou um ângulo ao LinkedIn, confirmar em uma linha se é para produzir também lá.
3. Escrever em `squads/laia-conteudo/output/angulos-selecionados.yaml`:

```yaml
angulos_selecionados:
  - angulo_id: 3
    titulo: "{título}"
    lente: "{lente}"
    resumo: "{resumo integral do ângulo}"
    ancora_pesquisa: "{dado}"
    formato_destino: "carrossel"
    plataforma: "Instagram"
    provocacao: 4
    risco: "{risco declarado}"
    ajustes_usuario: "{ajustes pedidos, ou vazio}"

selecionado_em: "YYYY-MM-DD HH:MM"
```

4. Avançar para o Step 05 (Geração de Ganchos).

## Opções Especiais

- **"nenhum"** → voltar ao Step 03 pedindo lentes diferentes das já usadas. Máximo de 1
  retorno; no segundo, seguir com o melhor conjunto disponível.
- **"ajustar N"** → registrar o ajuste em `ajustes_usuario` e seguir. O Gabriel Gancho e os
  criadores respeitam o ajuste.
- **"combinar N e M"** → pedir à Ângela um ângulo híbrido antes de avançar, verificando que
  o resultado ainda passa no teste de distinção.
- **Ângulo de provocação 5 escolhido** → repetir o risco declarado em uma linha e pedir
  confirmação antes de seguir.
