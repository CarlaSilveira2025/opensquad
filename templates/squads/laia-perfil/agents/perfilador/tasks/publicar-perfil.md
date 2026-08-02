---
task: "Publicar Perfil"
order: 3
input: |
  - perfil: output/perfil.json (aprovado no checkpoint 11)
  - brand_book: output/brand-book.md
  - validacao: output/validacao-perfil.md
  - cliente: output/cliente.md (slug e tipo novo/atualização)
output: |
  - publicacao_report: relatório dos arquivos publicados (output/publicacao-report.md)
---

# Publicar Perfil

Copia o perfil aprovado para o registro de clientes em
`_opensquad/_memory/clientes/{slug}/`, onde os squads `laia-calendario` e `laia-conteudo`
vão lê-lo. Em atualizações, arquiva a versão anterior antes de sobrescrever.

Esta task só roda depois do checkpoint de aprovação (step 11). Escrever no registro antes
disso publica um perfil que o cliente ainda pode rejeitar.

## Process

1. **Confirmar a aprovação.** Ler `output/validacao-perfil.md` e conferir que o veredito é
   APROVADO. Se for REPROVADO, abortar a publicação e reportar — não publicar perfil reprovado.

2. **Resolver o slug e os caminhos de destino.** Destino base:
   `_opensquad/_memory/clientes/{slug}/`. Arquivos: `perfil.json`, `brand-book.md`,
   subpasta `assets/` e subpasta `historico/`.

3. **Arquivar a versão anterior, se existir.** Verificar se
   `_opensquad/_memory/clientes/{slug}/perfil.json` já existe. Se sim, copiá-lo para
   `historico/perfil-{YYYY-MM-DD}.json` e o brand-book para
   `historico/brand-book-{YYYY-MM-DD}.md` antes de qualquer sobrescrita.

4. **Escrever os arquivos novos** usando a ferramenta Write (que cria os diretórios pais
   automaticamente). Nunca usar `mkdir` via Bash.

5. **Registrar os assets informados.** Se o cliente indicou caminhos de logo ou fotos,
   listá-los no relatório com a observação de que os arquivos precisam ser colocados em
   `assets/` manualmente pelo usuário — o squad não move binários que não recebeu.

6. **Emitir o relatório de publicação** com todos os caminhos escritos, o que foi arquivado
   e as pendências que seguem abertas.

## Output Format

```markdown
# Publicação do Perfil — {nome}

**Slug:** {slug}
**Tipo:** novo | atualização
**Data:** {YYYY-MM-DD}

## Arquivos publicados
- `_opensquad/_memory/clientes/{slug}/perfil.json`
- `_opensquad/_memory/clientes/{slug}/brand-book.md`

## Versão anterior arquivada
- {caminho do histórico} | Não aplicável (primeiro cadastro)

## Assets pendentes de upload manual
- {caminho declarado} → colocar em `_opensquad/_memory/clientes/{slug}/assets/`

## Pendências do perfil que seguem abertas
- `{campo}` ({criticidade})

## Próximo passo
Rodar `/opensquad run laia-calendario` para gerar o calendário editorial de {slug}.
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Publicação do Perfil — LAIA

**Slug:** laia
**Tipo:** novo
**Data:** 2026-08-02

## Arquivos publicados
- `_opensquad/_memory/clientes/laia/perfil.json`
- `_opensquad/_memory/clientes/laia/brand-book.md`

## Versão anterior arquivada
Não aplicável (primeiro cadastro)

## Assets pendentes de upload manual
- `logo.png` → colocar em `_opensquad/_memory/clientes/laia/assets/`
  O perfil aponta para esse caminho; enquanto o arquivo não estiver lá, os carrosséis
  serão gerados sem logo.

## Pendências do perfil que seguem abertas
- `objetivos.historico_nao_funcionou` (CRITICA) — responder antes do primeiro calendário
- `visual.elementos_graficos` (OPCIONAL)

## Próximo passo
Rodar `/opensquad run laia-calendario` para gerar o calendário editorial de laia.
```

## Quality Criteria

- [ ] A publicação só ocorreu com veredito APROVADO
- [ ] Todos os caminhos escritos estão listados no relatório
- [ ] Em atualização, o histórico foi gravado antes da sobrescrita
- [ ] Assets declarados mas não entregues aparecem como upload manual pendente
- [ ] O relatório indica o próximo comando a rodar

## Veto Conditions

Rejeitar e refazer se:
1. Houve escrita no registro de clientes com veredito REPROVADO
2. Um perfil anterior foi sobrescrito sem arquivamento
3. O relatório omite algum arquivo efetivamente escrito
4. Foi usado `mkdir` via Bash para criar os diretórios
