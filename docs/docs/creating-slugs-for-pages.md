---
title: Criando _Slugs_ Para Páginas
---

A lógica para criação de _slugs_ a partir de nomes de arquivos pode ser complicada, o _plugin_ `gatsby-source-filesystem` é fornecido com uma função para criá-los.

## Instalação

`npm install --save gatsby-source-filesystem`

## Criação de _slugs_ com gatsby-node.js

Adicione os novos _slugs_ diretamente nos nós `MarkdownRemark`. Todos os dados adicionados aos nós estão disponíveis para futuras consultas com GraphQL.

Para fazer isso, você usará uma função passada para a nossa implementação de API chamada [`createNodeField`](/docs/actions/#createNodeField). Essa função permite a criação de campos adicionais em nós criados por outros _plugins_.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)

// highlight-start
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  // highlight-end
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
    // highlight-end
  }
}
```

## Consulta aos _slugs_ criados

Recarregue e abra o GraphiQL, então execute a seguinte consulta GraphQL para visualizar todos os seus _slugs_:

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        fields {
          slug
        }
      }
    }
  }
}
```
