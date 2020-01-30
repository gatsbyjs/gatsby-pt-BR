---
title: Consultando dados em componentes usando StaticQuery
---

A v2 do Gatsby introduziu a `StaticQuery`, uma nova API que permite componentes receberem dados através de uma query GraphQL.

Neste guia, você verá um exemplo da utilização da `StaticQuery`, e aprender sobre [a diferença entre uma StaticQuery e uma page query](#como-o-staticquery-se-difere-de-uma-page-query).

## Como usar `StaticQuery` nos componentes

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-load-data-using-graphql-queries-directly-in-a-gatsby-v2-component-with-staticquery"
  lessonTitle="Carregar dados utilizando queries GraphQL diretamente num componente Gatsby v2 com a StaticQuery"
/>

### Exemplo Básico

Aqui está um exemplo de um componente `Header` usando` StaticQuery`

```jsx:title=src/components/header.js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

export default () => (
  <StaticQuery
    query={graphql`
      query HeadingQuery {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={data => (
      <header>
        <h1>{data.site.siteMetadata.title}</h1>
      </header>
    )}
  />
)
```

Usando o `StaticQuery`, você pode linkar um componente com seus dados. Não é mais necessário, por exemplo, passar dados do `Layout` para o `Header`.

### useStaticQuery

Há também uma versão React hooks do StaticQuery: confira a documentação em [`useStaticQuery`](/docs/use-static-query/)

### Typechecking

Com o padrão acima, você perde a capacidade de typecheck utilizando PropTypes. Para recuperar o typechecking enquanto obtém o mesmo resultado, você pode alterar o componente para:

```jsx:title=src/components/header.js
import React from "react"
import { StaticQuery, graphql } from "gatsby"
import PropTypes from "prop-types"

const Header = ({ data }) => (
  <header>
    <h1>{data.site.siteMetadata.title}</h1>
  </header>
)

export default props => (
  <StaticQuery
    query={graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={data => <Header data={data} {...props} />}
  />
)

Header.propTypes = {
  data: PropTypes.shape({
    site: PropTypes.shape({
      siteMetadata: PropTypes.shape({
        title: PropTypes.string.isRequired,
      }).isRequired,
    }).isRequired,
  }).isRequired,
}
```

## Como o StaticQuery se difere de uma page query


Uma StaticQuery pode fazer a maioria das coisas que uma page query pode fazer, incluindo fragmentos. As principais diferenças são:

- page queries podem aceitar variáveis (via `pageContext`), mas só podem ser adicionadas aos componentes _page_
- StaticQuery não aceita variáveis (daí o nome "estático"), mas pode ser usado em _qualquer_ componente, incluindo page
- StaticQuery não funciona com chamadas puras do React.createElement; para isso use JSX, por exemplo `<StaticQuery />`
