---
title: MDX Plugins
---


## Plugins Remark do Gatsby
Todos os [plugins gatby-remark](/packages/gatsby-remark-images/?=gatsby-remark) 
são compátiveis com o plugin `gatsby-plugin-mdx`. Um exemplo é o plugin 
[`gatsby-remark-images`](https://next.gatsbyjs.org/packages/gatsby-remark-images/?=gatsby-remark).

Para habilitar o `gatsby-remark-images` você deve instalar os plugins de imagem relevantes:
```shell
yarn add gatsby-plugin-sharp gatsby-remark-images
```
(Se você não tem instalado o plugin `gatsby-source-filesystem`, instale-o.)


É importante agora configurar os plugins instalados. O plugin `gatsby-source-filesystem` deve apontar para onde suas imagens se encontram (em disco), já `gatsby-remark-images` deve ser mencionado no array de plugins  bem como um sub-plugin de `gatsby-plugin-mdx`  e `gatsby-plugin-sharp` pode ser incluído normalmente.


```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    `gatsby-remark-images`,
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        gatsbyRemarkPlugins: [
          {
            resolve: `gatsby-remark-images`,
            options: {
              maxWidth: 1035,
              sizeByPixelDensity: true,
            },
          },
        ],
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`,
      },
    },
  ],
}
```
A partir deste ponto o processamento de imagem do Gatsby automaticamente tomará conta de qualquer imagem em seus arquivos `MDX`

```markdown
![my image](./my-awesome-image.png)
```

## Plugins do Remark

Você pode usar os [plugins do Remark](https://github.com/remarkjs/remark/blob/master/doc/plugins.md) diretamente se desejar fazer transformações em seus documentos `MDX`. Isso permite fazer coisas desde adicionar suporte a emojis à import um padrão de título.

```javascript:title=gatsby-config.js
const capitalize = require(`remark-capitalize`)
const emoji = require(`remark-emoji`)

module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        remarkPlugins: [capitalize, emoji],
      },
    },
  ],
}
```
