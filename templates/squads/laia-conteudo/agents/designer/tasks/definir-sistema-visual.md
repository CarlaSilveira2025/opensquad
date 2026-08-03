---
task: "Definir Sistema Visual"
order: 1
input: |
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (paleta, tipografias, estilo, logo)
  - carrossel: output/carrossel.md (número de slides e tipo de conteúdo de cada um)
  - linkedin: output/linkedin.md (peça visual sugerida)
output: |
  - sistema_visual: regras aplicadas a todos os slides (output/sistema-visual.md)
---

# Definir Sistema Visual

Define uma vez as regras que valem para todas as peças do conteúdo: escala tipográfica,
grid, uso de cor, tratamento de destaque e composição por tipo de slide. É o que garante
consistência — carrossel com slides visualmente diferentes parece amador.

## Process

1. **Ler a identidade visual do perfil.** Verificar que `visual.paleta` tem no mínimo 2 cores
   com hex válido. Se não tiver, **parar e reportar** — não escolher cor por conta própria.

2. **Definir os papéis de cor:** fundo, texto principal, destaque, texto secundário. Cada
   papel recebe um hex da paleta. Verificar contraste entre fundo e texto principal — se for
   insuficiente, inverter os papéis em vez de introduzir cor nova.

3. **Definir a escala tipográfica** em px, para peça de 1080px de largura:
   - Título de capa: 88-110px
   - Título de slide: 64-80px
   - Corpo: 40-52px
   - Legenda/rodapé: 32-36px (mínimo absoluto)
   Nenhum tamanho abaixo de 34px.

4. **Definir o grid:** margem externa (mínimo 80px em peça de 1080px), alinhamento padrão e
   posição fixa do logo e do número do slide.

5. **Definir o tratamento por tipo de conteúdo**, a partir das indicações visuais do
   carrossel: número dominante, lista, citação, comparação, texto puro.

6. **Verificar os assets.** Conferir se `visual.logo` aponta para arquivo existente em
   `_opensquad/_memory/clientes/{slug}/assets/`. Se não existir, registrar e seguir sem logo.

7. **Registrar tudo em valores concretos** — px, hex, peso — nunca em adjetivos.

## Output Format

```markdown
# Sistema Visual — {assunto}

**Cliente:** {slug} · **Peças:** {N} slides IG + {N} peça LinkedIn

## Papéis de cor
| Papel | Hex | Origem no perfil |
| Contraste fundo/texto | {avaliação} |

## Escala tipográfica
| Uso | Tamanho | Peso | Fonte |

## Grid
- Viewport: {largura}×{altura}px
- Margem externa: {px}
- Alinhamento: {padrão}
- Logo: {posição e tamanho}

## Tratamento por tipo de slide
| Tipo | Composição |

## Assets
- Logo: {caminho} | ausente
- Fontes: {nome} | fallback {nome}

## Restrições detectadas
- {problema de identidade visual e efeito prático}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Sistema Visual — O orçamento que você reescreve 20 vezes por semana

**Cliente:** laia · **Peças:** 8 slides IG (1080×1440) + 1 peça LinkedIn (1200×627)

## Papéis de cor
| Papel | Hex | Origem no perfil |
|---|---|---|
| Fundo | #1A1A2E | visual.paleta — Grafite |
| Texto principal | #FFFFFF | branco puro, permitido como neutro |
| Destaque | #00D982 | visual.paleta — Verde sinal |
| Texto secundário | #A0A0B8 | derivado do grafite por clareamento |

**Contraste fundo/texto:** #FFFFFF sobre #1A1A2E — alto, legível em mobile e sob sol.

## Escala tipográfica
| Uso | Tamanho | Peso | Fonte |
|---|---|---|---|
| Título de capa | 96px | 800 | Inter |
| Título de slide | 72px | 700 | Inter |
| Corpo | 46px | 400 | Inter |
| Rodapé | 34px | 500 | Inter |

## Grid
- Viewport: 1080×1440px
- Margem externa: 96px em todos os lados
- Alinhamento: texto à esquerda, bloco centralizado verticalmente
- Logo: canto inferior direito, 120px de largura, apenas na capa e no slide final

## Tratamento por tipo de slide
| Tipo | Composição |
|---|---|
| Capa | título 96px, sem elemento gráfico, muito espaço vazio |
| Número dominante | número em 200px verde sinal ocupando 2/3, texto de apoio embaixo |
| Texto puro | corpo 46px centralizado verticalmente, máximo 5 linhas |
| Reflexão | frase centralizada, margem ampliada para 140px, sem elemento gráfico |
| CTA | fundo invertido (#00D982), texto em #1A1A2E |

## Assets
- Logo: `_opensquad/_memory/clientes/laia/assets/logo.png` — presente
- Fontes: Inter (do perfil); fallback: system-ui, sans-serif

## Restrições detectadas
- `visual.elementos_graficos` está vazio no perfil: os slides usam apenas tipografia e cor,
  sem elementos gráficos próprios da marca. Não é bloqueador, mas reduz a distintividade
  visual em relação a outros perfis do nicho.
```

## Quality Criteria

- [ ] Todas as cores vêm de `visual.paleta` (neutros puros permitidos)
- [ ] Contraste fundo/texto avaliado explicitamente
- [ ] Nenhum tamanho de fonte abaixo de 34px
- [ ] Grid com viewport, margem, alinhamento e posições fixas
- [ ] Tratamento definido para cada tipo de slide presente no carrossel
- [ ] Existência do arquivo de logo verificada
- [ ] Tudo expresso em valores concretos, não adjetivos

## Veto Conditions

Rejeitar e refazer se:
1. Alguma cor usada não vem da paleta do perfil nem é neutro puro
2. `visual.paleta` tem menos de 2 hex válidos e a task seguiu mesmo assim
3. Algum tamanho de fonte está abaixo de 34px
4. Alguma decisão está descrita por adjetivo em vez de valor
