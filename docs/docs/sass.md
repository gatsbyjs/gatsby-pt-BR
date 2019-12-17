---
title: Usando Sass no Gatsby
---

[Sass](https://sass-lang.com) é uma extensão do CSS, adicionando regras aninhadas, variáveis, mixins, herança de seletor e muito mais. No Gatsby, o código Sass pode ser traduzido para o padrão CSS bem formatado usando um plugin.

O Sass compilará arquivos `.sass` e `.scss` em arquivos `.css`, para que você possa escrever suas folhas de estilo com recursos mais avançados.

> **Nota**: a diferença entre usar um arquivo `.sass` ou `.scss` é a sintaxe em que você escreve seus estilos. Todo CSS válido é SCSS válido, além de ser o mais fácil de usar e o mais popular. Você pode ler mais sobre as diferenças na [documentação do Sass](https://sass-lang.com/documentation/syntax).

## Instalando e configurando o Sass

Este guia pressupõe que você tenha um projeto Gatsby configurado. Se você precisar configurar um projeto, vá para o [**Guia de início rápido**](/docs/quick-start/), e volte depois.

1.  Instale o plugin Gatsby [**gatsby-plugin-sass**](/packages/gatsby-plugin-sass/) e `node-sass`, uma dependência necessária a partir da versão 2.0.0.

`npm install --save node-sass gatsby-plugin-sass`

2.  Inclua o plugin no seu arquivo  `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

> **Nota**: Você pode configurar [opções adicionais de plugin](/packages/gatsby-plugin-sass/#other-options) como caminhos a serem incluídos e opções para `css-loader`.

3.  Escreva suas folhas de estilo como arquivos `.sass` ou `.scss` e declare ou importe-as normalmente.

```css:styles.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css:styles.sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```javascript
import "./styles.scss"
import "./styles.sass"
```

## Outros recursos

- [Introdução ao Sass](https://designmodo.com/introduction-sass/)
- [Documentação do Sass](https://sass-lang.com/documentation)
- [Starters Gatsby que usam Sass](/starters/?c=Styling%3ASCSS)
