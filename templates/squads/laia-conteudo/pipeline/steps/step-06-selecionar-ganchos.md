---
step: "06"
name: "Seleção de Ganchos"
type: checkpoint
depends_on: step-05
outputFile: squads/laia-conteudo/output/ganchos-selecionados.yaml
---

# 🛑 Checkpoint: Seleção de Ganchos

## Para o Pipeline Runner

Apresentar os três ganchos de cada ângulo aprovado e coletar a escolha. O gancho escolhido é
imutável a partir daqui: os criadores o usam literal, sem reescrever.

## Formato de Apresentação ao Usuário

Ler `squads/laia-conteudo/output/ganchos.yaml` e apresentar, por ângulo:

```
🪝 Gabriel Gancho escreveu 3 ganchos para cada ângulo aprovado.

━━━ Ângulo {N}: {título} ━━━
⭐ Recomendado: {id} — {justificativa em uma linha}

{id}a · tipo {tipo} · {formato}
"{texto exato}"
🎬 Abertura: {abertura_visual}
🤝 Promete: {promessa}

{id}b · tipo {tipo} · {formato}
"{texto exato}"
🎬 Abertura: {abertura_visual}
🤝 Promete: {promessa}

{id}c · ...

Qual gancho para cada ângulo?
Responda com o id (ex.: "3b") ou "3b, mas troca 'processo' por 'rotina'".
```

## Ação do Pipeline Runner após Resposta

1. Registrar o gancho escolhido por ângulo. Se o usuário pedir ajuste de palavra, aplicar o
   ajuste ao texto e gravar o **texto já ajustado** — é ele que vai literal ao conteúdo.
2. Conferir que o texto ajustado ainda respeita os limites: 2 linhas visíveis e, no
   LinkedIn, ~200 caracteres. Se estourar, avisar e pedir confirmação.
3. Escrever em `squads/laia-conteudo/output/ganchos-selecionados.yaml`:

```yaml
ganchos_selecionados:
  - angulo_id: 3
    angulo_titulo: "{título}"
    gancho_id: "3b"
    texto_final: |
      {texto exato que vai ao conteúdo, já com ajustes do usuário}
    tipo: "{tipo}"
    formato_destino: "carrossel"
    plataforma: "Instagram"
    abertura_visual: "{cena}"
    promessa: "{promessa}"
    ajustado_pelo_usuario: true | false

selecionado_em: "YYYY-MM-DD HH:MM"
```

4. Avançar para os steps de criação (07 e/ou 08, conforme os formatos de destino).

## Opções Especiais

- **"nenhum desses"** → voltar ao Step 05 para o ângulo em questão, pedindo tipos diferentes
  dos já apresentados. Máximo de 1 retorno por ângulo.
- **Gancho de um ângulo usado em outro formato** → permitido, desde que o texto seja
  reavaliado quanto ao limite do formato de destino.
- **Ajuste que remove o número de um gancho de dado** → avisar que o tipo muda de "dado"
  para outro e que o conteúdo perde a âncora numérica na abertura.
