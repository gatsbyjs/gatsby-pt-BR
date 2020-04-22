---
title: PostCSS
---

PostCSS transforma sintaxes e funcionalidades extensas em um CSS moderno e compatível com o browser. Este guia vai lhe mostrar como começar a usar o Gatsby e PostCSS juntos.

<<<<<<< HEAD
## Instalando e Configurando o PostCSS

Este guia supõe que você já tenha o Gatsby configurado em seu projeto. Caso você precise configurá-lo, leia o [**Guia de Início Rápido**](/docs/quick-start/) antes de seguir.

1.  Instale o plugin do Gatsby [**gatsby-plugin-postcss**](/packages/gatsby-plugin-postcss/).
=======
## Installing and configuring PostCSS

<<<<<<< HEAD
This guide assumes that you have a Gatsby project set up. If you need to set up a project, head to the [quick start guide](/docs/quick-start/), then come back.

1.  Install the Gatsby plugin [gatsby-plugin-postcss](/packages/gatsby-plugin-postcss/).
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

=======
>>>>>>> master
```shell
npm install --save gatsby-plugin-postcss
```

2.  Adicione o plugin em seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-postcss`],
```

> **Nota**: Se você precisar passar opções para o PostCSS, use as opções do plugin; Veja todas as opções disponíveis em [postcss-loader](https://github.com/postcss/postcss-loader).

<<<<<<< HEAD
3.  Escreva suas folhas de estilos usando o PostCSS (arquivos .css) e importe ou faça `require` normalmente.
=======
3.  Write your stylesheets using PostCSS (`.css` files) and require or import them as normal.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```css:title=styles.css
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

<<<<<<< HEAD
### Com Módulos CSS
=======
### With CSS modules
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Não é necessário configuração inicial para utilizar módulos CSS. Apenas adicione `.module` a extensão. Por exemplo: `App.css -> App.module.css`. Qualquer arquivo com a extensão `.module` irá usar os módulos CSS.

### Plugins PostCSS

Se você preferir adicionar um pós-processamento adicional a sua saída PostCSS, você pode especificar os plugins nas opções:

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
