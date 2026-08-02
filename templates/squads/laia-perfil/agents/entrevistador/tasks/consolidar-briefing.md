---
task: "Consolidar Briefing"
order: 1
input: |
  - cliente: identificação do cliente (output/cliente.md)
  - bloco_identidade: respostas do bloco 1 (output/respostas/identidade.md)
  - bloco_publico: respostas do bloco 2 (output/respostas/publico.md)
  - bloco_comunicacao: respostas do bloco 3 (output/respostas/comunicacao.md)
  - bloco_objetivos: respostas do bloco 4 (output/respostas/objetivos.md)
  - bloco_assets: respostas do bloco 5 (output/respostas/assets.md)
  - schema: pipeline/data/domain-framework.md (campos obrigatórios do perfil)
output: |
  - briefing_consolidado: briefing normalizado em campos (output/briefing-consolidado.md)
---

# Consolidar Briefing

Transforma as respostas cruas dos cinco blocos em um único briefing estruturado por campos,
normalizado e rastreável. Não interpreta nem completa — transporta o que foi dito para o
formato que o Perfilador consegue converter em JSON.

## Process

1. **Ler os cinco blocos e a identificação do cliente.** Se algum arquivo de bloco não
   existir ou estiver vazio, tratar todos os campos daquele bloco como `PENDENTE` e seguir —
   não interromper a consolidação.

2. **Mapear cada resposta para os campos do schema.** Abrir
   `pipeline/data/domain-framework.md` e percorrer os campos na ordem definida. Para cada
   campo, localizar a informação correspondente nas respostas. Nunca criar campo novo fora
   do schema.

3. **Normalizar formatos.** Converter enumerações em listas item a item; extrair preços com
   moeda e periodicidade explícitas; converter frequências para o padrão
   "N por semana / N por mês"; padronizar nomes de plataformas (Instagram, LinkedIn).

4. **Marcar ausências.** Todo campo do schema sem informação correspondente recebe o valor
   literal `PENDENTE`. Nenhum campo do schema pode ser omitido do briefing.

5. **Registrar a origem de cada campo.** Anotar de qual bloco veio a informação, para
   permitir correção pontual sem refazer a entrevista.

6. **Verificar declarações públicas quando houver URL.** Se o cliente informou site ou
   perfis, usar `web_fetch` para conferir nicho, oferta e linguagem declarados. Divergências
   entram na seção de observações — nunca sobrescrevem o que o cliente disse.

## Output Format

```markdown
# Briefing Consolidado — {Nome do Cliente}

**Slug:** {slug}
**Data:** {YYYY-MM-DD}
**Tipo:** novo | atualização

## 1. Identidade
- **nome_marca:** {valor | PENDENTE}  _(origem: bloco 1)_
- **nicho:** {valor | PENDENTE}
- **ofertas:** [{nome} — {promessa} — {preço}]
- **diferenciais:** [item, item]
- **percepcao_desejada:** {valor}

## 2. Público-Alvo
- **quem_sao:** {valor}
- **dores:** [item, item, item]
- **desejos:** [item, item]
- **onde_estao:** [canal, canal]
- **faixa_etaria:** {valor}
- **linguagem:** {valor}

## 3. Comunicação
- **tom_de_voz:** {valor}
- **palavras_usar:** [termo, termo]
- **palavras_evitar:** [termo, termo]
- **referencias:** [@perfil — o que admira]

## 4. Objetivos
- **meta_principal:** {valor}
- **ofertas_atuais:** [item]
- **historico_funcionou:** [item]
- **historico_nao_funcionou:** [item]
- **plataformas:** [Instagram | LinkedIn]
- **frequencia:** {N por semana}

## 5. Assets Visuais
- **logo:** {caminho | PENDENTE}
- **paleta:** [#RRGGBB]
- **tipografias:** [nome]
- **estilo_imagem:** {valor}
- **elementos_graficos:** [item]
- **fotos_referencia:** [caminho]

## Observações e Divergências
- {divergência entre o declarado e o verificado, se houver}
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Briefing Consolidado — LAIA

**Slug:** laia
**Data:** 2026-08-02
**Tipo:** novo

## 1. Identidade
- **nome_marca:** LAIA  _(origem: bloco 1)_
- **nicho:** Automação e IA aplicada a pequenos negócios  _(origem: bloco 1)_
- **ofertas:** ["Implantação de agentes de IA — entrega em 30 dias — R$ 4.500 projeto",
  "Mentoria mensal de automação — R$ 890/mês"]
- **diferenciais:** ["Entrega funcionando, não só diagnóstico", "Atende quem não é técnico"]
- **percepcao_desejada:** Autoridade acessível — especialista que explica sem jargão

## 2. Público-Alvo
- **quem_sao:** Donos de pequenos negócios de serviço com 2 a 15 funcionários
- **dores:** ["Perde lead por demora na resposta", "Faz tudo manual e não escala",
  "Testou IA e não saiu do ChatGPT"]
- **desejos:** ["Ter processo rodando sozinho", "Parecer maior do que é"]
- **onde_estao:** ["Instagram", "Grupos de WhatsApp de empreendedorismo"]
- **faixa_etaria:** 30-50
- **linguagem:** Informal, direta, sem termos técnicos

## Observações e Divergências
- O bloco 4 lista LinkedIn como plataforma ativa, mas o bloco 2 aponta o público apenas
  no Instagram e em grupos de WhatsApp. Levar para detecção de lacunas.
```

## Quality Criteria

- [ ] Todos os campos do schema aparecem, preenchidos ou como `PENDENTE`
- [ ] Nenhum valor foi inferido a partir do nicho ou de outro cliente
- [ ] Listas estão em formato de lista, não em prosa
- [ ] Cada campo preenchido tem origem rastreável a um dos cinco blocos
- [ ] Divergências entre blocos aparecem na seção de observações

## Veto Conditions

Rejeitar e refazer se:
1. Algum campo do schema foi omitido do documento
2. Algum campo contém valor plausível mas sem origem em nenhum bloco
3. Adjetivos subjetivos foram transportados sem o exemplo concreto que o cliente deu
4. O documento é prosa corrida em vez de campos nomeados
