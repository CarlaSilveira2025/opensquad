---
task: "Criar Slides HTML"
order: 2
input: |
  - sistema_visual: output/sistema-visual.md
  - carrossel: output/carrossel.md (texto exato e indicação visual por slide)
  - linkedin: output/linkedin.md (peça visual sugerida)
output: |
  - slides_html: um arquivo HTML por slide (output/slides/slide-NN.html)
---

# Criar Slides HTML

Monta cada slide como um HTML/CSS autocontido, aplicando o sistema visual. O texto aprovado
entra sem nenhuma alteração.

## Process

1. **Criar um arquivo por slide**, nomeado `slide-01.html` a `slide-NN.html`, mais
   `linkedin-01.html` para a peça de LinkedIn quando houver.

2. **Escrever HTML autocontido.** Todo CSS inline no `<style>` do próprio arquivo. Nenhuma
   referência externa — sem CDN, sem fonte remota, sem imagem por URL. Fontes por
   `font-family` com fallback de sistema; imagens locais por caminho relativo ou data URI.

3. **Fixar as dimensões no `body`**: 1080×1350px para carrossel de Instagram, 1200×627px ou
   1080×1080px para LinkedIn. Usar `box-sizing: border-box` e `overflow: hidden` para que
   nada vaze da viewport.

4. **Colar o texto aprovado literalmente.** Sem cortar, sem abreviar, sem reescrever. Se o
   texto não couber, ajustar o design — reduzir o corpo dentro da escala, aumentar a área
   útil, mudar a composição — nunca o texto.

5. **Aplicar o tratamento do tipo de slide** definido no sistema visual: capa, número
   dominante, texto puro, reflexão, CTA.

6. **Inserir logo e numeração** nas posições fixas definidas, quando aplicável. Se o arquivo
   de logo não existir, omitir e registrar.

7. **Conferir a legibilidade antes de fechar cada arquivo**: nenhuma fonte abaixo de 32px,
   contraste mantido, e nenhum bloco de texto encostando na margem.

## Output Format

Um arquivo HTML por slide, com esta estrutura:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    width: 1080px; height: 1350px;
    background: {hex do fundo};
    font-family: '{fonte}', system-ui, sans-serif;
    padding: {margem}px;
    display: flex; flex-direction: column; justify-content: center;
    overflow: hidden;
  }
  .titulo { font-size: {px}; font-weight: {peso}; color: {hex}; line-height: 1.1; }
  .destaque { color: {hex do destaque}; }
  .rodape { position: absolute; bottom: {px}; font-size: 34px; color: {hex secundário}; }
</style>
</head>
<body>
  <div class="titulo">{texto exato aprovado}</div>
  <div class="rodape">{numeração}</div>
</body>
</html>
```

## Output Example

> Referência de qualidade, não gabarito. Exemplo do `slide-01.html` (capa).

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    width: 1080px; height: 1350px;
    background: #1A1A2E;
    font-family: 'Inter', system-ui, -apple-system, sans-serif;
    padding: 96px;
    display: flex; flex-direction: column; justify-content: center;
    position: relative; overflow: hidden;
  }
  .capa {
    font-size: 96px; font-weight: 800; color: #FFFFFF;
    line-height: 1.08; letter-spacing: -0.02em;
  }
  .destaque { color: #00D982; display: block; margin-top: 24px; }
  .numeracao {
    position: absolute; bottom: 96px; left: 96px;
    font-size: 34px; font-weight: 500; color: #A0A0B8;
  }
  .logo { position: absolute; bottom: 88px; right: 96px; width: 120px; }
</style>
</head>
<body>
  <div class="capa">
    Você não tem problema de ferramenta.
    <span class="destaque">Tem problema de processo.</span>
  </div>
  <div class="numeracao">01/08</div>
  <img class="logo" src="../../../../_opensquad/_memory/clientes/laia/assets/logo.png" alt="">
</body>
</html>
```

Observações do exemplo: o texto é exatamente o gancho aprovado 3b, sem alteração; a segunda
linha recebe o destaque em verde sinal conforme o sistema visual; nenhuma fonte abaixo de
34px; margem de 96px respeitada em todos os lados.

## Quality Criteria

- [ ] Um arquivo por slide, nomeados em sequência
- [ ] HTML autocontido, sem nenhuma referência de rede
- [ ] Dimensões fixas corretas por plataforma
- [ ] Texto aprovado presente sem nenhuma alteração
- [ ] Apenas cores do sistema visual
- [ ] Nenhuma fonte abaixo de 32px
- [ ] `overflow: hidden` e margens respeitadas
- [ ] Logo e numeração nas posições definidas, quando aplicável

## Veto Conditions

Rejeitar e refazer se:
1. Alguma palavra do texto aprovado foi cortada, abreviada ou reescrita
2. O HTML referencia recurso externo por URL
3. Alguma cor fora do sistema visual foi usada
4. Alguma fonte está abaixo de 32px
5. As dimensões do `body` não correspondem à plataforma
