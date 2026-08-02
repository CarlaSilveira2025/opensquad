---
task: "Criar Post LinkedIn"
order: 1
input: |
  - ganchos_selecionados: output/ganchos-selecionados.yaml
  - angulos_selecionados: output/angulos-selecionados.yaml
  - pesquisa: output/pesquisa.md
  - perfil: _opensquad/_memory/clientes/{slug}/perfil.json
  - tom: pipeline/data/tone-of-voice.md
output: |
  - linkedin: post completo pronto para publicar (output/linkedin.md)
---

# Criar Post LinkedIn

Escreve o post longo de LinkedIn na estrutura gancho → contexto → desenvolvimento → insight
→ CTA, com hashtags discretas e sugestão de peça visual.

## Process

1. **Ler o gancho aprovado para LinkedIn.** Ele ocupa a primeira linha, literal. Conferir que
   cabe em ~200 caracteres — é o que aparece antes do "ver mais".

2. **Abrir com cena, não com tese.** Depois do gancho, uma situação concreta em que o leitor
   se reconheça. A conclusão vem depois, quando ele já está dentro do texto.

3. **Desenvolver em blocos de 1 a 3 linhas**, separados por quebra dupla. Bloco denso é
   abandonado na rolagem.

4. **Usar especificidade.** Número, nome de ferramenta, prazo, valor. "De 2 dias para 4
   minutos" vale mais que "reduzimos bastante o tempo".

5. **Escrever o insight explícito** antes do CTA: a frase que o leitor levaria para uma
   reunião. Sem ela, o post é descrição e não é compartilhado.

6. **Fechar com CTA específico.** Pergunta que convida a uma resposta concreta, ou convite
   ligado à oferta quando o item for de fundo de funil.

7. **Adicionar 3 a 5 hashtags** ao final e sugerir a peça visual — imagem única ou carrossel
   em PDF, com descrição do conteúdo dela.

8. **Escrever texto distinto do carrossel**, mesmo que o ângulo seja o mesmo. Copiar slides
   produz post picotado e sem fluxo.

## Output Format

```markdown
# Post LinkedIn — {assunto}

**Ângulo:** {título} · **Gancho:** {id}
**Primeiras 3 linhas:** {contagem de caracteres} (limite ~200)

## Texto

{texto completo, pronto para colar, com as quebras de linha reais}

## Hashtags
{3 a 5}

## Peça visual sugerida
**Tipo:** imagem única | carrossel PDF
**Conteúdo:** {descrição do que a peça mostra}
**Dimensão:** 1200×627 | 1080×1080
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Post LinkedIn — O orçamento que você reescreve 20 vezes por semana

**Ângulo:** Os 20% que ninguém resolve · **Gancho:** 3c
**Primeiras 3 linhas:** 104 caracteres (limite ~200)

## Texto

Comprei a ferramenta, configurei tudo, e três meses depois estava fazendo orçamento no Word
de novo.

Não foi preguiça. Foi que a automação dava conta de 80% dos casos, e os outros 20% eram
justamente os orçamentos grandes — os que pagavam a conta.

Aí acontece o previsível: você mantém dois processos em paralelo. O automático para o que é
simples, o manual para o que importa. E manter dois é mais caro que manter um.

Foi só quando parei de tentar automatizar os 20% que a coisa funcionou.

O que fiz: separei o orçamento em duas partes. A estrutura — escopo, prazos, condições,
termos — virou template automático. O que exige julgamento — dimensionamento e preço —
continuou manual, mas passou a chegar num documento já 70% pronto.

Tempo de resposta: de 2 dias para o mesmo dia.
Tempo de escrita por orçamento grande: de 50 minutos para 15.

O insight que eu levaria pra qualquer processo: automação não é sobre eliminar o
julgamento humano. É sobre tirar dele tudo que não exige julgamento.

Quem tentou automatizar orçamento e voltou pro manual: em qual parte travou?

## Hashtags
#automacao #processos #pequenosnegocios #gestao

## Peça visual sugerida
**Tipo:** imagem única
**Conteúdo:** comparação em duas colunas — "Estrutura (automática)" com os 4 itens listados
à esquerda, "Julgamento (manual)" com os 2 itens à direita, na paleta da marca
**Dimensão:** 1200×627
```

## Quality Criteria

- [ ] Gancho aprovado, literal, na primeira linha
- [ ] Três primeiras linhas ≤ ~200 caracteres e com sentido isoladas
- [ ] Estrutura completa: gancho → contexto → desenvolvimento → insight → CTA
- [ ] Nenhum bloco com mais de 3 linhas
- [ ] Números e nomes específicos presentes
- [ ] Insight explícito antes do CTA
- [ ] Entre 3 e 5 hashtags
- [ ] Peça visual sugerida com tipo, conteúdo e dimensão
- [ ] Texto distinto do carrossel
- [ ] Nenhuma palavra proibida nem corporativês

## Veto Conditions

Rejeitar e refazer se:
1. O gancho aprovado foi reescrito ou não cabe antes do "ver mais"
2. O post abre com tese abstrata em vez de cena concreta
3. Algum dado citado não existe no relatório de pesquisa
4. Não há insight explícito antes do CTA
5. Mais de 5 hashtags
6. O texto é o carrossel reformatado
