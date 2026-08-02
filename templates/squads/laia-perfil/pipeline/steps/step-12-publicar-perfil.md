---
step: "12"
name: "Publicação no Registro de Clientes"
type: agent
execution: inline
agent: perfilador
tasks:
  - publicar-perfil
depends_on: step-11
inputFile: squads/laia-perfil/output/perfil.json
outputFile: squads/laia-perfil/output/publicacao-report.md
---

# Step 12: Priscila Perfil — Publicação no Registro de Clientes

## Context Loading

Carregar antes de executar:

- `squads/laia-perfil/output/perfil.json` — perfil aprovado no checkpoint 11
- `squads/laia-perfil/output/brand-book.md` — versão legível a publicar junto
- `squads/laia-perfil/output/validacao-perfil.md` — veredito da validação
- `squads/laia-perfil/output/cliente.md` — slug e tipo do cadastro
- Registro de destino: `_opensquad/_memory/clientes/{slug}/`

## Instructions

### Process

1. **Confirmar a autorização de publicação.** Ler o veredito da validação. Se for REPROVADO,
   só publicar se o checkpoint 11 registrou confirmação explícita do usuário; nesse caso,
   registrar a decisão no relatório. Sem essa confirmação, abortar e reportar.

2. **Arquivar a versão vigente, se existir.** Verificar se
   `_opensquad/_memory/clientes/{slug}/perfil.json` já existe. Se sim, copiar para
   `_opensquad/_memory/clientes/{slug}/historico/perfil-{YYYY-MM-DD}.json` e o brand book
   para `historico/brand-book-{YYYY-MM-DD}.md` antes de qualquer sobrescrita.

3. **Escrever os arquivos no registro** com a ferramenta Write, que cria os diretórios pais
   automaticamente: `perfil.json` e `brand-book.md` em
   `_opensquad/_memory/clientes/{slug}/`. Nunca usar `mkdir` via Bash.

4. **Listar assets declarados mas não entregues.** Caminhos de logo e fotos que o perfil
   referencia mas que não existem no disco entram no relatório como upload manual pendente.

5. **Gravar o relatório** em `squads/laia-perfil/output/publicacao-report.md` com todos os
   caminhos escritos, o que foi arquivado, os assets pendentes e as pendências do perfil que
   seguem abertas.

6. **Apresentar ao usuário** os caminhos publicados e o próximo comando a rodar.

## Output Format

```markdown
# Publicação do Perfil — {nome}

**Slug:** {slug}
**Tipo:** novo | atualização
**Data:** {YYYY-MM-DD}
**Veredito da validação:** APROVADO | REPROVADO (publicado por decisão do usuário)

## Arquivos publicados
- `_opensquad/_memory/clientes/{slug}/perfil.json`
- `_opensquad/_memory/clientes/{slug}/brand-book.md`

## Versão anterior arquivada
- {caminho} | Não aplicável (primeiro cadastro)

## Assets pendentes de upload manual
- {caminho declarado} → colocar em `_opensquad/_memory/clientes/{slug}/assets/`

## Pendências do perfil que seguem abertas
- `{campo}` ({criticidade})

## Próximo passo
Rodar `/opensquad run laia-calendario` para gerar o calendário editorial de {slug}.
```

## Output Example

```markdown
# Publicação do Perfil — Authentic Studio

**Slug:** authentic-studio
**Tipo:** novo
**Data:** 2026-08-02
**Veredito da validação:** APROVADO

## Arquivos publicados
- `_opensquad/_memory/clientes/authentic-studio/perfil.json`
- `_opensquad/_memory/clientes/authentic-studio/brand-book.md`

## Versão anterior arquivada
Não aplicável (primeiro cadastro)

## Assets pendentes de upload manual
- `logo.png` → colocar em `_opensquad/_memory/clientes/authentic-studio/assets/`
  O campo `visual.logo` está `null`; enquanto o arquivo não estiver na pasta, os
  carrosséis serão gerados sem logo no slide de assinatura.

## Pendências do perfil que seguem abertas
- `visual.logo` (IMPORTANTE)
- `objetivos.historico_nao_funcionou` (IMPORTANTE) — o primeiro calendário roda em modo
  exploratório, sem feedback loop
- `visual.elementos_graficos` (OPCIONAL)

## Próximo passo
Rodar `/opensquad run laia-calendario` para gerar o calendário editorial de
authentic-studio. O calendário vai ler este perfil automaticamente.
```

## Veto Conditions

Rejeitar e refazer se qualquer uma for verdadeira:
1. Houve escrita no registro de clientes com veredito REPROVADO sem confirmação explícita
   registrada no checkpoint 11
2. Um perfil anterior foi sobrescrito sem que o arquivamento em `historico/` tenha ocorrido
3. O relatório omite algum arquivo efetivamente escrito
4. Foi usado `mkdir` via Bash em vez da ferramenta Write

## Quality Criteria

- [ ] Todos os caminhos escritos aparecem no relatório
- [ ] Em atualização, o histórico foi gravado antes da sobrescrita
- [ ] Assets declarados e ausentes no disco listados como upload manual
- [ ] Pendências abertas do perfil repetidas no relatório com criticidade
- [ ] Próximo comando indicado ao usuário
- [ ] Nenhum diretório criado via Bash
