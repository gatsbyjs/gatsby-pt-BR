---
title: Criando e modificando páginas
---

O Gatsby facilita a manipulação programática das suas páginas.

As páginas podem ser criadas de três maneiras:

- Através da implementação da API [`createPages`](/docs/node-apis/#createPages) no arquivo gatsby-node.js do seu site.
- O Gatsby core automaticamente transforma os componentes React nas `src/pages` em páginas.
- Plugins também pode implementar o `createPages` e criar páginas para você.

Você também pode implementar a API [`onCreatePage`](/docs/node-apis/#onCreatePage) caso queira modificar páginas criadas no Gatsby core, por plugins ou também criar [rotas apenas-para-clientes](/docs/building-apps-with-gatsby/).

## Ajuda na depuração

Para ver quais páginas estão sendo criadas pelo seu código ou plugins, você pode consultar as informações da página enquanto desenvolve no Graph*i*QL. Cole a seguinte consulta na IDE do Graph*i*QL para o seu site. A IDE do Graph*i*QL fica disponível ao executar o servidor de desenvolvimento do seu site na `HOST:PORT/___graphql` e.g.
`localhost:8000/___graphql`.

```graphql
{
  allSitePage {
    edges {
      node {
        path
        component
        pluginCreator {
          name
          pluginFilepath
        }
      }
    }
  }
}
```

A propriedade `context` aceita objetos, então podemos passar quaisquer dados que nós queiramos que a página possa acessar. 

Você também pode consultar quaisquer dados `context` adicionadas por você ou pelos plugins utilizados.

> **NOTA:** Existem algumas palavras reservadas que _não_ podem ser utilizadas no `context`. As palavras são: `path`, `matchPath`, `component`, `componentChunkName`, `pluginCreator___NODE`, e `pluginCreatorId`.

## Criando páginas no gatsby-node.js

Frequentemente, você precisará criar páginas através de código. Por exemplo, você terá arquivos markdown, onde cada um deve ser uma página.

Esse exemplo assume que cada página markdown tem um `path` definido no _frontmatter_ do arquivo markdown.

```javascript:title=gatsby-node.js
// Implemente a API do Gatsby "createPages". Isso é executado quando a camada
// de dados é inicializada, a fim de permitir que os plugins criem as páginas
// a partir de dados
exports.createPages = async ({ graphql, actions, reporter }) => {
  const { createPage } = actions

  // Pesquisa nós markdown para usar na criação das páginas.
  const result = await graphql(
    `
      {
        allMarkdownRemark(limit: 1000) {
          edges {
            node {
              frontmatter {
                path
              }
            }
          }
        }
      }
    `
  )

  // Manipula erros
  if (result.errors) {
    reporter.panicOnBuild(`Error while running GraphQL query.`)
    return
  }

  // Cria páginas para cada arquivo markdown.
  const blogPostTemplate = path.resolve(`src/templates/blog-post.js`)
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    const path = node.frontmatter.path
    createPage({
      path,
      component: blogPostTemplate,

      // Na consulta graphql do template do seu blog, você pode usar a variável GraphQL para consultar dados dos arquivos markdown.
      context: {
        path,
      },
    })
  })
}
```

## Modificando páginas criadas pelo Gatsby core ou por plugins

Tanto o Gatsby core quanto plugins podem criar páginas para você de forma automática. Algumas vezes o padrão criado não é exatamente o que você quer e, por isso, você precisará modificar essas páginas criadas.


### Removendo barras à direita

Uma razão comum para modificar automaticamente páginas já criadas é a remoção de barras à direita

Para isso, no arquivo `gatsby-node.js` do seu site adicione um código similar ao seguinte:

_Nota: Existe um plugin que irá remover todos as barras à direita das páginas automaticamente:
[plugin-gatsby-que-remove-as-barras-à-direita](/packages/gatsby-plugin-remove-trailing-slashes/)_.

_Nota: Caso você precise fazer uma ação assíncrona no `onCreatePage` você pode retornar uma _promise_ ou usar uma função `async`._

```javascript:title=gatsby-node.js
// substituir o '/' resultaria em uma string vazia, o que é inválido.
const replacePath = path => (path === `/` ? path : path.replace(/\/$/, ``))
// Implemente a API do Gatsby “onCreatePage”. Isso é
// executado logo que uma página é criada
exports.onCreatePage = ({ page, actions }) => {
  const { createPage, deletePage } = actions

  const oldPage = Object.assign({}, page)
  // Remove a barra à direita a não ser que a página seja /
  page.path = replacePath(page.path)
  if (page.path !== oldPage.path) {
    // substitui a página antiga pela nova
    deletePage(oldPage)
    createPage(page)
  }
}
```

### Adicionar contexto à páginas

As páginas criadas automaticamente podem receber contextos e usá-lo como variáveis nas consultas da GraphQL. Para substituir o padrão e usar o seu próprio contexto, abra o arquivo `gatsby-node.js` do seu site e adicione um código similar ao seguinte:

```javascript:title=gatsby-node.js
exports.onCreatePage = ({ page, actions }) => {
  const { createPage, deletePage } = actions

  deletePage(page)
  // Você pode acessar a variável "house" nas consultas da sua paǵina.
  createPage({
    ...page,
    context: {
      ...page.context,
      house: `Gryffindor`,
    },
  })
}
```
Nas suas páginas e templates, você pode acessar seu contexto através do suporte `pageContext` dessa maneira:

```jsx
import React from "react"

const Page = ({ pageContext }) => {
  return <div>{pageContext.house}</div>
}

export default Page
```
O contexto da página é serializado antes de ser passado para as páginas: Isso significa que ele não pode ser usado para transformar funções em componentes


## Criando rotas somente para clientes

Em casos específicos, talvez você queira criar sites com porções apenas para clientes que são bloqueadas por autenticação. Para saber como fazê-lo, recorra ao [Rotas apenas-para-clientes & autenticação de usuário](https://www.gatsbyjs.org/docs/client-only-routes-and-user-authentication/).
