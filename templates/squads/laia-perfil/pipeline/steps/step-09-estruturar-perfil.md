---
step: "09"
name: "Estruturação do Perfil"
type: agent
execution: inline
agent: perfilador
tasks:
  - estruturar-perfil
  - gerar-brand-book
depends_on: step-08
inputFile: squads/laia-perfil/output/respostas/lacunas-respondidas.md
outputFile: squads/laia-perfil/output/perfil.json
---

# Step 09: Priscila Perfil — Estruturação do Perfil

## Context Loading

Carregar antes de executar:

- `squads/laia-perfil/output/briefing-consolidado.md` — briefing normalizado do Step 07
- `squads/laia-perfil/output/lacunas.md` — lacunas com criticidade atribuída
- `squads/laia-perfil/output/respostas/lacunas-respondidas.md` — respostas do Step 08
- `squads/laia-perfil/output/cliente.md` — slug, nome e tipo do cadastro
- `squads/laia-perfil/pipeline/data/domain-framework.md` — schema canônico do `perfil.json`
- `squads/laia-perfil/pipeline/data/output-examples.md` — exemplos de perfil e brand book
- Em caso de retorno por `on_reject`: `squads/laia-perfil/output/validacao-perfil.md` — as
  correções apontadas pela Renata Revisão

## Instructions

### Process

1. **Aplicar as respostas de lacunas sobre o briefing.** Onde a resposta preenche um campo
   antes `PENDENTE`, usar o valor novo. Onde a lacuna ficou sem resposta, o campo permanece
   pendente — nunca preencher com valor plausível.

2. **Executar a task `estruturar-perfil`.** Instanciar todas as chaves do schema, converter
   tipos, normalizar cores para `#RRGGBB`, preencher o bloco `meta` e montar a lista
   `pendencias` com a criticidade herdada de `lacunas.md`. Validar o JSON antes de gravar em
   `squads/laia-perfil/output/perfil.json`.

3. **Executar a task `gerar-brand-book`.** Derivar exclusivamente do JSON as seis seções do
   documento e gravar em `squads/laia-perfil/output/brand-book.md`.

4. **Conferir espelhamento.** Percorrer o JSON campo a campo e verificar que cada valor
   preenchido aparece no brand book e que o brand book não afirma nada que o JSON não tenha.

5. **Se este for um retorno por `on_reject`**, tratar cada bloqueador do relatório de
   validação como item obrigatório: corrigir todos antes de reentregar, e listar no resumo
   qual correção foi aplicada em cada campo apontado.

6. **Apresentar o resumo** com contagem de campos preenchidos e pendentes e os caminhos dos
   dois arquivos gerados.

## Output Format

Dois arquivos. `perfil.json` segue o schema literal da task `estruturar-perfil`.
`brand-book.md` segue este template literal:

```markdown
# Brand Book — {nome}

_Gerado pelo sistema LAIA em {data} · perfil versão {versao_schema}_

## Quem é
## Para quem fala
## Como fala
## O que quer
## Como aparece
## O que ainda falta
### Crítico
### Importante / Opcional
```

## Output Example

```json
{
  "meta": {
    "slug": "authentic-studio",
    "nome": "Authentic Studio",
    "versao_schema": "1.0.0",
    "criado_em": "2026-08-02",
    "atualizado_em": "2026-08-02",
    "origem_run": "2026-08-02-153012"
  },
  "identidade": {
    "nome_marca": "Authentic Studio",
    "nicho": "Consultoria financeira para donos de pequenos negócios",
    "ofertas": [
      { "nome": "Diagnóstico financeiro", "promessa": "Saber quanto o negócio lucra de fato",
        "preco": "R$ 1.200 avulso" }
    ],
    "diferenciais": ["Trabalha com quem não entende de planilha"],
    "percepcao_desejada": "Profissional mas próxima"
  },
  "publico": {
    "quem_sao": "Donos de pequenos negócios de serviço, faturamento até R$ 100 mil/mês",
    "dores": [
      "Chega no fim do mês sem saber quanto lucrou",
      "Mistura conta pessoal com conta da empresa",
      "Aumenta faturamento e o dinheiro some do mesmo jeito"
    ],
    "desejos": ["Tirar pró-labore previsível", "Saber se pode contratar"],
    "onde_estao": ["Instagram", "LinkedIn"],
    "faixa_etaria": "28-45",
    "linguagem": "Direta, sem termo de contador"
  },
  "visual": {
    "logo": null,
    "paleta": [{ "nome": "Azul noite", "hex": "#12233A" },
               { "nome": "Dourado", "hex": "#C9A227" }],
    "tipografias": ["Poppins"],
    "estilo_imagem": "Clean, fundo claro",
    "elementos_graficos": [],
    "fotos_referencia": []
  },
  "pendencias": [
    { "campo": "visual.logo", "criticidade": "IMPORTANTE" },
    { "campo": "objetivos.historico_nao_funcionou", "criticidade": "IMPORTANTE" },
    { "campo": "visual.elementos_graficos", "criticidade": "OPCIONAL" }
  ]
}
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. O `perfil.json` não faz parse como JSON válido
2. Alguma chave do schema está ausente do documento
3. Existe hex de cor que o cliente não informou nem aprovou explicitamente
4. Um campo `null` não tem entrada correspondente em `pendencias`
5. O brand book afirma algo que contradiz o `perfil.json`
6. Em retorno por `on_reject`, algum bloqueador apontado na validação segue sem correção

## Quality Criteria

- [ ] JSON válido, com todas as chaves do schema e tipos corretos
- [ ] Listas são arrays mesmo quando têm um único item
- [ ] `meta.slug` idêntico ao definido no Step 01
- [ ] Brand book cobre as seis seções e espelha o JSON
- [ ] Resumo informa contagem de campos preenchidos e pendentes
- [ ] Caminhos dos dois arquivos apresentados ao usuário
