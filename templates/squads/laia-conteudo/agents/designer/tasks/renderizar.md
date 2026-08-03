---
task: "Renderizar"
order: 3
input: |
  - slides_html: output/slides/slide-NN.html (todos os slides)
  - sistema_visual: output/sistema-visual.md (dimensões por peça)
output: |
  - imagens: PNGs prontos para postar (output/slides/rendered/slide-NN.png)
---

# Renderizar

Converte cada HTML em PNG na dimensão correta usando a skill `image-creator` (Playwright), e
confere o resultado antes de entregar.

## Process

1. **Renderizar cada arquivo HTML** com a skill `image-creator`, passando a viewport exata:
   1080×1440 para carrossel de Instagram, 1200×627 ou 1080×1080 para LinkedIn. Salvar em
   `output/slides/rendered/` com o mesmo nome-base do HTML.

2. **Conferir cada PNG gerado.** Verificar que a imagem existe, tem as dimensões esperadas e
   não está em branco. Renderização silenciosamente vazia é a falha mais comum.

3. **Inspecionar visualmente cada imagem** com a ferramenta Read, procurando três defeitos:
   texto cortado na borda, texto transbordando a viewport e contraste insuficiente. São os
   três que a inspeção do HTML não pega.

4. **Corrigir e re-renderizar** o slide defeituoso ajustando o HTML — nunca o texto. Máximo
   de 2 tentativas por slide; na terceira, reportar o slide como problemático em vez de
   entregar defeituoso.

5. **Conferir a ordem.** A numeração dos arquivos precisa corresponder à ordem de publicação
   do carrossel. Slide fora de ordem publicado é erro visível.

6. **Listar todos os arquivos gerados** com caminho, dimensão e tamanho, mais os que
   falharam e por quê.

## Output Format

```markdown
# Renderização — {assunto}

**Peças renderizadas:** {N} de {N}

## Carrossel Instagram (1080×1440)
| # | Arquivo | Dimensão | Status |

## Peça LinkedIn ({dimensão})
| Arquivo | Dimensão | Status |

## Ordem de publicação
1. `slide-01.png` — {resumo do conteúdo}

## Verificações
- [ ] Todas as imagens existem e não estão em branco
- [ ] Nenhum texto cortado ou transbordando
- [ ] Contraste conferido em todas

## Falhas
- {arquivo}: {problema e o que foi tentado}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Renderização — O orçamento que você reescreve 20 vezes por semana

**Peças renderizadas:** 9 de 9

## Carrossel Instagram (1080×1440)
| # | Arquivo | Dimensão | Status |
|---|---|---|---|
| 1 | `output/slides/rendered/slide-01.png` | 1080×1440 | ok |
| 2 | `output/slides/rendered/slide-02.png` | 1080×1440 | ok |
| 3 | `output/slides/rendered/slide-03.png` | 1080×1440 | ok — re-renderizado |
| 6 | `output/slides/rendered/slide-06.png` | 1080×1440 | ok |
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
6. `slide-06.png` — reflexão: automatizar bagunça acelera a bagunça
7. `slide-07.png` — CTA: escreve os 3 passos que você repete
8. `slide-08.png` — assinatura com logo

## Verificações
- [x] Todas as imagens existem e não estão em branco
- [x] Nenhum texto cortado ou transbordando
- [x] Contraste conferido — #FFFFFF sobre #1A1A2E em todos, #1A1A2E sobre #00D982 no CTA

## Falhas
- `slide-03.png` (1ª tentativa): o texto de apoio transbordou 40px abaixo da margem
  inferior. Corrigido reduzindo o corpo de 46px para 42px, dentro da escala definida no
  sistema visual. O texto não foi alterado. Re-renderizado com sucesso.
```

## Quality Criteria

- [ ] Todos os HTMLs renderizados
- [ ] Cada PNG com a dimensão correta da plataforma
- [ ] Nenhuma imagem em branco
- [ ] Cada imagem inspecionada visualmente
- [ ] Nenhum texto cortado ou transbordando
- [ ] Ordem de publicação listada
- [ ] Correções feitas no HTML, nunca no texto
- [ ] Falhas registradas com o que foi tentado

## Veto Conditions

Rejeitar e refazer se:
1. Alguma imagem esperada não foi gerada ou está em branco
2. Alguma imagem tem dimensão diferente da definida para a plataforma
3. Existe texto cortado ou transbordando em alguma imagem entregue
4. Algum texto foi alterado para resolver problema de layout
