---
task: "Montar Calendário"
order: 2
input: |
  - grade: saída da task distribuir-funil (slots com etapa, formato, plataforma)
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json (dores, ofertas, objetivos)
  - pesquisa: output/pesquisa-mensal.md (achados, lacunas, saturação)
  - ajustes: output/ajustes-pesquisa.md (direcionamento do usuário no checkpoint 03)
output: |
  - calendario_yaml: calendário estruturado (output/calendario.yaml)
  - calendario_md: calendário legível em tabela (output/calendario.md)
---

# Montar Calendário

Preenche cada slot da grade com assunto e justificativa. É aqui que a pesquisa vira plano:
cada item precisa apontar para uma dor do perfil, um achado datado ou um objetivo declarado.

## Process

1. **Listar as fontes de tema disponíveis**, em ordem de prioridade:
   (a) lacunas editoriais da pesquisa — maior valor, ninguém está cobrindo;
   (b) dores do perfil ainda não endereçadas no mês;
   (c) achados de tendência com confiança ALTA ou MÉDIA;
   (d) ganchos sazonais com conexão concreta;
   (e) formatos que o feedback brief apontou como de melhor desempenho.

2. **Preencher os slots de fundo primeiro.** São os mais restritos: cada um precisa nomear
   uma oferta específica de `identidade.ofertas`. Distribuir as ofertas entre eles em vez de
   repetir a mesma.

3. **Preencher os slots de meio.** Prova social, bastidor, autoridade e caso. Marcar os que
   dependem de asset do cliente conforme a grade.

4. **Preencher os slots de topo** com as lacunas e tendências restantes, garantindo que
   nenhuma dor do perfil fique sem cobertura no mês, quando o volume permitir.

5. **Escrever a justificativa de cada item**, citando explicitamente a origem: nome da dor,
   achado com data, ou objetivo. Justificativa que descreve o próprio tema é inválida.

6. **Verificar repetição.** Nenhum assunto se repete. Dois itens sobre a mesma dor só
   coexistem com ângulos e formatos declaradamente diferentes.

7. **Evitar os temas saturados** listados na pesquisa. Se um tema saturado for usado mesmo
   assim, a justificativa precisa explicar qual ângulo o diferencia do que já circula.

8. **Gerar os dois arquivos**: `calendario.yaml` para consumo do squad de produção e
   `calendario.md` em tabela para leitura humana.

## Output Format

```yaml
cliente: "{slug}"
mes_referencia: "YYYY-MM"
total_itens: 18
distribuicao_efetiva:
  topo: { itens: 6, percentual: 33 }
  meio: { itens: 6, percentual: 33 }
  fundo: { itens: 6, percentual: 34 }
itens:
  - n: 1
    data: "YYYY-MM-DD"
    assunto: "{tema específico, não rótulo}"
    etapa: "topo|meio|fundo"
    formato: "carrossel|post-linkedin"
    plataforma: "Instagram|LinkedIn"
    oferta_promovida: "{apenas em itens de fundo}"
    depende_de_asset: false
    justificativa: "{origem explícita: dor X | achado de DD/MM | objetivo Y}"
    status: "planejado"
```

## Output Example

> Referência de qualidade, não gabarito.

```yaml
cliente: "laia"
mes_referencia: "2026-08"
total_itens: 18
distribuicao_efetiva:
  topo: { itens: 6, percentual: 33 }
  meio: { itens: 6, percentual: 33 }
  fundo: { itens: 6, percentual: 34 }
itens:
  - n: 1
    data: "2026-08-03"
    assunto: "O orçamento que você reescreve 20 vezes por semana"
    etapa: "topo"
    formato: "carrossel"
    plataforma: "Instagram"
    depende_de_asset: false
    justificativa: >
      Lacuna editorial confirmada na pesquisa: 0 de 4 concorrentes abordaram a dor
      "faz orçamento manual e repete o mesmo texto 20x por semana" no período.
      Dor está em publico.dores do perfil.
    status: "planejado"

  - n: 3
    data: "2026-08-07"
    assunto: "Como o cliente X passou de 2 dias para 4 minutos no primeiro retorno"
    etapa: "fundo"
    formato: "carrossel"
    plataforma: "Instagram"
    oferta_promovida: "Implantação de agentes de IA"
    depende_de_asset: true
    justificativa: >
      Objetivo principal do perfil é leads. Feedback brief aponta que carrossel com print
      de resultado real teve o melhor desempenho de julho (11,2% vs 6,8% de média).
      Depende de autorização e print do cliente X.
    status: "planejado"

  - n: 5
    data: "2026-08-12"
    assunto: "Por que sua IA parou no ChatGPT e não virou processo"
    etapa: "meio"
    formato: "post-linkedin"
    plataforma: "LinkedIn"
    depende_de_asset: false
    justificativa: >
      Dor "testou IA e parou no ChatGPT" do perfil, com cobertura apenas superficial por
      1 de 4 concorrentes (lacuna parcial na pesquisa de 2026-07).
    status: "planejado"
```

## Quality Criteria

- [ ] Todos os slots da grade foram preenchidos
- [ ] Toda justificativa cita dor, achado datado ou objetivo — nunca o próprio tema
- [ ] Itens de fundo nomeiam oferta existente em `identidade.ofertas`
- [ ] Nenhum assunto repetido no mês
- [ ] Temas saturados evitados, ou com ângulo diferenciador declarado
- [ ] Assuntos são temas específicos, não rótulos genéricos
- [ ] Os dois arquivos gerados e consistentes entre si

## Veto Conditions

Rejeitar e refazer se:
1. Algum item tem justificativa circular ou vazia
2. Algum item de fundo não nomeia oferta específica do perfil
3. Existe assunto repetido dentro do mês
4. A distribuição efetiva não corresponde à grade aprovada na task anterior
5. Algum assunto é um rótulo genérico do tipo "dica do dia" ou "conteúdo educativo"
