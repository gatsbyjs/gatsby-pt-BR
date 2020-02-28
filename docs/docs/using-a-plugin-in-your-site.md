---
title: Usando um Plugin em Seu Site
---

Plugins do Gatsby são pacotes do Node.js, assim você pode instalar eles como qualquer outro pacote do Node usando NPM.

Por exemplo, `gatsby-transformer-json` é um pacote que adiciona suporte para arquivos JSON na camada de dados do Gatsby.

Para instalar ele, execute na raiz do seu site:

```shell
npm install --save gatsby-transformer-json
```

Então, no `gatsby-config.js` do seu site, você adiciona `gatsby-transformer-json` ao array de plugins desta forma:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-transformer-json`],
}
```

Plugins podem ter opções. Por exemplo:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    // Atalho para adicionar plugins sem opções.
    "gatsby-plugin-react-helmet",
    {
      // Exemplo padrão de plugin com opções.
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/data/`,
        name: "data",
      },
    },
    {
      resolve: "gatsby-plugin-offline",
      // Opções em branco, equivalentes ao plugin somente string.
      options: {
        plugins: [],
      },
    },
    {
      resolve: `gatsby-transformer-remark`,
      options: {
        // Plugins dentro de plugins.
        plugins: [`gatsby-remark-smartypants`],
      },
    },
  ],
}
```

Note que as opções do plugin serão convertidas em string pelo Gatsby, então elas não podem ser funções.
