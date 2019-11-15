---
title: Crie páginas programaticamente a partir de dados
typora-copy-images-to: ./
disableTableOfContents: true
---

> Este tutorial é parte de uma série sobre a camada de dados do Gatsby. Certifique-se que você passou por [part 4](/tutorial/part-four/), [part 5](/tutorial/part-five/), e [part 6](/tutorial/part-six/) antes de continuar aqui.

## O que há neste tutorial?

No tutorial anterior, você criou uma boa página index que consulta arquivos markdown e produziu uma lista de títulos e trechos de postagens de blog. Mas você não quer apenas ver trechos, você quer páginas reais para seus arquivos markdown.

Você pode continuar criando páginas colocando componentes React em `src/pages`. Contudo, você agora vai aprender como _programaticamente_ criar páginas a partir de _dados_. Gatsby _não_ se limita a criar páginas a partir de arquivos como muitos geradores de sites estáticos. Gatsby te permite usar GraphQL para consultar seus _dados_ e _mapear_ os resultados da consulta para _páginas_ — tudo em tempo de compilação. Esta é uma ideia realmente poderosa. Você vai explorar suas implicações e formas de usá-lo no resto desta parte do tutorial.

Vamos começar.

## Criar slugs para páginas

Criar novas páginas tem dois passos:

1.  Gerar a "rota" ou "slug" para a página.
2.  Criar a página.

_**Nota**: Geralmente as fontes de dados fornecem diretamente um slug ou nome de rota para o conteúdo — quando trabalha com um desses sistemas (por exemplo um CMS), você não precisa criar os slugs você mesmo, como faz com os arquivos markdown._

Para criar suas páginas markdown, você vai aprender a usar duas APIs Gatsby:
[`onCreateNode`](/docs/node-apis/#onCreateNode) e
[`createPages`](/docs/node-apis/#createPages). 
Estas são duas APIs workhorse que você verá sendo usadas em vários sites e plugins.

Fazemos nosso melhor para que as APIs Gatsby sejam simples de implementar. 
Para implementar uma API, exporte uma função com o nome da API de `gatsby-node.js`.

Então, aqui é onde você fará isto. Na raiz do seu site, crie um arquivo nomeado `gatsby-node.js`. Logo após adicione o seguinte.

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type)
}
```

Esta função `onCreateNode` será chamada pelo Gatsby sempre que um novo nó é criado (ou atualizado).

Pare e reinicie o servidor de desenvolvimento. Ao fazer isto, verá vários nós recem criados sendo registrados no console do terminal.

Use esta API para adicionar os slugs das suas páginas de markdown para os nós `MarkdownRemark`.

Modifique sua função para que agora apenas registre nós `MarkdownRemark`.

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  // highlight-start
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type)
  }
  // highlight-end
}
```
Você quer utilizar cada nome de arquivo markdown para criar o slug da página. Para que 
`pandas-and-bananas.md` se torne `/pandas-and-bananas/`. 
Mas como você consegue o nome do arquivo do nó `MarkdownRemark`? Para consegui-lo, 
você precisa _atravessar_ o "grafo do nó" até seu nó pai `File`, pois os nós `File` contêm 
dados que você precisa sobre os arquivos em disco. Para fazer isso, modifique sua função novamente:

```javascript:title=gatsby-node.js
// highlight-next-line
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const fileNode = getNode(node.parent)
    console.log(`\n`, fileNode.relativePath)
    // highlight-end
  }
}
```

Após reinicar seu servidor de desenvolvimento, você deve ver as rotas relativas para seus dois 
arquivos markdown impressos na tela do terminal.

![markdown-relative-path](markdown-relative-path.png)

