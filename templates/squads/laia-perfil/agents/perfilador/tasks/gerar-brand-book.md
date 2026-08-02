---
task: "Gerar Brand Book"
order: 2
input: |
  - perfil: output/perfil.json
  - exemplos: pipeline/data/output-examples.md
output: |
  - brand_book: versão legível do perfil para conferência do cliente (output/brand-book.md)
---

# Gerar Brand Book

Produz a versão humana do perfil: um documento que o cliente lê em dois minutos e confirma
"é isso mesmo" ou aponta o que está errado. Espelha o `perfil.json` sem acrescentar nem
contradizer informação.

## Process

1. **Ler o `perfil.json` inteiro.** O brand book é derivado exclusivamente dele — não voltar
   ao briefing para buscar informação extra.

2. **Escrever as seis seções** na ordem: Quem é, Para quem fala, Como fala, O que quer,
   Como aparece, O que ainda falta.

3. **Traduzir campos técnicos em frases legíveis.** `percepcao_desejada` vira "Quer ser
   percebida como…"; `frequencia` vira "Publica X vezes por semana". Manter os valores
   exatos.

4. **Renderizar a paleta com o hex visível** ao lado do nome da cor, para o cliente conferir.

5. **Fechar com a seção de pendências**, agrupada por criticidade, indicando o que fica
   bloqueado enquanto cada pendência crítica existir.

6. **Conferir espelhamento.** Percorrer o JSON campo a campo e verificar que cada valor
   preenchido aparece no documento e que nenhum valor do documento inexiste no JSON.

## Output Format

```markdown
# Brand Book — {nome}

_Gerado pelo sistema LAIA em {data} · perfil versão {versao_schema}_

## Quem é
{nicho}. {percepcao_desejada}

**Ofertas:** {nome} — {promessa} ({preco})
**Diferenciais:** {lista}

## Para quem fala
{quem_sao}, {faixa_etaria}. Fala {linguagem}.
**Dores:** {lista}
**Desejos:** {lista}
**Onde está:** {lista}

## Como fala
**Tom:** {tom_de_voz}
**Usa:** {palavras_usar}
**Evita:** {palavras_evitar}
**Referências:** {perfil} — {o_que_admira}

## O que quer
**Meta principal:** {meta_principal}
**Plataformas:** {plataformas} · **Frequência:** {frequencia}
**Já funcionou:** {lista}
**Não funcionou:** {lista}

## Como aparece
**Logo:** {logo}
**Paleta:** {nome} `{hex}`
**Tipografia:** {lista} · **Estilo:** {estilo_imagem}

## O que ainda falta
### Crítico
- `{campo}` — bloqueia {consequência}
### Importante / Opcional
- `{campo}`
```

## Output Example

> Referência de qualidade, não gabarito.

```markdown
# Brand Book — LAIA

_Gerado pelo sistema LAIA em 2026-08-02 · perfil versão 1.0.0_

## Quem é
Automação e IA aplicada a pequenos negócios. Quer ser percebida como autoridade
acessível — especialista que explica sem jargão.

**Ofertas:**
- Implantação de agentes de IA — rodando em 30 dias (R$ 4.500 por projeto)
- Mentoria de automação — acompanhamento contínuo (R$ 890/mês)

**Diferenciais:** entrega funcionando, não só diagnóstico · atende quem não é técnico

## Para quem fala
Donos de pequenos negócios de serviço com 2 a 15 funcionários, 30-50 anos.
Fala de forma informal, direta, sem termos técnicos.

**Dores:** perde lead por demora na resposta · faz tudo manual e não escala ·
testou IA e não saiu do ChatGPT
**Desejos:** ter processo rodando sozinho · parecer maior do que é
**Onde está:** Instagram · grupos de WhatsApp de empreendedorismo

## Como aparece
**Paleta:** Grafite `#1A1A2E` · Verde sinal `#00D982`
**Tipografia:** Inter · **Estilo:** bold, alto contraste, fundo escuro

## O que ainda falta
### Crítico
- `objetivos.historico_nao_funcionou` — sem isso o calendário pode repetir formato que
  já falhou
### Importante / Opcional
- `visual.elementos_graficos`
```

## Quality Criteria

- [ ] Todas as seis seções presentes
- [ ] Nenhuma informação que não exista no `perfil.json`
- [ ] Nenhum valor preenchido do JSON ficou de fora
- [ ] Paleta exibe nome e hex juntos
- [ ] Pendências agrupadas por criticidade, com consequência nas críticas

## Veto Conditions

Rejeitar e refazer se:
1. O documento afirma algo que contradiz o `perfil.json`
2. Alguma seção foi omitida
3. Pendências críticas não aparecem no documento
4. O texto preenche lacuna com linguagem genérica de marketing
