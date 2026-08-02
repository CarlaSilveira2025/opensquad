# Quality Criteria — Calendário Editorial LAIA

Checklist canônica da Vera Veredito no Step 05. Fixa entre execuções. Só **bloqueador**
reprova; ressalva nunca soma para reprovação.

---

## 1. Bloqueadores (reprovam o calendário)

| # | Critério | Condição de aprovação |
|---|---|---|
| 1 | Distribuição de funil | dentro de 40/35/25 ±5 p.p., ou desvio registrado e ligado à meta principal |
| 2 | Volume total | entre 16 e 20 itens, coerente com `objetivos.frequencia` |
| 3 | Justificativa rastreável | **todo** item cita dor, achado datado ou objetivo |
| 4 | Plataforma válida | todo item em plataforma de `objetivos.plataformas` |
| 5 | Oferta em item de fundo | todo item de fundo nomeia oferta de `identidade.ofertas` |
| 6 | Sem repetição | nenhum assunto repetido no mês |
| 7 | Restrição do usuário | nenhum tema da lista de descarte de `ajustes-pesquisa.md` |
| 8 | Campos completos | `assunto`, `etapa`, `formato`, `plataforma`, `justificativa` preenchidos |

---

## 2. Como classificar uma justificativa

| Classe | Definição | Efeito |
|---|---|---|
| **Rastreável** | aponta dor do perfil, achado com data ou objetivo declarado | aprovada |
| **Circular** | justifica o tema com o próprio tema | **bloqueador** |
| **Vazia** | genérica, aplicável a qualquer item ("para engajar") | **bloqueador** |

Teste prático: se a justificativa serviria igualmente para outro item do calendário, ela é
vazia.

---

## 3. Ressalvas (aprovam com observação)

- Dois itens de fundo em dias consecutivos
- Mais de 2 itens de fundo na mesma semana
- Um formato representando mais de 70% do mês
- Gancho sazonal identificado na pesquisa e não aproveitado
- Dois itens sobre a mesma dor com ângulos distintos, mas datas próximas
- Dor do perfil sem nenhuma cobertura no mês, quando o volume permitiria

---

## 4. Verificação da distribuição (obrigatória e explícita)

```
% etapa = (itens da etapa / total de itens) × 100
```

Sempre apresentada em tabela com quatro colunas: itens, % efetivo, % meta, situação.
Avaliar "no olho" é violação de critério — desvios de 15 pontos passam despercebidos.

**Faixas aceitáveis:**

| Etapa | Piso | Teto |
|---|---|---|
| Topo | 35% | 45% |
| Meio | 30% | 40% |
| Fundo | 20% | 30% |

Com ajuste declarado pela meta principal, a faixa da etapa afetada desloca em até 5 p.p.

---

## 5. Critérios da planilha de controle (Step 07)

- [ ] Cabeçalho idêntico ao canônico de 20 colunas, na ordem exata
- [ ] Uma linha por item, sem omissão
- [ ] Toda linha com exatamente 20 campos após o parse
- [ ] Campos com vírgula ou aspas escapados
- [ ] Colunas de métrica e `data_postagem` vazias — nunca `0`, `-` ou `n/a`
- [ ] `status` = `planejado` em todas as linhas
- [ ] Sem quebra de linha dentro de célula

---

## 6. Critérios da pesquisa mensal (Step 02)

- [ ] As três frentes presentes: performance, contexto, concorrência
- [ ] Todo achado com fonte, data e nível de confiança
- [ ] Mínimo de 3 buscas com ângulos diferentes na frente de contexto
- [ ] Máximo de 5 perfis na análise de concorrência
- [ ] Temas saturados em seção separada dos temas em alta
- [ ] Datas sazonais apenas com conexão concreta ao negócio
- [ ] Nenhuma métrica estimada; célula vazia nunca tratada como zero
- [ ] Limitações de coleta declaradas
- [ ] Nenhuma pauta recomendada

---

## 7. Regras do ciclo de revisão

- Máximo de **2 ciclos** automáticos de `on_reject` entre Step 05 e Step 04.
- No terceiro, apresentar ao usuário para decisão manual.
- Ajuste pedido pelo usuário no checkpoint 06 **não** conta nesse limite.
- A auditora nunca corrige: aponta item, problema e correção esperada.
