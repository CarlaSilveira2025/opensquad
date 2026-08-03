---
step: "03"
name: "Geração de Ângulos"
type: agent
execution: inline
agent: angulista
tasks:
  - gerar-angulos
depends_on: step-02
inputFile: squads/laia-conteudo/output/pesquisa.md
outputFile: squads/laia-conteudo/output/angulos.yaml
---

# Step 03: Ângela Ângulo — Geração de Ângulos (Fase 3.2)

## Context Loading

Carregar antes de executar:

- `squads/laia-conteudo/output/pesquisa.md` — dados, saturação e recortes ausentes
- `squads/laia-conteudo/output/briefing-item.md` — assunto, etapa, formato, plataforma
- `_opensquad/_memory/clientes/{slug}/perfil.json` — público, percepção desejada, meta
- `squads/laia-conteudo/pipeline/data/domain-framework.md` — definição e lentes de ângulo
- `squads/laia-conteudo/pipeline/data/anti-patterns.md` — o erro de gerar pautas no lugar
  de ângulos

## Instructions

### Process

1. **Isolar a tensão central do assunto** a partir da pesquisa — o fato mais contraintuitivo
   ou incômodo disponível. Todos os ângulos giram essa mesma tensão.

2. **Gerar no mínimo 5 ângulos**, cada um usando uma lente distinta entre as sete canônicas
   (revelador, erro comum, contraintuitivo, história, números, passo a passo, pergunta
   incômoda). São cinco lentes sobre o **mesmo** assunto — cinco assuntos diferentes seriam
   pautas, não ângulos.

3. **Ancorar cada ângulo em dado do relatório**, citando qual achado o sustenta no campo
   `ancora_pesquisa`.

4. **Aplicar o teste de distinção.** Escrever mentalmente o slide 1 de cada ângulo; se dois
   aceitam a mesma abertura sem estranheza, refazer um deles.

5. **Evitar os enquadramentos saturados.** Se algum for usado, preencher `diferenciador` com
   o que o separa do que já circula.

6. **Classificar cada ângulo** com formato indicado, nível de provocação de 1 a 5, segmento,
   força e risco. Distribuir os níveis de provocação; declarar risco em todo ângulo ≥ 4.

7. **Recomendar um ângulo** com justificativa ligada ao perfil. Quando o item previr mais de
   um formato, indicar qual ângulo serve melhor a cada um.

## Output Format

```yaml
assunto: "{assunto do item}"
tensao_central: "{a virada que sustenta todos os ângulos}"

angulos:
  - id: 1
    titulo: "{2-5 palavras}"
    lente: "revelador|erro-comum|contraintuitivo|historia|numeros|passo-a-passo|pergunta-incomoda"
    resumo: |
      {2-3 linhas}
    ancora_pesquisa: "{dado do relatório}"
    formato_indicado: "carrossel|post-linkedin"
    provocacao: 3
    segmento: "{parte do público}"
    forca: "{por que funciona}"
    risco: "{obrigatório se provocacao >= 4}"
    diferenciador: "{apenas se a lente estiver saturada}"

angulo_recomendado: 1
justificativa_recomendacao: "{ligada a meta, percepção desejada ou dor}"
```

## Output Example

```yaml
assunto: "O orçamento que você reescreve 20 vezes por semana"
tensao_central: >
  Quem faz orçamento manual não perde tempo por falta de ferramenta — perde porque acha que
  cada orçamento é único, quando 80% deles é o mesmo texto com três variáveis.

angulos:
  - id: 1
    titulo: "As 11 horas invisíveis"
    lente: "numeros"
    resumo: |
      Quantifica o custo da tarefa que ninguém contabiliza. O dono não percebe as 11h
      semanais porque elas vêm em fatias de 20 minutos espalhadas pela semana.
    ancora_pesquisa: "11h/semana em tarefas administrativas em PME (2025-11, ALTA)"
    formato_indicado: "carrossel"
    provocacao: 2
    segmento: "Dono que sente que trabalha muito e não sabe onde o tempo vai"
    forca: "Número específico e verificável, alto scroll-stop, baixo risco"
    risco: "Dado internacional — declarar como tal no conteúdo"

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
    forca: "Se posiciona contra os 11 carrosséis de lista de ferramentas do período"
    risco: "Pode soar como crítica a quem comprou — o texto precisa acolher, não acusar"

angulo_recomendado: 3
justificativa_recomendacao: >
  A percepção desejada do perfil é "autoridade acessível". O ângulo 3 é o que mais constrói
  autoridade: se posiciona contra o enquadramento saturado dominante (11 de 31 peças) com
  lastro em dado.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Foram gerados assuntos diferentes em vez de ângulos sobre o mesmo assunto
2. Menos de 5 ângulos
3. Dois ou mais ângulos aceitam o mesmo slide de abertura
4. Algum ângulo não tem lastro em dado do relatório de pesquisa
5. Ângulo com provocação ≥ 4 sem risco declarado
6. Ângulo com lente saturada sem `diferenciador` preenchido

## Quality Criteria

- [ ] Mínimo de 5 ângulos sobre o mesmo assunto
- [ ] Lentes distintas entre si
- [ ] `ancora_pesquisa` preenchida em todos
- [ ] Níveis de provocação distribuídos, não todos em 4 e 5
- [ ] Segmento, força e risco preenchidos
- [ ] Ângulo recomendado com justificativa ligada ao perfil
- [ ] Indicação de qual ângulo serve a cada formato, quando houver mais de um
