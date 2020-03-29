---
title: Suporte do Navegador
---

O Gatsby suporta [os mesmos navegadores que a versão estável atual do React.js](https://pt-br.reactjs.org/docs/react-dom.html#browser-support) que atualmente é o IE9+, assim como as versões mais recentes de outros navegadores populares.

## Polyfills

Gatsby aproveita a capacidade do Babel 7 de adicionar automaticamente polyfills para os navegadores escolhidos.

Navegadores mais novos suportam mais APIs JavaScript do que navegadores mais antigos. Para versões mais antigas, o Gatsby (via Babel) adiciona automaticamente os "polyfills" mínimos necessários para que seu código funcione nesses navegadores.

Se você começar a usar uma API mais recente do JavaScript, como `[].includes`, que não é suportada por alguns dos navegadores escolhidos, você não precisará se preocupar com a quebra dos navegadores mais antigos, pois o Babel adicionará automaticamente o polyfill `core-js/modules/es7.array.includes`.

## Especifique quais navegadores seu projeto suporta usando "Browserslist"

Você pode personalizar sua lista de versões suportadas dos navegadores declarando uma [`"browserslist"`](https://github.com/ai/browserslist) dentro do seu `package.json`. Alterar esses valores irá modificar o resultado de seu JavaScript (via
[`babel-preset-env`](https://github.com/babel/babel-preset-env#targetsbrowsers)) e CSS (via [`autoprefixer`](https://github.com/postcss/autoprefixer)).

Este artigo é uma boa introdução à crescente comunidade de ferramentas em torno da lista de navegadores (Browserslist)  — https://css-tricks.com/browserlist-good-idea/

Por padrão, o Gatsby emula a seguinte configuração:

```json:title=package.json
{
  "browserslist": [">0.25%", "not dead"]
}
```

Se você suporta apenas navegadores mais novos, certifique-se de especificar no seu `package.json`. Isso geralmente permite que você envie arquivos JavaScript menores.
