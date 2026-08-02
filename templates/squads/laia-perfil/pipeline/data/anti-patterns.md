# Anti-Patterns — Perfil de Cliente LAIA

Erros que corrompem o perfil e só aparecem semanas depois, como conteúdo genérico ou visual
quebrado. Cada item traz o sintoma observável, a causa e a correção.

---

## A. Preenchimento indevido

### A1. Completar campo com base no nicho
**Sintoma:** perfil de nutricionista com meta "autoridade" que a cliente nunca declarou.
**Causa:** o agente assume o padrão do setor para não deixar campo vazio.
**Correção:** `null` + entrada em `pendencias`. Campo vazio é informação; campo inventado é
ruído que contamina 30 posts.

### A2. Adivinhar hex a partir de nome de cor
**Sintoma:** o azul dos slides muda de tom entre execuções.
**Causa:** `"azul escuro"` convertido em hex diferente a cada run.
**Correção:** propor o hex ao usuário no checkpoint 06 e gravar só o que ele aprovar.

### A3. Transformar "não sei" em valor plausível
**Sintoma:** o cliente lê o brand book e não se reconhece.
**Causa:** o agente trata "não sei" como convite a sugerir.
**Correção:** gravar a ausência literalmente; a sugestão vira pergunta, não valor.

---

## B. Perda de estrutura

### B1. Briefing em prosa corrida
**Sintoma:** cada squad consumidor interpreta o mesmo perfil de um jeito.
**Causa:** as respostas foram resumidas em texto em vez de mapeadas para campos.
**Correção:** briefing sempre em campos nomeados do schema.

### B2. Omitir chaves nulas do JSON
**Sintoma:** o squad de calendário falha ou se comporta de forma indefinida.
**Causa:** o gerador "limpa" o JSON removendo campos vazios.
**Correção:** toda chave do schema existe sempre; ausência é `null`, não chave faltando.

### B3. Parágrafo inteiro dentro de campo de lista
**Sintoma:** o criador de conteúdo não consegue usar um diferencial isoladamente.
**Causa:** `diferenciais` recebeu um texto único em vez de itens.
**Correção:** listas com um conceito por item.

---

## C. Falhas de diagnóstico

### C1. Aceitar adjetivo como resposta
**Sintoma:** conteúdo com voz genérica de internet, que serviria para qualquer marca.
**Causa:** "tom descontraído" aceito sem amostra de voz real.
**Correção:** todo adjetivo subjetivo exige exemplo concreto; sem exemplo, é lacuna.

### C2. Silenciar contradição entre blocos
**Sintoma:** calendário com posts de LinkedIn para um público que só está no Instagram.
**Causa:** o agente escolheu um dos lados sem perguntar.
**Correção:** contradição vira pergunta de desempate no checkpoint 08.

### C3. Menos de 3 dores mapeadas
**Sintoma:** os temas do mês giram em torno da mesma ideia repetida.
**Causa:** o bloco 2 foi aceito com 1 ou 2 dores.
**Correção:** bloqueador — pedir explicitamente mais dores antes de estruturar.

### C4. Rodada com mais de 8 perguntas
**Sintoma:** o cliente abandona o onboarding ou responde tudo em uma linha.
**Causa:** todas as lacunas viraram pergunta de uma vez.
**Correção:** críticas primeiro, corte em 8, resto em "Fica para depois".

---

## D. Falhas de publicação

### D1. Sobrescrever perfil sem arquivar
**Sintoma:** não há como comparar o que mudou quando a performance cai.
**Causa:** atualização gravou direto por cima.
**Correção:** copiar para `historico/perfil-{data}.json` antes de qualquer escrita.

### D2. Publicar antes da aprovação
**Sintoma:** squads consomem um perfil que o cliente ainda vai rejeitar.
**Causa:** a escrita no registro aconteceu no Step 09 em vez do Step 12.
**Correção:** registro de clientes só é tocado depois do checkpoint 11.

### D3. Criar diretório com `mkdir` via Bash
**Sintoma:** falha de caminho em Windows por conflito de separador.
**Causa:** uso de Bash em vez da ferramenta Write.
**Correção:** Write cria os diretórios pais automaticamente — usar sempre.

---

## E. Escopo indevido da revisão

### E1. Reprovar por pendência tolerável
**Sintoma:** o cliente trava por falta de fonte tipográfica secundária.
**Correção:** só os 9 bloqueadores canônicos reprovam.

### E2. Auditar a qualidade do negócio
**Sintoma:** discussão sobre preço ou posicionamento no meio da validação técnica.
**Correção:** a revisão verifica se o perfil é operável, não se o negócio é bom.

### E3. Corrigir e aprovar no mesmo passo
**Sintoma:** a validação sempre aprova e deixa de detectar problemas reais.
**Correção:** quem corrige é a Perfiladora, no ciclo de rejeição.
