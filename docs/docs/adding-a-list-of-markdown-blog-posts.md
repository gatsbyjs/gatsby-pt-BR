---
title: Adicionando uma Lista de Marcações de Posts no Blog
---

Depois de adicionar as páginas de marcações ao seu site, você fica a apenas um passo de poder listar suas postagens em uma página de índice dedicada.

### Criando postagens

Conforme descrito [aqui](/docs/adding-markdown-pages), você terá que criar suas postagens nos arquivos do Markdown, que irá se parecer com isto:

```md
---
path: "/blog/my-first-post"
date: "2017-11-07"
title: "My first blog post"
---

Alguém já ouviu falar sobre o GatsbyJS?
```

### Criando a página

O primeiro passo será criar a página que exibirá suas postagens, em `src/pages/`. Você pode, por exemplo, usar o `index.js`.

```jsx:title=src/pages/index.js
import React from "react"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // You can filter your posts based on some criteria
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage
```

## Criando a consulta GraphQL

Segundo, você precisa fornecer os dados para o seu componente com uma consulta GraphQL. Vamos adicioná-lo, para que o `index.js` se pareça com isto:

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // You can filter your posts based on some criteria
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage

export const pageQuery = graphql`
  query {
    allMarkdownRemark(sort: { order: DESC, fields: [frontmatter___date] }) {
      edges {
        node {
          id
          excerpt(pruneLength: 250)
          frontmatter {
            date(formatString: "MMMM DD, YYYY")
            path
            title
          }
        }
      }
    }
  }
`
```

### Criando o componente `PostLink`

A única coisa que resta a fazer é adicionar o componente `PostLink`. Crie um novo arquivo `post-link.js` em` src/components/` e adicione o seguinte:

```jsx:title=src/components/post-link.js
import React from "react"
import { Link } from "gatsby"

const PostLink = ({ post }) => (
  <div>
    <Link to={post.frontmatter.path}>
      {post.frontmatter.title} ({post.frontmatter.date})
    </Link>
  </div>
)

export default PostLink
```

Isso deve gerar uma página com suas postagens classificadas por data decrescente. Você pode personalizar ainda mais o `frontmatter` e os componentes de página e `PostLink` para obter os efeitos desejados!