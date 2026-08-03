# Anti-Patterns — Calendário Editorial LAIA

Erros que produzem um mês inteiro de conteúdo desperdiçado. Cada um custa quatro fases de
trabalho na Camada 3, não uma linha de planilha.

---

## A. Pesquisa

### A1. Tratar célula vazia como zero
**Sintoma:** o feedback loop passa a evitar um formato que nunca foi medido.
**Causa:** a análise leu `""` como `0` ao calcular médias.
**Correção:** vazio = não medido, excluído dos rankings. Zero só quando medido e zero.

### A2. Tendência sem janela temporal
**Sintoma:** post publicado em agosto sobre assunto que esfriou em março.
**Correção:** todo achado carrega data da fonte e janela a que se refere.

### A3. Confundir volume com oportunidade
**Sintoma:** o calendário repete o tema que o feed do público já cansou de ver.
**Causa:** muitos posts sobre um tema lidos como tendência, quando indicam saturação.
**Correção:** saturado e em alta são seções distintas do relatório.

### A4. Simular dados de post de concorrente
**Sintoma:** lacuna editorial apontada onde na verdade há cobertura densa.
**Causa:** a coleta falhou e o agente preencheu com plausível.
**Correção:** declarar a limitação. Coleta parcial declarada vale mais que coleta inventada.

### A5. Listar data comemorativa sem conexão
**Sintoma:** slot do mês gasto com Dia do Programador num cliente de nutrição.
**Correção:** data sem conexão concreta com o negócio não entra na lista.

---

## B. Montagem do calendário

### B1. Escolher tema antes de fechar a grade
**Sintoma:** mês com 70% topo, pouca conversão, cliente reclamando que "não vende".
**Causa:** os temas mais fáceis de pensar são de topo; sem grade prévia, eles dominam.
**Correção:** `distribuir-funil` roda **antes** de `montar-calendario`, sempre.

### B2. Justificativa circular
**Sintoma:** a Camada 3 produz conteúdo genérico e ninguém sabe explicar a escolha do tema.
**Exemplo:** "Carrossel sobre precificação porque precificação é importante."
**Correção:** justificativa aponta dor do perfil, achado datado ou objetivo.

### B3. Encher o mês para bater o número
**Sintoma:** o cliente abandona o calendário na segunda semana.
**Causa:** slots preenchidos com tema genérico para chegar a 20 itens.
**Correção:** 16 itens fortes valem mais que 20 com 6 vazios. A faixa tem piso por isso.

### B4. Concentrar fundo de funil no fim do mês
**Sintoma:** queda de engajamento na última semana e desinscrição.
**Correção:** máximo 2 de fundo por semana, nunca em dias consecutivos.

### B5. Reagendar formato que já falhou
**Sintoma:** o mesmo resultado ruim, agora com o cliente perdendo confiança no sistema.
**Causa:** `historico_nao_funcionou` do perfil e o feedback brief foram ignorados.
**Correção:** formato reprovado só volta com mudança de abordagem declarada na justificativa.

### B6. Planejar para plataforma inativa
**Sintoma:** produção feita e nunca publicada.
**Correção:** validar toda plataforma contra `objetivos.plataformas`.

### B7. Item de fundo sem oferta nomeada
**Sintoma:** conteúdo de conversão que não converte porque não pede nada específico.
**Correção:** todo item de fundo nomeia uma oferta de `identidade.ofertas`.

---

## C. Revisão

### C1. Estimar a distribuição no olho
**Sintoma:** desvio de 15 pontos aprovado sem ninguém notar.
**Correção:** contar e calcular percentual, em tabela, sempre.

### C2. Reprovar por gosto editorial
**Sintoma:** discussão sobre tema que a auditoria não tem escopo para resolver.
**Correção:** a auditoria verifica estrutura e rastreabilidade, não mérito do tema.

### C3. Parar no primeiro erro
**Sintoma:** dois ciclos de correção onde bastaria um.
**Correção:** auditar o mês inteiro antes de emitir veredito.

---

## D. Planilha e publicação

### D1. Preencher métrica com zero
**Sintoma:** o mês seguinte evita formatos que talvez tenham ido bem.
**Correção:** métricas nascem vazias e assim permanecem até medição real.

### D2. Mudar nome de coluna entre meses
**Sintoma:** comparação histórica quebra justamente quando começaria a ter valor.
**Correção:** cabeçalho é contrato; muda só com incremento de versão.

### D3. CSV sem escape
**Sintoma:** a planilha abre com colunas deslocadas e o usuário desiste de preencher.
**Causa:** `assunto` e `justificativa` quase sempre contêm vírgula.
**Correção:** aspas duplas em todo texto livre, aspas internas duplicadas.

### D4. Sobrescrever o mês anterior
**Sintoma:** o histórico some e o feedback loop perde a base.
**Correção:** um diretório por mês, sempre.

### D5. Republicar perdendo métricas preenchidas
**Sintoma:** o usuário preencheu 12 linhas e perdeu tudo ao pedir um ajuste no calendário.
**Correção:** em republicação, preservar métricas das linhas com `n` e `data` coincidentes.

### D6. Chamar a planilha de "dashboard"
**Sintoma:** o cliente espera métricas automáticas que só chegam na v2.
**Correção:** dizer explicitamente o que é manual nesta versão.
