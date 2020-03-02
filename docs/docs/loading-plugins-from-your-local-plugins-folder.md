---
title: Carregando plugins da sua pasta local de plugins
---

O Gatsby também pode carregar plugins da pasta local de plugins do seu site, que é uma pasta chamada `plugins` no diretório raiz do site.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-local-plugin`],
}
```

Se você deseja fazer referência a um plugin que não está na pasta de plugins, use algo como o seguinte:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    // Atalho para adicionar plugins sem opções.
    "gatsby-plugin-react-helmet",
    {
      // Exemplo de plugin padrão com opções
      resolve: require.resolve(`/path/to/gatsby-local-plugin`),
    },
  ],
}
```