---
task: "Estruturar Perfil"
order: 1
input: |
  - briefing_consolidado: output/briefing-consolidado.md
  - lacunas_respondidas: output/respostas/lacunas-respondidas.md (pode estar vazio)
  - cliente: output/cliente.md (nome, slug, tipo novo/atualização)
  - schema: pipeline/data/domain-framework.md
output: |
  - perfil: contrato de dados do cliente em JSON válido (output/perfil.json)
---

# Estruturar Perfil

Converte o briefing consolidado, já complementado pelas respostas de lacunas, no
`perfil.json` — o contrato de dados que alimenta os squads `laia-calendario` e
`laia-conteudo`. Fidelidade e estabilidade de schema são mais importantes que completude.

## Process

1. **Ler o briefing e as respostas de lacunas.** Onde a resposta de lacuna preencher um
   campo antes `PENDENTE`, usar a resposta nova. Onde a lacuna não foi respondida, o campo
   permanece pendente.

2. **Instanciar o schema completo.** Criar todas as chaves definidas em
   `pipeline/data/domain-framework.md`, na ordem do schema. Nenhuma chave pode faltar.

3. **Converter valores conforme o tipo do campo.** Strings simples para textos; arrays para
   listas (mesmo com um item); `null` para pendências. Preços permanecem strings com moeda
   e periodicidade ("R$ 890/mês"). Frequência como string padronizada ("3 por semana").

4. **Normalizar cores.** Cada cor da paleta vira `#RRGGBB` em maiúsculas. Cor citada apenas
   por nome, sem hex informado nem aprovado pelo cliente, vira entrada em
   `pendencias` com o rótulo `visual.paleta` — nunca um hex adivinhado.

5. **Preencher o bloco de metadados.** `slug`, `nome`, `criado_em`, `atualizado_em`,
   `versao_schema` e `origem_run`.

6. **Montar a lista de pendências.** Todo campo `null` ou lista vazia entra em `pendencias`
   com criticidade herdada de `output/lacunas.md`.

7. **Validar o JSON.** Conferir que o documento é sintaticamente válido antes de gravar.

## Output Format

```json
{
  "meta": {
    "slug": "string",
    "nome": "string",
    "versao_schema": "1.0.0",
    "criado_em": "YYYY-MM-DD",
    "atualizado_em": "YYYY-MM-DD",
    "origem_run": "string"
  },
  "identidade": {
    "nome_marca": "string|null",
    "nicho": "string|null",
    "ofertas": [{ "nome": "", "promessa": "", "preco": "" }],
    "diferenciais": [],
    "percepcao_desejada": "string|null"
  },
  "publico": {
    "quem_sao": "string|null",
    "dores": [],
    "desejos": [],
    "onde_estao": [],
    "faixa_etaria": "string|null",
    "linguagem": "string|null"
  },
  "comunicacao": {
    "tom_de_voz": "string|null",
    "palavras_usar": [],
    "palavras_evitar": [],
    "referencias": [{ "perfil": "", "o_que_admira": "" }]
  },
  "objetivos": {
    "meta_principal": "string|null",
    "ofertas_atuais": [],
    "historico_funcionou": [],
    "historico_nao_funcionou": [],
    "plataformas": [],
    "frequencia": "string|null"
  },
  "visual": {
    "logo": "string|null",
    "paleta": [{ "nome": "", "hex": "#RRGGBB" }],
    "tipografias": [],
    "estilo_imagem": "string|null",
    "elementos_graficos": [],
    "fotos_referencia": []
  },
  "pendencias": [{ "campo": "", "criticidade": "CRITICA|IMPORTANTE|OPCIONAL" }]
}
```

## Output Example

> Referência de qualidade, não gabarito.

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
    "nicho": "Automação e IA aplicada a pequenos negócios",
    "ofertas": [
      { "nome": "Implantação de agentes de IA", "promessa": "Rodando em 30 dias",
        "preco": "R$ 4.500 por projeto" },
      { "nome": "Mentoria de automação", "promessa": "Acompanhamento contínuo",
        "preco": "R$ 890/mês" }
    ],
    "diferenciais": ["Entrega funcionando, não só diagnóstico",
                     "Atende quem não é técnico"],
    "percepcao_desejada": "Autoridade acessível — especialista que explica sem jargão"
  },
  "publico": {
    "quem_sao": "Donos de pequenos negócios de serviço com 2 a 15 funcionários",
    "dores": ["Perde lead por demora na resposta", "Faz tudo manual e não escala",
              "Testou IA e não saiu do ChatGPT"],
    "desejos": ["Ter processo rodando sozinho", "Parecer maior do que é"],
    "onde_estao": ["Instagram", "Grupos de WhatsApp de empreendedorismo"],
    "faixa_etaria": "30-50",
    "linguagem": "Informal, direta, sem termos técnicos"
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
    { "campo": "objetivos.historico_nao_funcionou", "criticidade": "CRITICA" },
    { "campo": "visual.elementos_graficos", "criticidade": "OPCIONAL" }
  ]
}
```

## Quality Criteria

- [ ] JSON sintaticamente válido
- [ ] Todas as chaves do schema presentes, inclusive as nulas
- [ ] Nenhum valor inventado — ausência é `null` mais entrada em `pendencias`
- [ ] Cores em `#RRGGBB` maiúsculo ou registradas como pendência
- [ ] Listas sempre arrays, mesmo com um item
- [ ] `meta.slug` idêntico ao slug definido no step 01

## Veto Conditions

Rejeitar e refazer se:
1. O JSON não faz parse
2. Alguma chave do schema está ausente
3. Existe hex de cor que o cliente não informou nem aprovou
4. Um campo `null` não tem entrada correspondente em `pendencias`
