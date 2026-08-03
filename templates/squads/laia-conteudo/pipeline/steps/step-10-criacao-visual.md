---
step: "10"
name: "Criação Visual"
type: agent
execution: inline
agent: designer
format: image-design
tasks:
  - definir-sistema-visual
  - criar-slides-html
  - renderizar
depends_on: step-09
inputFile: squads/laia-conteudo/output/carrossel.md
outputFile: squads/laia-conteudo/output/sistema-visual.md
---

# Step 10: Davi Design — Criação Visual (Fase 3.5)

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/carrossel.md` — texto aprovado e indicação visual por slide
- `squads/laia-conteudo/output/linkedin.md` — peça visual sugerida, se existir
- `_opensquad/_memory/clientes/{slug}/perfil.json` — paleta, tipografias, logo, estilo
- `_opensquad/_memory/clientes/{slug}/assets/` — arquivos de logo e fotos
- `squads/laia-conteudo/pipeline/data/domain-framework.md` — dimensões por plataforma
- `squads/laia-conteudo/pipeline/data/anti-patterns.md` — erros visuais conhecidos

## Instructions

### Process

1. **Executar `definir-sistema-visual`.** Antes de qualquer slide, verificar que
   `visual.paleta` tem no mínimo 2 hex válidos. Se não tiver, **parar e reportar** — não
   escolher cor. Definir papéis de cor, escala tipográfica (nada abaixo de 34px), grid e
   tratamento por tipo de slide. Salvar em `squads/laia-conteudo/output/sistema-visual.md`.

2. **Verificar os assets.** Conferir se o arquivo apontado por `visual.logo` existe. Se não
   existir, seguir sem logo e registrar no relatório.

3. **Executar `criar-slides-html`.** Um HTML autocontido por slide, sem nenhuma referência de
   rede, com dimensões fixas: 1080×1440 para carrossel de Instagram, 1200×627 ou 1080×1080
   para LinkedIn. O texto aprovado entra literal.

4. **Se o texto não couber, ajustar o design — nunca o texto.** Reduzir o corpo dentro da
   escala, aumentar a área útil ou mudar a composição.

5. **Executar `renderizar`.** Converter cada HTML em PNG via `image-creator` na viewport
   correta, salvando em `squads/laia-conteudo/output/slides/rendered/`.

6. **Inspecionar cada imagem** com a ferramenta Read, procurando texto cortado, texto
   transbordando e contraste insuficiente. Corrigir no HTML e re-renderizar; máximo de 2
   tentativas por slide.

7. **Listar todos os arquivos gerados** com caminho, dimensão e ordem de publicação.

## Output Format

Três saídas. `sistema-visual.md` segue o formato da task correspondente; os HTMLs ficam em
`output/slides/`; os PNGs em `output/slides/rendered/`. O relatório apresentado ao usuário
segue este template:

```markdown
# Criação Visual — {assunto}

**Peças renderizadas:** {N} de {N}

## Sistema visual aplicado
| Papel | Hex | Origem |
| Escala | {tamanhos} |

## Carrossel Instagram (1080×1440)
| # | Arquivo | Dimensão | Status |

## Peça LinkedIn ({dimensão})
| Arquivo | Dimensão | Status |

## Ordem de publicação
1. `slide-01.png` — {resumo}

## Restrições e falhas
- {problema, efeito e o que foi feito}
```

## Output Example

```markdown
# Criação Visual — O orçamento que você reescreve 20 vezes por semana

**Peças renderizadas:** 9 de 9

## Sistema visual aplicado
| Papel | Hex | Origem |
|---|---|---|
| Fundo | #1A1A2E | visual.paleta — Grafite |
| Texto principal | #FFFFFF | neutro puro |
| Destaque | #00D982 | visual.paleta — Verde sinal |
| Texto secundário | #A0A0B8 | derivado do grafite |

**Escala:** capa 96px · título 72px · corpo 46px · rodapé 34px — fonte Inter
**Grid:** viewport 1080×1440, margem 96px, logo inferior direito 120px

## Carrossel Instagram (1080×1440)
| # | Arquivo | Dimensão | Status |
|---|---|---|---|
| 1 | `output/slides/rendered/slide-01.png` | 1080×1440 | ok |
| 2 | `output/slides/rendered/slide-02.png` | 1080×1440 | ok |
| 3 | `output/slides/rendered/slide-03.png` | 1080×1440 | ok — re-renderizado |
| 7 | `output/slides/rendered/slide-07.png` | 1080×1440 | ok |
| 8 | `output/slides/rendered/slide-08.png` | 1080×1440 | ok |

## Peça LinkedIn (1200×627)
| Arquivo | Dimensão | Status |
|---|---|---|
| `output/slides/rendered/linkedin-01.png` | 1200×627 | ok |

## Ordem de publicação
1. `slide-01.png` — capa: "Você não tem problema de ferramenta"
2. `slide-02.png` — dado: 4 em 10 empresas abandonam
3. `slide-03.png` — a causa: processo não desenhado
7. `slide-07.png` — CTA: escreve os 3 passos
8. `slide-08.png` — assinatura com logo

## Restrições e falhas
- `slide-03` (1ª tentativa): texto de apoio transbordou 40px abaixo da margem. Corrigido
  reduzindo o corpo de 46px para 42px, dentro da escala. O texto não foi alterado.
- `visual.elementos_graficos` vazio no perfil: os slides usam apenas tipografia e cor. Não
  bloqueia, mas reduz a distintividade visual frente a outros perfis do nicho.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Alguma cor usada não vem de `visual.paleta` nem é neutro puro
2. `visual.paleta` tem menos de 2 hex válidos e o step seguiu mesmo assim
3. Alguma palavra do texto aprovado foi cortada, abreviada ou reescrita
4. Alguma fonte está abaixo de 34px
5. Algum HTML referencia recurso externo por URL
6. Alguma imagem esperada não foi gerada, está em branco ou com dimensão errada
7. Existe texto cortado ou transbordando em imagem entregue

## Quality Criteria

- [ ] Sistema visual definido antes do primeiro slide e aplicado a todos
- [ ] Existência do arquivo de logo verificada
- [ ] HTMLs autocontidos, sem referência de rede
- [ ] Dimensões corretas por plataforma
- [ ] Cada imagem inspecionada visualmente
- [ ] Correções feitas no HTML, nunca no texto
- [ ] Ordem de publicação listada
- [ ] Restrições e falhas registradas com o que foi feito