Agora terá que criar slugs. Como a lógica para criar slugs a partir dos nomes de 
arquivo pode ser complicada, o plugin `gatsby-source-filesystem` é fornecido com uma 
função para criar slugs. Vamos usar isso.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`) // highlight-line

exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` })) // highlight-line
  }
}
```

A função lida com a localização do nó pai `File` juntamente com a criação do slug. 
Execute o servidor de desenvolvimento novamente e deverá ver registrado no terminal 
dois slugs, um para cada arquivo markdown.

Agora pode adicionar seus novos slugs diretamente nos nós `MarkdownRemark`. Isto é 
poderoso, já que qualquer dado que você adicione aos nós estará disponível para consulta 
posterior com o GraphQL. Portanto, será fácil obter o slug quando chegar o momento de 
criar as páginas.

Para fazer isso, você usará uma função passada para sua implementação de API chamada 
[`createNodeField`](/docs/actions/#createNodeField). Esta função permite você criar 
campos adicionais em nós criados por outros plugins. Apenas o criador original de um 
nó pode modifica-lo diretamento—todos os outros plugins (incluindo seu `gatsby-node.js`)
devem usar esta função para criar campos adicionais.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)
// highlight-next-line
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions // highlight-line
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

Reinicie o servidor de desenvolvimento e abra ou atualize o GraphQL. Então execute
esta consulta GraphQL para ver seus novos slugs.

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

Agora que os slugs foram criados, você pode criar as páginas.

## Criando páginas

No mesmo arquivo `gatsby-node.js` , adicione o seguinte.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

// highlight-start
exports.createPages = async ({ graphql, actions }) => {
  // **Note:** The graphql function call returns a Promise
  // see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise for more info
  const result = await graphql(`
    query {
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
  `)

  console.log(JSON.stringify(result, null, 4))
}
// highlight-end
```

Você adicionou uma implementação de [`createPages`](/docs/node-apis/#createPages) da API 
que Gatsby chama para que plugins possam adicionar páginas.

Conforme foi mencionado na introdução desta parte do tutorial, os passos para criar páginas programaticamente são:

1.  Consultar dados com GraphQL
2.  Mapear os resultados das consultas às páginas

O código acima é o primeiro passo para criar páginas a partir de seu markdown, 
já que está usando a função `graphql` fornecida para consultar os slugs markdown que criou. 
Então você está efetuando logout do resultado da consulta, que deve se parecer com:

![query-markdown-slugs](query-markdown-slugs.png)

Você precisa de uma coisa adicional além de um slug para criar páginas: um componente 
de template de página. Como tudo no Gatsby, as páginas programáticas funcionam com 
componentes React. Quando criar uma página, você precisa especificar que componente usar.

Crie um diretório em `src/templates`, e então adicione o seguinte em um arquivo chamado 
`src/templates/blog-post.js`.

```jsx:title=src/templates/blog-post.js
import React from "react"
import Layout from "../components/layout"

export default () => {
  return (
    <Layout>
      <div>Hello blog post</div>
    </Layout>
  )
}
```

Atualize `gatsby-node.js`

```javascript:title=gatsby-node.js
const path = require(`path`) // highlight-line
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions // highlight-line
  const result = await graphql(`
    query {
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
  `)

  // highlight-start
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/templates/blog-post.js`),
      context: {
        // Data passed to context is available
        // in page queries as GraphQL variables.
        slug: node.fields.slug,
      },
    })
  })
  // highlight-end
}
```

Reinicie o servidor de desenvolvimento e suas páginas serão criadas! Uma maneira fácil 
de encontrar novas páginas criadas durante o desenvolvimento é ir para uma rota aleatória 
onde o Gatsby mostrará uma lista de páginas no site. Se você for para <http://localhost:8000/sdf>, 
verá as novas páginas que criou.

![new-pages](new-pages.png)

Visite uma delas e verá:

![hello-world-blog-post](hello-world-blog-post.png)

O que é um pouco chato e não o que você quer. Agora você pode obter dados de sua postagem markdown. Altere
`src/templates/blog-post.js` para:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-start
export default ({ data }) => {
  const post = data.markdownRemark
  // highlight-end
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

// highlight-start
export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`
// highlight-end
```

E…

![blog-post](blog-post.png)

Lindo!

O último passo é vincular suas novas páginas a partir da página index.

Volte para `src/pages/index.js`, consulte seus slugs markdown, e crie links.

```jsx:title=src/pages/index.js
import React from "react"
import { css } from "@emotion/core"
import { Link, graphql } from "gatsby" // highlight-line
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Pandas incríveis comendo coisas
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            {/* highlight-start */}
            <Link
              to={node.fields.slug}
              css={css`
                text-decoration: none;
                color: inherit;
              `}
            >
              {/* highlight-end */}
              <h3
                css={css`
                  margin-bottom: ${rhythm(1 / 4)};
                `}
              >
                {node.frontmatter.title}{" "}
                <span
                  css={css`
                    color: #bbb;
                  `}
                >
                  — {node.frontmatter.date}
                </span>
              </h3>
              <p>{node.excerpt}</p>
            </Link> {/* highlight-line */}
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC }) {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          // highlight-start
          fields {
            slug
          }
          // highlight-end
          excerpt
        }
      }
    }
  }
`
```

E aí está! Um blog funcionando, mesmo que pequeno.

## Desafio

Tente brincar mais com o site. Tente adicionar mais alguns arquivos markdown. 
Explore consultando outros dados dos nós MarkdownRemark e adicione-os à 
primeira página ou às páginas de postagens do blog.

Nesta parte do tutorial, você aprendeu os conceitos básicos de construção 
com a camada de dados Gatsby. Você aprendeu como _originar_ e _transformar_ dados 
usando plugins, como usar o GraphQL para mapear dados para páginas e, em 
seguida, como criar _componentes de template de página_ onde você consulta 
dados para cada página.

## O que vem depois?

Agora que você criou um site Gatsby, para onde irá?

- Compartilhe seu site Gatsby no Twitter e veja o que outras pessoas criaram pesquisando #gatsbytutorial! Não se esqueça de mencionar @gatsbyjs no seu Tweet e incluir a hashtag #gatsbytutorial :)
- Você pode dar uma olhada em alguns [exemplos de site](https://github.com/gatsbyjs/gatsby/tree/master/examples#gatsby-example-websites)
- Explore mais [plugins](/docs/plugins/)
- Veja o que [outras pessoas estão criando com Gatsby](/showcase/)
- Confira a documentação em [Gatsby's APIs](/docs/api-specification/), [nodes](/docs/node-interface/), ou [GraphQL](/docs/graphql-reference/)
