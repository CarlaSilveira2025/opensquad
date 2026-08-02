---
task: "Gerar Ganchos"
order: 1
input: |
  - angulos_selecionados: output/angulos-selecionados.yaml
  - pesquisa: output/pesquisa.md (dados com número e fonte)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (tom, palavras a evitar)
  - tom: pipeline/data/tone-of-voice.md
output: |
  - ganchos: 3 ganchos por ângulo aprovado, classificados (output/ganchos.yaml)
---

# Gerar Ganchos

Para cada ângulo aprovado, escreve três ganchos de tipos diferentes. O texto entregue é o
texto final — vai literal para o slide 1 ou para a primeira linha do post.

## Process

1. **Ler o ângulo e sua âncora de pesquisa.** O gancho precisa cumprir a promessa daquele
   ângulo específico, não do assunto em geral.

2. **Escolher três tipos diferentes** entre os cinco canônicos: pergunta provocativa,
   afirmação chocante, história, dado/estatística, contraintuitivo. Três do mesmo tipo são
   uma opção só.

3. **Escrever o texto exato de cada um.** Pronto para publicação, sem "algo como". Máximo de
   2 linhas visíveis. Para LinkedIn, conferir que cabe em ~200 caracteres, antes do "ver mais".

4. **Conferir os números.** Todo gancho do tipo dado usa número que existe no relatório de
   pesquisa, com a mesma grandeza e o mesmo recorte.

5. **Conferir as palavras proibidas.** Nenhum termo de `comunicacao.palavras_evitar` pode
   aparecer — é a frase mais visível do conteúdo.

6. **Escrever a abertura visual de cada gancho** em uma linha: a cena, a composição ou o
   elemento que acompanha aquele texto no slide 1 ou na imagem do post.

7. **Indicar o formato em que cada gancho funciona melhor** e recomendar um por ângulo.

## Output Format

```yaml
ganchos_por_angulo:
  - angulo_id: 1
    angulo_titulo: "{título do ângulo}"
    opcoes:
      - id: "1a"
        texto: |
          {texto exato, pronto para publicar}
        tipo: "pergunta|afirmacao|historia|dado|contraintuitivo"
        formato_indicado: "carrossel|post-linkedin"
        abertura_visual: "{cena ou composição em uma linha}"
        promessa: "{o que este gancho compromete o conteúdo a entregar}"
        caracteres: {contagem, relevante para LinkedIn}
    recomendado: "1a"
    justificativa: "{por que este entre os três}"
```

## Output Example

> Referência de qualidade, não gabarito.

```yaml
ganchos_por_angulo:
  - angulo_id: 3
    angulo_titulo: "Você não tem problema de ferramenta"
    opcoes:
      - id: "3a"
        texto: |
          4 em 10 empresas abandonam a automação no primeiro trimestre.
          Não é a ferramenta que falha.
        tipo: "dado"
        formato_indicado: "carrossel"
        abertura_visual: >
          Número "4 em 10" ocupando dois terços do slide em verde sinal sobre fundo
          grafite; a segunda linha em corpo menor, embaixo.
        promessa: "Explicar o que realmente falha quando a automação é abandonada"
        caracteres: 89

      - id: "3b"
        texto: |
          Você não tem problema de ferramenta. Tem problema de processo.
        tipo: "contraintuitivo"
        formato_indicado: "carrossel"
        abertura_visual: >
          Frase quebrada em duas linhas, a segunda em destaque de cor; sem imagem de apoio,
          só tipografia grande.
        promessa: "Mostrar por que instalar ferramenta sobre processo bagunçado não resolve"
        caracteres: 62

      - id: "3c"
        texto: |
          Comprei a ferramenta, configurei tudo, e três meses depois estava fazendo
          orçamento no Word de novo.
        tipo: "historia"
        formato_indicado: "post-linkedin"
        abertura_visual: >
          Sem imagem no primeiro momento — o texto carrega sozinho. Imagem de apoio entra
          como captura do processo mapeado.
        promessa: "Contar o que faltou naquela tentativa e o que mudaria hoje"
        caracteres: 104

    recomendado: "3b"
    justificativa: >
      É o mais curto, o mais legível em slide e o que melhor entrega a lente contraintuitiva
      do ângulo. O 3a é forte mas gasta o dado logo na capa, deixando o slide 2 sem escada.
      O 3c é o melhor para LinkedIn, e deve ser usado lá se o item também for para essa
      plataforma.
```

## Quality Criteria

- [ ] Exatamente 3 ganchos por ângulo aprovado
- [ ] Os 3 são de tipos diferentes entre os 5 canônicos
- [ ] Texto exato, pronto para publicar, sem esboço
- [ ] Nenhum gancho passa de 2 linhas visíveis
- [ ] Ganchos de LinkedIn com contagem de caracteres ≤ ~200
- [ ] Todo gancho de dado usa número presente na pesquisa
- [ ] Nenhuma palavra de `comunicacao.palavras_evitar`
- [ ] Abertura visual e promessa preenchidas em todos
- [ ] Um recomendado por ângulo, com justificativa

## Veto Conditions

Rejeitar e refazer se:
1. Dois ou mais ganchos do mesmo ângulo são do mesmo tipo
2. Algum gancho cita número que não existe no relatório de pesquisa
3. Algum gancho contém palavra da lista de proibidas do perfil
4. Algum gancho de LinkedIn passa de 200 caracteres
5. Alguma promessa não pode ser cumprida pelo ângulo correspondente
