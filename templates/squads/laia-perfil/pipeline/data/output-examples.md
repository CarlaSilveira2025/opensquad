# Output Examples — Perfil de Cliente LAIA

Exemplos completos de saída final do squad. Referência de qualidade e profundidade — nunca
gabarito a ser copiado.

---

## Exemplo 1 — Perfil forte (0 bloqueadores, 2 pendências)

### `perfil.json`

```json
{
  "meta": {
    "slug": "laia",
    "nome": "LAIA",
    "versao_schema": "1.0.0",
    "criado_em": "2026-08-02",
    "atualizado_em": "2026-08-02",
    "origem_run": "2026-08-02-141530"
  },
  "identidade": {
    "nome_marca": "LAIA",
    "nicho": "Automação e IA aplicada a pequenos negócios de serviço",
    "ofertas": [
      { "nome": "Implantação de agentes de IA", "promessa": "Rodando em 30 dias",
        "preco": "R$ 4.500 por projeto" },
      { "nome": "Mentoria de automação", "promessa": "Acompanhamento mensal",
        "preco": "R$ 890/mês" }
    ],
    "diferenciais": [
      "Entrega o processo funcionando, não só o diagnóstico",
      "Atende quem não é técnico, sem exigir vocabulário de TI"
    ],
    "percepcao_desejada": "Autoridade acessível — especialista que explica sem jargão"
  },
  "publico": {
    "quem_sao": "Donos de pequenos negócios de serviço com 2 a 15 funcionários",
    "dores": [
      "Perde lead porque demora um dia pra responder no WhatsApp",
      "Faz orçamento manual e repete o mesmo texto 20 vezes por semana",
      "Testou IA, parou no ChatGPT e não conseguiu colocar em processo"
    ],
    "desejos": ["Ter processo rodando sem depender dele", "Parecer maior do que é"],
    "onde_estao": ["Instagram", "Grupos de WhatsApp de empreendedorismo"],
    "faixa_etaria": "30-50",
    "linguagem": "Informal, direta, sem termos técnicos"
  },
  "comunicacao": {
    "tom_de_voz": "Didático e direto, com exemplo concreto antes da explicação",
    "palavras_usar": ["processo", "na prática", "rodando", "sem enrolação"],
    "palavras_evitar": ["disruptivo", "revolucionário", "solução inovadora"],
    "referencias": [
      { "perfil": "@exemplo", "o_que_admira": "Abre com número e explica em 3 frases" }
    ]
  },
  "objetivos": {
    "meta_principal": "leads",
    "ofertas_atuais": ["Implantação de agentes de IA"],
    "historico_funcionou": ["Carrossel com print de automação real rodando"],
    "historico_nao_funcionou": ["Post motivacional sobre futuro do trabalho — 0 comentários"],
    "plataformas": ["Instagram", "LinkedIn"],
    "frequencia": "4 por semana"
  },
  "visual": {
    "logo": "_opensquad/_memory/clientes/laia/assets/logo.png",
    "paleta": [{ "nome": "Grafite", "hex": "#1A1A2E" },
               { "nome": "Verde sinal", "hex": "#00D982" }],
    "tipografias": ["Inter"],
    "estilo_imagem": "Bold, alto contraste, fundo escuro",
    "elementos_graficos": [],
    "fotos_referencia": []
  },
  "pendencias": [
    { "campo": "visual.elementos_graficos", "criticidade": "OPCIONAL" },
    { "campo": "visual.fotos_referencia", "criticidade": "OPCIONAL" }
  ]
}
```

### Trecho do `brand-book.md` correspondente

```markdown
# Brand Book — LAIA

_Gerado pelo sistema LAIA em 2026-08-02 · perfil versão 1.0.0_

## Quem é
Automação e IA aplicada a pequenos negócios de serviço. Quer ser percebida como
autoridade acessível — especialista que explica sem jargão.

**Ofertas**
- Implantação de agentes de IA — rodando em 30 dias (R$ 4.500 por projeto)
- Mentoria de automação — acompanhamento mensal (R$ 890/mês)

**Diferenciais:** entrega o processo funcionando, não só o diagnóstico · atende quem
não é técnico, sem exigir vocabulário de TI

## Como aparece
**Paleta:** Grafite `#1A1A2E` · Verde sinal `#00D982`
**Tipografia:** Inter · **Estilo:** bold, alto contraste, fundo escuro

## O que ainda falta
### Crítico
Nenhum.
### Importante / Opcional
- `visual.elementos_graficos`
- `visual.fotos_referencia`
```

---

## Exemplo 2 — Perfil incompleto que ainda assim é operável

Cliente que respondeu bem os blocos 1 a 4 e travou no bloco 5.

**Resultado:** 0 bloqueadores porque o usuário aprovou os hex propostos no checkpoint 06;
4 pendências toleráveis (logo, tipografias, elementos gráficos, fotos).

**Efeito prático registrado no brand book:**

```markdown
## O que ainda falta
### Crítico
Nenhum.
### Importante / Opcional
- `visual.logo` — os carrosséis saem sem logo no slide de assinatura até o arquivo ser
  colocado em `_opensquad/_memory/clientes/{slug}/assets/`
- `visual.tipografias` — o gerador usa a fonte padrão do template
- `objetivos.historico_nao_funcionou` — o primeiro mês roda em modo exploratório
```

**Leitura:** perfil aprovado com ressalva. A produção começa; as pendências viram uma
atualização de perfil depois do primeiro mês, quando o cliente já tem dado de performance.

---

## Exemplo 3 — Caso de reprovação legítima

Cliente respondeu tudo, mas:

- `publico.dores` = `["falta de organização", "falta de tempo"]` → 2 itens e ambos são
  adjetivos, não situações. **Bloqueador duplo** (quantidade e qualidade).
- `visual.paleta` = 1 cor com hex.  **Bloqueador.**

**Veredito:** REPROVADO, 3 bloqueadores. Volta ao Step 09 com correções acionáveis. Não é
falha do cliente — é o processo funcionando: melhor descobrir agora do que depois de um mês
de conteúdo genérico publicado.
