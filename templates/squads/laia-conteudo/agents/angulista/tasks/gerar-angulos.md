---
task: "Gerar Ângulos"
order: 1
input: |
  - pesquisa: output/pesquisa.md (dados, saturação, recortes ausentes)
  - briefing_item: output/briefing-item.md (assunto, etapa de funil, formato, plataforma)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (público, percepção desejada)
output: |
  - angulos: 5 ou mais ângulos distintos classificados (output/angulos.yaml)
---

# Gerar Ângulos

Gera no mínimo cinco ângulos genuinamente distintos sobre **o mesmo** assunto. Ângulo é a
lente emocional pela qual o assunto é contado — não é subtema nem outra pauta.

## Process

1. **Isolar a tensão central do assunto** a partir da pesquisa: o fato mais contraintuitivo,
   surpreendente ou incômodo disponível. Todo ângulo é uma forma diferente de girar essa
   tensão.

2. **Gerar cinco lentes distintas.** Percorrer as lentes canônicas e escolher as que o
   material sustenta:
   - **Revelador** — o que está acontecendo e ninguém percebeu
   - **Erro comum** — o que a maioria faz errado
   - **Contraintuitivo** — o oposto do senso comum do nicho
   - **História** — o caso concreto, com começo, virada e consequência
   - **Números** — a dimensão que só aparece quando se mede
   - **Passo a passo** — o método, quando o valor está na execução
   - **Pergunta incômoda** — a dúvida que o público evita fazer

3. **Ancorar cada ângulo em dado da pesquisa.** Citar qual achado o sustenta. Ângulo sem
   lastro é opinião.

4. **Aplicar o teste de distinção.** Escrever mentalmente o slide 1 de cada ângulo. Se dois
   aceitam a mesma abertura sem estranheza, são duplicados — refazer um.

5. **Evitar os enquadramentos saturados** da pesquisa. Se usar um, o campo `diferenciador`
   precisa dizer o que o separa do que já circula.

6. **Classificar cada ângulo**: formato mais adequado, nível de provocação de 1 a 5, segmento
   do público, força e risco. Distribuir os níveis de provocação — não concentrar tudo em 4 e 5.

7. **Recomendar um ângulo** com justificativa ligada ao perfil: meta, percepção desejada ou
   dor. Quando o item do calendário pedir mais de um formato, indicar qual ângulo serve melhor
   a cada um.

## Output Format

```yaml
assunto: "{assunto do item}"
tensao_central: "{a virada que sustenta todos os ângulos}"

angulos:
  - id: 1
    titulo: "{2-5 palavras que capturam a lente}"
    lente: "revelador|erro-comum|contraintuitivo|historia|numeros|passo-a-passo|pergunta-incomoda"
    resumo: |
      {2-3 linhas: a tensão que esse ângulo explora e como ele a desenvolve}
    ancora_pesquisa: "{dado do relatório que sustenta o ângulo}"
    formato_indicado: "carrossel|post-linkedin"
    provocacao: 3
    segmento: "{parte do público que mais se identifica}"
    forca: "{por que funciona para esta audiência}"
    risco: "{o que pode dar errado — obrigatório se provocacao >= 4}"
    diferenciador: "{apenas se a lente estiver na lista de saturados}"

angulo_recomendado: 1
justificativa_recomendacao: "{ligada a meta, percepção desejada ou dor do perfil}"
```

## Output Example

> Referência de qualidade, não gabarito.

