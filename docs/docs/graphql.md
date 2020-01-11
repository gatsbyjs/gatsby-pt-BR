---
title: GraphQL & Gatsby
overview: true
---

Ao trabalhar com Gatsby, você acessa os seus dados através de uma linguagem de consulta chamada [GraphQL](http://graphql.org/). O GraphQL permite que você expresse os dados que você precisa de forma declarativa. Isso é feito através de consultas, `queries`. Consultas são uma representação dos dados que você precisa. Uma consulta tem o seguinte formato:

```graphql
{
  site {
    siteMetadata {
      title
    }
  }
}
```

Que retorna o seguinte resultado:

```json
{
  "site": {
    "siteMetadata": {
      "title": "A Gatsby site!"
    }
  }
}
```

Note como o formato da consulta tem exatamente o mesmo formato dos dados retornados em JSON. Isso é possivel por que em GraphQL, a consulta é comparada com um modelo de dados, `schema`, que é a representação dos dados disponíveis. Não se preocupe ainda sobre de onde vem o modelo de dados. O Gatsby organiza todos os seus dados para você e os torna acessíveis através de uma ferramenta chamada GraphiQL. GraphiQL é uma interface gráfica que permite que você 1) faça consultas em seus dados usando o navegador de sua preferência, e 2) investigue a estrutura dos dados disponíveis a você através de uma ferramenta de exploração de estruturas de dados.

Se você quiser saber mais sobre GraphQL, você pode ler sobre o [porque do Gatsby adotar essa tecnologia](/docs/why-gatsby-uses-graphql/), e conferir o [guia conceitual](/docs/querying-with-graphql/) sobre como consultar dados utilizando o GraphQL.

<GuideList slug={props.slug} />
