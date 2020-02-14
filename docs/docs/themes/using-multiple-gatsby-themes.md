---
Título: Usando Múltiplos Temas Gatsby
---

Os temas Gatsby podem ser combinados. Isso significa que você pode instalar múltiplos temas juntos.

O `gatsby-starter-theme` é composto por dois temas Gatsby: `gatsby-theme-blog` e `gatsby-theme-notes`

```shell
gatsby new my-notes-blog https://github.com/gatsbyjs/gatsby-starter-theme
```

O tema starter inclui ambos pacotes de temas (`gatsby-theme-blog` e `gatsby-theme-notes`) no arquivo `gatsby-config.js` do tema starter.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-notes`,
      options: {
        mdx: true,
        basePath: `/notes`,
      },
    },
    // com o gatsby-plugin-theme-ui, o último tema na configuração
    // irá sobrescrever o contexto de theme-ui dos outros temas
    { resolve: `gatsby-theme-blog` },
  ],
  siteMetadata: {
    title: `Shadowed Site Title`,
  },
}
```

Na configuração padrão, um blog será rodado no caminho raiz (`/`), e o conteúdo das notas estarão no caminho `/notes`.

Rode `gatsby develop` para iniciar seu servidor de desenvolvimento e visualizar seu site:

![A página inicial criada pelo gatsby-theme-starter](../images/gatsby-theme-starter-home.png)

![A rota de 'notas' criada pelo gatsby-theme-starter](../images/gatsby-theme-starter-notes.png)

## Tutorial

Para um tutorial passo-a-passo, veja [Tutorial "Usando Múltiplos Temas Juntos"](/tutorial/using-multiple-themes-together).
