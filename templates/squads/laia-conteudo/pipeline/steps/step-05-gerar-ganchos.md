---
step: "05"
name: "Geração de Ganchos"
type: agent
execution: inline
agent: ganchista
tasks:
  - gerar-ganchos
depends_on: step-04
inputFile: squads/laia-conteudo/output/angulos-selecionados.yaml
outputFile: squads/laia-conteudo/output/ganchos.yaml
---

# Step 05: Gabriel Gancho — Geração de Ganchos (Fase 3.3)

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/angulos-selecionados.yaml` — ângulos aprovados e ajustes
- `squads/laia-conteudo/output/pesquisa.md` — números exatos, para os ganchos de dado
- `_opensquad/_memory/clientes/{slug}/perfil.json` — tom de voz e `palavras_evitar`
- `squads/laia-conteudo/pipeline/data/tone-of-voice.md` — calibragem de registro
- `squads/laia-conteudo/pipeline/data/domain-framework.md` — os 5 tipos canônicos de gancho

## Instructions

### Process

1. **Para cada ângulo aprovado, escrever exatamente 3 ganchos**, cada um de um tipo
   diferente entre os cinco canônicos: pergunta provocativa, afirmação chocante, história,
   dado/estatística, contraintuitivo.

2. **Escrever o texto final, não esboço.** O que sai daqui vai literal para o slide 1 ou
   para a primeira linha do post. Máximo de 2 linhas visíveis.

3. **Conferir os números.** Todo gancho de dado usa número que existe no relatório de
   pesquisa, com a mesma grandeza e o mesmo recorte. Número aproximado ou arredondado para
   soar melhor é violação.

4. **Contar caracteres nos ganchos de LinkedIn.** Precisam caber em ~210 caracteres, antes do
   corte do "ver mais", e fazer sentido isolados.

5. **Conferir `palavras_evitar`.** É a frase mais visível do conteúdo; nenhuma palavra
   proibida pode aparecer.

6. **Escrever a abertura visual de cada gancho** em uma linha — a cena ou composição que o
   acompanha — e a promessa que ele faz.

7. **Recomendar um gancho por ângulo**, justificando entre os três.

## Output Format

```yaml
ganchos_por_angulo:
  - angulo_id: 3
    angulo_titulo: "{título}"
    opcoes:
      - id: "3a"
        texto: |
          {texto exato, pronto para publicar}
        tipo: "pergunta|afirmacao|historia|dado|contraintuitivo"
        formato_indicado: "carrossel|post-linkedin"
        abertura_visual: "{cena ou composição}"
        promessa: "{o que compromete o conteúdo a entregar}"
        caracteres: {contagem}
    recomendado: "3a"
    justificativa: "{por que este entre os três}"
```

## Output Example

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
          Número "4 em 10" ocupando dois terços do slide em verde sinal sobre grafite;
          segunda linha em corpo menor, embaixo.
        promessa: "Explicar o que realmente falha quando a automação é abandonada"
        caracteres: 89

      - id: "3b"
        texto: |
          Você não tem problema de ferramenta. Tem problema de processo.
        tipo: "contraintuitivo"
        formato_indicado: "carrossel"
        abertura_visual: >
          Frase em duas linhas, a segunda em destaque de cor, só tipografia grande.
        promessa: "Mostrar por que ferramenta sobre processo bagunçado não resolve"
        caracteres: 62

      - id: "3c"
        texto: |
          Comprei a ferramenta, configurei tudo, e três meses depois estava fazendo
          orçamento no Word de novo.
        tipo: "historia"
        formato_indicado: "post-linkedin"
        abertura_visual: >
          Sem imagem na abertura — o texto carrega sozinho; imagem de apoio entra como
          captura do processo mapeado.
        promessa: "Contar o que faltou naquela tentativa e o que mudaria hoje"
        caracteres: 104

    recomendado: "3b"
    justificativa: >
      É o mais curto, o mais legível em slide e o que melhor entrega a lente contraintuitiva.
      O 3a gasta o dado logo na capa e deixa o slide 2 sem escada. O 3c é o melhor para
      LinkedIn e deve ser usado lá, se o item também for para essa plataforma.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Algum ângulo recebeu número de ganchos diferente de 3
2. Dois ou mais ganchos do mesmo ângulo são do mesmo tipo
3. Algum gancho de dado cita número que não existe no relatório de pesquisa
4. Algum gancho contém palavra de `comunicacao.palavras_evitar`
5. Algum gancho de LinkedIn passa de ~210 caracteres
6. Alguma promessa não pode ser cumprida pelo ângulo correspondente

## Quality Criteria

- [ ] 3 ganchos por ângulo, de tipos diferentes
- [ ] Texto exato, pronto para publicar
- [ ] Nenhum gancho com mais de 2 linhas visíveis
- [ ] Contagem de caracteres presente nos ganchos de LinkedIn
- [ ] Abertura visual e promessa preenchidas em todos
- [ ] Um recomendado por ângulo, com justificativa comparativa
- [ ] Nenhuma fórmula batida ("você sabia que", "neste post vou te contar")