```yaml
assunto: "O orçamento que você reescreve 20 vezes por semana"
tensao_central: >
  Quem faz orçamento manual não perde tempo por falta de ferramenta — perde porque acha
  que cada orçamento é único, quando 80% deles é o mesmo texto com três variáveis.

angulos:
  - id: 1
    titulo: "As 11 horas invisíveis"
    lente: "numeros"
    resumo: |
      Quantifica o custo real da tarefa que ninguém contabiliza. O dono não percebe as 11h
      semanais porque elas vêm em fatias de 20 minutos espalhadas pela semana.
    ancora_pesquisa: "11h/semana em tarefas administrativas repetitivas em PME (2025-11, ALTA)"
    formato_indicado: "carrossel"
    provocacao: 2
    segmento: "Dono que sente que trabalha muito e não sabe onde o tempo vai"
    forca: "Número específico e verificável, alto poder de scroll-stop, baixo risco"
    risco: "Dado internacional — precisa ser declarado como tal no conteúdo"

  - id: 2
    titulo: "Os 20% que ninguém resolve"
    lente: "pergunta-incomoda"
    resumo: |
      Todo mundo fala em padronizar orçamento, ninguém fala do que fazer com os casos que
      não se encaixam no template. É exatamente onde quem tentou automatizar desistiu.
    ancora_pesquisa: "recorte ausente: 0 de 31 peças abordaram os casos não padronizáveis"
    formato_indicado: "post-linkedin"
    provocacao: 3
    segmento: "Quem já tentou automatizar e travou"
    forca: "Endereça a objeção real; nenhum concorrente cobriu no período"
    risco: "Exige conhecimento concreto do problema — não funciona com resposta genérica"

  - id: 3
    titulo: "Você não tem problema de ferramenta"
    lente: "contraintuitivo"
    resumo: |
      Contraria o senso comum do nicho: o gargalo não é falta de IA, é falta de processo.
      Quem instala ferramenta sobre processo bagunçado automatiza a bagunça.
    ancora_pesquisa: "4 em 10 empresas abandonam automação no 1º trimestre (2026-02, MÉDIA)"
    formato_indicado: "carrossel"
    provocacao: 4
    segmento: "Quem já comprou ferramenta e não usou"
    forca: "Se posiciona contra os 11 carrosséis de 'lista de ferramentas' do período"
    risco: "Pode soar como crítica a quem comprou ferramenta — o texto precisa acolher, não acusar"

  - id: 4
    titulo: "O escritório que respondeu no mesmo dia"
    lente: "historia"
    resumo: |
      Caso concreto de 6 pessoas que saiu de 3 dias para o mesmo dia de retorno. A virada
      não foi a tecnologia, foi decidir o que padronizar primeiro.
    ancora_pesquisa: "caso do escritório de arquitetura (fonte comercial, viés declarado)"
    formato_indicado: "carrossel"
    provocacao: 2
    segmento: "Empresa de serviço com equipe pequena"
    forca: "Case com antes/depois teve boa resposta no período"
    risco: "Fonte é material comercial de fornecedor — não usar como prova estatística"

  - id: 5
    titulo: "O erro de automatizar o texto errado"
    lente: "erro-comum"
    resumo: |
      A maioria automatiza o envio e mantém a escrita manual — inverte a ordem e economiza
      o passo errado, o que explica por que a sensação de ganho não aparece.
    ancora_pesquisa: "pergunta frequente #1: 'preciso saber programar?' revela foco na ferramenta"
    formato_indicado: "carrossel"
    provocacao: 3
    segmento: "Quem começou a automatizar sozinho"
    forca: "Reenquadra a dor sem confrontar o leitor"
    risco: "Exige exemplo concreto para não virar afirmação vaga"

angulo_recomendado: 3
justificativa_recomendacao: >
  A percepção desejada do perfil é "autoridade acessível — especialista que explica sem
  jargão", e o ângulo 3 é o que mais constrói autoridade: se posiciona contra o
  enquadramento saturado dominante do período (lista de ferramentas, 11 de 31 peças) com
  lastro em dado. Provocação 4 é compatível com a marca, desde que o texto acolha quem já
  comprou ferramenta em vez de acusar.
```

## Quality Criteria

- [ ] Mínimo de 5 ângulos, todos sobre o mesmo assunto
- [ ] Lentes distintas entre si; nenhum par aceita o mesmo slide de abertura
- [ ] Cada ângulo tem `ancora_pesquisa` apontando dado real do relatório
- [ ] Níveis de provocação distribuídos, não todos em 4 e 5
- [ ] `risco` preenchido em todo ângulo com provocação ≥ 4
- [ ] `diferenciador` presente em todo ângulo que use lente saturada
- [ ] Ângulo recomendado com justificativa ligada ao perfil

## Veto Conditions

Rejeitar e refazer se:
1. Foram gerados assuntos diferentes em vez de ângulos sobre o mesmo assunto
2. Dois ou mais ângulos são a mesma lente com redação diferente
3. Algum ângulo não tem lastro em dado da pesquisa
4. Menos de 5 ângulos
5. Ângulo com provocação ≥ 4 sem risco declarado
