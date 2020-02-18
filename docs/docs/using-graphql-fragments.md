---
<<<<<<< HEAD:docs/docs/using-fragments.md
title: Utilizando Fragmentos
=======
title: Using GraphQL Fragments
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1:docs/docs/using-graphql-fragments.md
---

Fragmentos permitem a reutilização de consultas GraphQL. Elas também permitem a divisão de consultas complexas em componentes menores e de fácil compreensão.

## Os blocos que compõem um fragmento

Aqui temos um exemplo de fragmento:

```graphql
fragment FragmentName on TypeName {
  campo1
  campo2
}
```

Um fragmento consiste de três componentes:

1. `FragmentName`: o nome do fragmento que será referenciado posteriormente.
2. `TypeName`: o [tipo de objeto GraphQL](https://graphql.org/graphql-js/object-types/) no qual o fragmento será utilizado. Isso é importante porque só é possível consultar campos que existam em um determinado objeto.
3. O corpo da consulta. Pode-se definir quaisquer campos em qualquer nível de aninhamento, da mesma maneira que seria feito em outras consultas GraphQL.

## Criando e utilizando um fragmento

<<<<<<< HEAD:docs/docs/using-fragments.md
Um fragmento pode ser criado dentro de qualquer consulta GraphQL, mas é uma boa prática criar a consulta separadamente. Mais conselhos organizacionais no [Guia Conceitual](/docs/querying-with-graphql/#fragments).
=======
A fragment can be created inside any GraphQL query, but it's good practice to create the query separately. More organization advice in the [Conceptual Guide](/docs/graphql-concepts/#fragments).
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1:docs/docs/using-graphql-fragments.md

```jsx:title=src/components/IndexPost.jsx
import React from "react"
import { graphql } from "gatsby"

export default ( props ) => {
  return (...)
}

export const query = graphql`
  fragment SiteInformation on Site {
    siteMetadata {
      title
      siteDescription
    }
  }
`
```

Isto define um fragmento chamado `SiteInformation`. Agora, ele pode ser utilizado internamente na busca GraphQL da página:

```jsx:title=src/pages/main.jsx
import React from "react"
import { graphql } from "gatsby"
import IndexPost from "../components/IndexPost"

export default ({ data }) => {
  return (
    <div>
      <h1>{data.site.siteMetadata.title}</h1>
      <p>{data.site.siteMetadata.siteDescription}</p>

      {/*
        Ou é possível passar todos os dados do fragmento
        de volta ao componente que o definiu
      */}
      <IndexPost siteInformation={data.site.siteMetadata} />
    </div>
  )
}

export const query = graphql`
  query {
    site {
      ...SiteInformation
    }
  }
`
```

<<<<<<< HEAD:docs/docs/using-fragments.md
Ao compilar o site, o Gatsby pré-processa todas as consultas GraphQL encontradas, portanto, qualquer arquivo incluso no seu projeto pode definir um trecho. No entanto, apenas Páginas podem definir consultas GraphQL que realmente retornem dados, por isso que é possível definir fragmentos no arquivo do componente - ele não retorna nenhum dado diretamente.
=======
When compiling your site, Gatsby preprocesses all GraphQL queries it finds. Therefore, any file that gets included in your project can define a snippet. However, only Pages can define GraphQL queries that actually return data. This is why you can define the fragment in the component file - it doesn't actually return any data directly.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1:docs/docs/using-graphql-fragments.md

## Leituras Adicionais

<<<<<<< HEAD:docs/docs/using-fragments.md
- [Consultando Dados com GraphQL - Fragmentos](/docs/querying-with-graphql/#fragments)
- [Documentação GraphQL - Fragmentos](https://graphql.org/learn/queries/#fragments)
=======
- [Querying Data with GraphQL - Fragments](/docs/graphql-concepts/#fragments)
- [GraphQL Docs - Fragments](https://graphql.org/learn/queries/#fragments)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1:docs/docs/using-graphql-fragments.md
