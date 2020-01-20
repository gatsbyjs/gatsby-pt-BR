---
title: PostCSS
---

PostCSS transforma sintaxes e funcionalidades extensas em um CSS moderno e compatível com o browser. Este guia vai lhe mostrar como começar a usar o Gatsby e PostCSS juntos.

## Instalando e Configurando o PostCSS

Este guia supõe que você já tenha o Gatsby configurado em seu projeto. Caso você precise configura-lo, leia o [**Início Rápido**](/docs/quick-start/) antes de seguir.

1.  Instale o plugin do Gatsby [**gatsby-plugin-postcss**](/packages/gatsby-plugin-postcss/).

`npm install --save gatsby-plugin-postcss`

2.  Adicione o plugin em seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-postcss`],
```

> **Nota**: Se você precisar passar opções para o PostCSS, use as opções do plugin; Veja todas as opções disponíveis em [postcss-loader](https://github.com/postcss/postcss-loader).

3.  Escreva suas folhas de estilos usando o PostCSS (Arquivos .css) e importe ou faça `require` normalmente.

```css:styles.css
@custom-media --med (width <= 50rem);

@media (--med) {
  a {
    &:hover {
      color: color-mod(black alpha(54%));
    }
  }
}
```

```javascript
import "./styles.css"
```

### Com Módulos CSS

Não é necessário configuração inicial para utilizar módulos CSS. Apenas adicione `.module` a extensão. Por exemplo: `App.css -> App.module.css`. Qualquer arquivo com a extensão `.module` irá usar os módulos CSS.

### Plugins PostCSS

Se você preferir adicionar um postprocessing adicional a sua saída PostCSS, você pode especificar os plugins nas opções:

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-plugin-postcss`,
    options: {
      postCssPlugins: [require(`postcss-preset-env`)({ stage: 0 })],
    },
  },
],
```

Outra alternativa, você pode usar `postcss.config.js` para especificar sua própria configuração do PostCSS:

```javascript:title=postcss.config.js
const postcssPresetEnv = require(`postcss-preset-env`)

module.exports = () => ({
  plugins: [
    postcssPresetEnv({
      stage: 0,
    }),
  ],
})
```

## Outros Recursos

- [Introdução ao postcss](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)
