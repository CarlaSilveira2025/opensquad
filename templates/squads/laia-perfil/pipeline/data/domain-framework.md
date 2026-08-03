# Domain Framework — Perfil de Cliente LAIA

Framework operacional da Fase 1.1. Define o schema canônico do `perfil.json`, que é o
contrato de dados consumido pelos squads `laia-calendario` e `laia-conteudo`.

**Regra de ouro:** este schema é versionado. Renomear ou remover um campo quebra os squads
consumidores. Ao evoluir, incrementar `meta.versao_schema` e atualizar os dois squads.

---

## 1. Schema canônico do `perfil.json`

### `meta`
| Campo | Tipo | Obrigatório | Observação |
|---|---|---|---|
| `slug` | string | sim | minúsculas, sem acento, hífen no lugar de espaço |
| `nome` | string | sim | nome de exibição da marca |
| `versao_schema` | string | sim | atualmente `1.0.0` |
| `criado_em` | string `YYYY-MM-DD` | sim | data do primeiro cadastro |
| `atualizado_em` | string `YYYY-MM-DD` | sim | data desta versão |
| `origem_run` | string | sim | `run_id` que gerou esta versão |

### `identidade`
| Campo | Tipo | Mínimo | Observação |
|---|---|---|---|
| `nome_marca` | string\|null | — | **bloqueador** quando `nicho` também falta |
| `nicho` | string\|null | — | **bloqueador** |
| `ofertas` | array de `{nome, promessa, preco}` | 1 | **bloqueador** |
| `diferenciais` | array de string | 1 | |
| `percepcao_desejada` | string\|null | — | como quer ser percebida |

### `publico`
| Campo | Tipo | Mínimo | Observação |
|---|---|---|---|
| `quem_sao` | string\|null | — | **bloqueador** |
| `dores` | array de string | 3 | **bloqueador** — cada item é situação, não adjetivo |
| `desejos` | array de string | 1 | |
| `onde_estao` | array de string | 1 | redes, grupos, comunidades |
| `faixa_etaria` | string\|null | — | formato `28-45` |
| `linguagem` | string\|null | — | como o público fala |

### `comunicacao`
| Campo | Tipo | Mínimo | Observação |
|---|---|---|---|
| `tom_de_voz` | string\|null | — | **bloqueador**; ideal com amostra de voz real |
| `palavras_usar` | array de string | 0 | lista vazia é resposta válida |
| `palavras_evitar` | array de string | 0 | lista vazia é resposta válida |
| `referencias` | array de `{perfil, o_que_admira}` | 0 | |

### `objetivos`
| Campo | Tipo | Mínimo | Observação |
|---|---|---|---|
| `meta_principal` | string\|null | — | **bloqueador**; uma só meta dominante |
| `ofertas_atuais` | array de string | 0 | deve referenciar `identidade.ofertas` |
| `historico_funcionou` | array de string | 0 | alimenta o feedback loop |
| `historico_nao_funcionou` | array de string | 0 | alimenta o feedback loop |
| `plataformas` | array de string | 1 | **bloqueador**; `Instagram` e/ou `LinkedIn` |
| `frequencia` | string\|null | — | **bloqueador**; formato `N por semana` |

### `visual`
| Campo | Tipo | Mínimo | Observação |
|---|---|---|---|
| `logo` | string\|null | — | caminho do arquivo no registro de clientes |
| `paleta` | array de `{nome, hex}` | 2 | **bloqueador**; hex `#RRGGBB` maiúsculo |
| `tipografias` | array de string | 0 | |
| `estilo_imagem` | string\|null | — | clean · colorido · minimalista · bold |
| `elementos_graficos` | array de string | 0 | |
| `fotos_referencia` | array de string | 0 | caminhos de arquivo |

### `pendencias`
Array de `{campo, criticidade}`, onde `criticidade` ∈ `CRITICA` · `IMPORTANTE` · `OPCIONAL`.
Todo campo `null` ou array abaixo do mínimo tem entrada correspondente aqui.

---

## 2. Os cinco blocos de coleta

| Bloco | Step | Alimenta | Campo mais determinante |
|---|---|---|---|
| 1 — Identidade | 02 | `identidade` | `ofertas` |
| 2 — Público-Alvo | 03 | `publico` | `dores` (mín. 3) |
| 3 — Comunicação | 04 | `comunicacao` | amostra de voz real |
| 4 — Objetivos | 05 | `objetivos` | `historico_nao_funcionou` |
| 5 — Assets Visuais | 06 | `visual` | `paleta` com hex |

---

## 3. Método de consolidação

1. **Transporte fiel.** O valor gravado é o que o cliente disse, normalizado de formato —
   nunca reinterpretado de conteúdo.
2. **Ausência explícita.** Campo sem informação vira `PENDENTE` no briefing e `null` no JSON,
   com entrada em `pendencias`. Nunca valor plausível.
3. **Adjetivo exige exemplo.** "Descontraído", "jovem", "clean" só viram campo utilizável
   acompanhados de exemplo concreto, referência ou contra-exemplo.
4. **Contradição vira pergunta.** Conflito entre blocos nunca é resolvido silenciosamente.
5. **Verificação quando há URL.** Site e perfis públicos informados são conferidos; a
   divergência entre o declarado e o observado é registrada, não corrigida.

---

## 4. Classificação de lacunas

| Criticidade | Definição | Efeito |
|---|---|---|
| `CRITICA` | Bloqueia Camada 2 ou 3 | Reprova na validação |
| `IMPORTANTE` | Degrada qualidade, não impede produzir | Aprovado com ressalva |
| `OPCIONAL` | Refinamento | Registrada, sem efeito |

Limite: **8 perguntas por rodada**. Todas as críticas entram; o restante preenche por
impacto; o excedente vai para "Fica para depois".

---

## 5. Registro de clientes

```
_opensquad/_memory/clientes/{slug}/
├── perfil.json                       ← contrato lido pelas Camadas 2 e 3
├── brand-book.md                     ← versão legível para conferência
├── assets/                           ← logo e fotos (upload manual do usuário)
└── historico/
    ├── perfil-{YYYY-MM-DD}.json      ← versões anteriores
    └── brand-book-{YYYY-MM-DD}.md
```

Multi-cliente por construção: cada slug é um diretório isolado, o que sustenta a evolução
do sistema para o modelo de agência (V2) sem mudança de arquitetura.
