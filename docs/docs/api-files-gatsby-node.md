---
title: O arquivo gatsby-node.js da API
---

O código no arquivo `gatsby-node.js` é executado uma vez no processo de construção do seu site. 
Você pode usá-lo para criar páginas dinamicamente, adicionar nós no GraphQL ou responder a eventos durante o ciclo de vida da build. Para usar as [APIs Node do Gatsby](/docs/node-apis/), crie um arquivo chamado `gatsby-node.js` na raiz do seu site. Exporte qualquer uma das APIs que você deseja usar neste arquivo.

Toda API Node do Gatsby passa um [conjunto de helpers da API Node](/docs/node-api-helpers/). 
Isso permite você acessar vários métodos como o de reportar, ou executar ações como criar novas páginas.

```js:title=gatsby-node.js
const path = require(`path`)
// Log out information after a build is done
exports.onPostBuild = ({ reporter }) => {
  reporter.info(`Your Gatsby site has been built!`)
}
// Create blog pages dynamically
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions
  const blogPostTemplate = path.resolve(`src/templates/blog-post.js`)
  const result = await graphql(`
    query {
      allSamplePages {
        edges {
          node {
            slug
            title
          }
        }
      }
    }
  `)
  result.data.allSamplePages.edges.forEach(edge => {
    createPage({
      path: `${edge.node.slug}`,
      component: blogPostTemplate,
      context: {
        title: edge.node.title,
      },
    })
  })
}
```
