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

Note como o formato da consulta tem exatamento o mesmo formato dos dados retornados em JSON. Isso é possivel por que em GraphQL, a consulta é comparada com um modelo de dados, `schema`, que é a representação dos dados disponíveis. Não se preocupe ainda sobre de onde vem o modelo de dados. O Gatsby organiza todos os seus dados para você e os torna acessíveis através de uma ferramenta chamada GraphiQL. GraphiQL e uma interface gráfica que permite que você 1) faça consultas em seus dados através do navegador, e 2) investigue a estrutura dos dados disponiveis a você através de um navegador de tipo de dados.

Se você quiser saber mais sobre GraphQL, você pode ler sobre o [porquê do Gatsby usar isso](/docs/why-gatsby-uses-graphql/), e conferir o [guia conceitual](/docs/querying-with-graphql/) sobre a consulta de dados utilizando GraphQL.

<GuideList slug={props.slug} />
