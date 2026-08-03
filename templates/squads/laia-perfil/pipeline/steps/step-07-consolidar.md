---
step: "07"
name: "Consolidação e Detecção de Lacunas"
type: agent
execution: inline
agent: entrevistador
tasks:
  - consolidar-briefing
  - detectar-lacunas
depends_on: step-06
inputFile: squads/laia-perfil/output/respostas/assets.md
outputFile: squads/laia-perfil/output/lacunas.md
---

# Step 07: Otávio Onboarding — Consolidação e Detecção de Lacunas

## Context Loading

Carregar antes de executar:

- `squads/laia-perfil/output/cliente.md` — nome, slug e tipo (novo ou atualização)
- `squads/laia-perfil/output/respostas/identidade.md` — bloco 1 cru
- `squads/laia-perfil/output/respostas/publico.md` — bloco 2 cru
- `squads/laia-perfil/output/respostas/comunicacao.md` — bloco 3 cru
- `squads/laia-perfil/output/respostas/objetivos.md` — bloco 4 cru
- `squads/laia-perfil/output/respostas/assets.md` — bloco 5 cru
- `squads/laia-perfil/pipeline/data/domain-framework.md` — schema de campos do perfil
- `squads/laia-perfil/pipeline/data/quality-criteria.md` — bloqueadores e mínimos por campo
- `_opensquad/_memory/company.md` — contexto da empresa operadora do sistema
- Em atualização: `_opensquad/_memory/clientes/{slug}/perfil.json` — perfil vigente, usado
  para resolver respostas "manter"

## Instructions

### Process

1. **Executar a task `consolidar-briefing`.** Mapear os cinco blocos crus para os campos do
   schema, normalizar formatos, marcar ausências como `PENDENTE` e registrar a origem de
   cada campo. Salvar em `squads/laia-perfil/output/briefing-consolidado.md`.

2. **Resolver respostas "manter".** Para cada bloco cuja resposta seja `manter`, copiar os
   campos correspondentes do `perfil.json` vigente do cliente. Se o perfil vigente não
   existir, converter em `PENDENTE` e avisar.

3. **Verificar declarações públicas.** Se houver site ou perfis sociais informados, usar
   `web_fetch` para conferir nicho, oferta e linguagem. Registrar divergências na seção de
   observações do briefing — nunca sobrescrever o que o cliente declarou.

4. **Executar a task `detectar-lacunas`.** Listar campos `PENDENTE`, campos vagos e
   inconsistências cruzadas; classificar em CRÍTICA, IMPORTANTE e OPCIONAL; formular uma
   pergunta por lacuna com a consequência prática; cortar em 8 perguntas.

5. **Salvar `squads/laia-perfil/output/lacunas.md`** e apresentar ao usuário um resumo de
   duas linhas: quantos campos foram preenchidos e quantas perguntas vêm no próximo passo.

## Output Format

Dois arquivos. `briefing-consolidado.md` segue o formato da task `consolidar-briefing`.
`lacunas.md` segue este template literal:

```markdown
# Lacunas Detectadas — {Nome do Cliente}

**Total:** {N} lacunas ({N} críticas, {N} importantes, {N} opcionais)
**Nesta rodada:** {N} perguntas

## Perguntas desta rodada

### 1. [{CRÍTICA|IMPORTANTE|OPCIONAL}] {campo.em.ponto}
**Pergunta:** {pergunta em linguagem do cliente}
**Por que importa:** {consequência prática em uma linha}

## Inconsistências a resolver
- **{campo A} vs {campo B}:** {os dois lados citados} → {pergunta de desempate}

## Fica para depois
- `{campo}`: {motivo de ter sido adiada}
```

## Output Example

```markdown
# Lacunas Detectadas — Authentic Studio

**Total:** 7 lacunas (2 críticas, 4 importantes, 1 opcional)
**Nesta rodada:** 7 perguntas

## Perguntas desta rodada

### 1. [CRÍTICA] publico.dores
**Pergunta:** Me dá 3 situações concretas em que seu cliente sofre antes de te procurar.
Ex.: "chega no fim do mês sem saber quanto lucrou" é situação; "desorganização" não é.
**Por que importa:** é o campo que o sistema usa pra escolher tema de post; sem ele, todo
carrossel fala com todo mundo e não converte ninguém.

### 2. [CRÍTICA] visual.paleta
**Pergunta:** Você descreveu "azul escuro e dourado". Confirma se posso usar #12233A e
#C9A227 como as cores oficiais, ou me manda os códigos certos?
**Por que importa:** o gerador de imagem precisa do código exato; com nome de cor os
slides saem com tom aleatório a cada execução.

### 3. [IMPORTANTE] comunicacao.tom_de_voz
**Pergunta:** Você disse "profissional mas próximo". Me cola um texto seu que representa
bem esse tom?
**Por que importa:** sem amostra real, o texto sai com voz genérica de LinkedIn.

### 4. [IMPORTANTE] objetivos.historico_nao_funcionou
**Pergunta:** Teve algum post ou formato que claramente não engajou?
**Por que importa:** sem isso o calendário pode reagendar exatamente o que já falhou.

## Inconsistências a resolver
- **objetivos.frequencia vs objetivos.plataformas:** você declarou 5 conteúdos por semana
  em Instagram e LinkedIn, mas citou que hoje publica 1 vez por semana → a meta de 5 é
  para onde quer chegar ou é o ritmo que já consegue sustentar hoje?

## Fica para depois
- `visual.elementos_graficos`: refinamento; os slides funcionam sem elementos próprios.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Algum campo do schema foi omitido do briefing consolidado
2. Algum campo do briefing contém valor sem origem rastreável nos blocos ou no perfil vigente
3. A rodada de perguntas tem mais de 8 itens
4. Alguma lacuna crítica foi omitida ou rebaixada para caber no limite de 8
5. Alguma pergunta pede informação que já está explícita nos blocos respondidos

## Quality Criteria

- [ ] Os dois arquivos de saída foram gravados
- [ ] Todo campo `PENDENTE` do briefing aparece como lacuna ou como item adiado
- [ ] Cada pergunta cita o campo em notação de ponto e explica a consequência prática
- [ ] Inconsistências citam literalmente os dois lados em conflito
- [ ] Divergências entre o declarado e o verificado na web estão nas observações
- [ ] O resumo apresentado ao usuário tem no máximo duas linhas
