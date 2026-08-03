---
step: "06"
name: "Bloco 5 — Assets Visuais"
type: checkpoint
depends_on: step-05
outputFile: squads/laia-perfil/output/respostas/assets.md
---

# 🛑 Checkpoint: Bloco 5 — Assets Visuais

## Para o Pipeline Runner

Coletar a identidade visual. Este bloco alimenta diretamente o agente de design da Camada 3,
que gera HTML/CSS — por isso cor precisa de código hexadecimal, não de nome. Se o usuário
não tiver os códigos, oferecer proposta para aprovação em vez de registrar nome de cor.

## Formato de Apresentação ao Usuário

```
📋 Bloco 5 de 5 — Assets Visuais

1. Logotipo — me diz o caminho do arquivo, ou "não tenho"
2. Paleta de cores — de preferência os códigos hex (#1A1A2E).
   Se não tiver os códigos, descreve as cores que eu te proponho os hex pra aprovar
3. Tipografias/fontes da marca
4. Estilo de imagem preferido: clean · colorido · minimalista · bold
5. Elementos gráficos recorrentes (formas, texturas, ícones, molduras)
6. Fotos suas ou da marca pra usar como referência — caminho dos arquivos

Pode responder tudo de uma vez.
```

## Ação do Pipeline Runner após Resposta

1. Se o usuário descreveu cores sem hex, propor os códigos correspondentes e pedir
   aprovação explícita antes de gravar. Cor aprovada pelo usuário é dado; cor adivinhada
   pelo sistema é pendência.
2. Escrever em `squads/laia-perfil/output/respostas/assets.md`:

```markdown
# Bloco 5 — Assets Visuais

**Resposta do usuário:**
{texto integral}

**Hex aprovados pelo usuário:** {lista de #RRGGBB, ou "nenhum"}
**Arquivos declarados:** {caminhos informados}
**Perguntas não respondidas:** {lista, ou "nenhuma"}
```

3. Registrar que os arquivos binários (logo, fotos) precisarão ser colocados em
   `_opensquad/_memory/clientes/{slug}/assets/` pelo usuário — o squad não move arquivos
   que não recebeu.
4. Avançar para o Step 07 (Consolidação e Detecção de Lacunas).

## Opções Especiais

- **"não tenho identidade visual"** → gravar literalmente. O sistema segue: o agente de
  design da Camada 3 propõe identidades visuais e o usuário escolhe uma na primeira
  produção, que depois pode ser gravada aqui via atualização de perfil.
- **"manter"** (em atualização) → reaproveitar o bloco do perfil existente.
