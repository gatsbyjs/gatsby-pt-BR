---
title: Conceitos de GraphQL
---

import LayerModel from "../../www/src/components/layer-model"

Existem muitas opções para carregar dados nos componentes do React. Uma das mais
populares e poderosas é uma tecnologia chamada
[GraphQL](http://graphql.org/).

O GraphQL foi inventado no Facebook para ajudar os engenheiros de produto a _puxar_ os dados necessários para os
componentes React

GraphQL é uma **q**uery **l**anguage (a parte _QL_ do seu nome). Se vocês são
familiarizado com o SQL, ele funciona de maneira muito semelhante. Usando uma sintaxe especial, você descreve
os dados que você deseja no seu componente e, em seguida, esses dados são fornecidos
para você.

Gatsby usa GraphQL para habilitar [componentes de página e 
StaticQuery](/docs/building-with-components/) para declarar quais dados eles e seus
subcomponentes precisam. Em seguida, Gatsby disponibiliza esses dados no
navegador quando necessário pelos seus componentes.

Dados de várias fontes são tornados consultáveis ​​em uma camada unificada, uma parte essencial do processo de criação do Gatsby:

<LayerModel initialLayer="Data" />

## Por que o GraphQL é tão legal?

Para uma visão mais aprofundada, leia [por que o Gatsby usa o GraphQL](/docs/why-gatsby-uses-graphql/).

- Elimine o clichê de dados do frontend - não é necessário se preocupar em solicitar e aguardar dados. Basta solicitar os dados que você precisa com uma consulta GraphQL e eles aparecerão quando você precisar
- Empurre a complexidade do frontend para consultas — muitas transformações de dados podem ser feitas em _build-time_ dentro de suas consultas GraphQL
- É a linguagem de consulta de dados perfeita para as dependências de dados frequentemente complexas/aninhadas dos aplicativos modernos
- Melhore o desempenho removendo o inchaço dos dados — O GraphQL permite selecionar apenas os dados necessários, não o que uma API retornar

## Como é uma consulta no GraphQL?

O GraphQL permite que você solicite os dados exatos que você necessita. As consultas se parecem com JSON:

```graphql
{
  site {
    siteMetadata {
      title
    }
  }
}
```

A qual retorna isso:

```json
{
  "site": {
    "siteMetadata": {
      "title": "A Gatsby site!"
    }
  }
}
```

Um componente de página básico com uma consulta GraphQL pode ter a seguinte aparência:

```jsx
import React from "react"
import { graphql } from "gatsby"

export default ({ data }) => (
  <div>
    <h1>About {data.site.siteMetadata.title}</h1>
    <p>We're a very cool website you should return to often.</p>
  </div>
)

export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
```

O resultado da consulta é inserido automaticamente no seu componente React
na prop `data`. GraphQL e Gatsby te permitem solicitar dados e, em seguida,
começar a usá-los imediatamente.

**Nota:** Para executar consultas GraphQL em componentes que não são de página, você precisará usar o [recurso de consulta estática do Gatsby](/docs/static-query/).

### Compreendendo as partes de uma consulta

O diagrama a seguir mostra uma consulta GraphQL, com cada palavra destacada em uma cor correspondente ao seu nome na legenda:

![Diagrama de consulta GraphQL](./images/basic-query.png)

#### Tipo de operação de consulta

O diagrama marca a palavra `query` como o "Tipo de Operação ", para casos de uso com o Gatsby o único tipo de operação com o qual você lidará é `query`; isso pode ser omitido das suas consultas, se você preferir (como no exemplo acima).

#### Nome da Operação

`SiteInformation` está marcado como "Nome da operação", que é um nome exclusivo que você mesmo atribui a uma consulta. Isso é semelhante a como você nomearia uma função ou variável e, como uma função, isso pode ser omitido se você preferir que a consulta seja anônima.

#### Campos de consulta

As quatro palavras `site`, `id`, `siteMetadata` e `title` são marcadas como "Campos". Quaisquer campos de nível superior -- como `site` no diagrama -- às vezes são chamados de **campos no nível raiz**, embora o nome não tenha significância funcional, pois todos os campos nas consultas do GraphQL se comportam da mesma maneira.

## Como aprender GraphQL

Sua experiência desenvolvimento com o Gatsby pode ser a primeira vez que você vê o GraphQL! Esperamos que você goste tanto
como nós e ache-o útil para todos os seus projetos.

Ao iniciar o GraphQL, recomendamos os dois tutoriais a seguir:

- https://www.howtographql.com/
- http://graphql.org/learn/

[O tutorial oficial do Gatsby](/tutorial/part-four/) também inclui uma introdução ao uso do GraphQL especificamente com o Gatsby.

## Como o GraphQL e o Gatsby trabalham juntos?

Uma das grandes vantagens do GraphQL é a sua flexibilidade. As pessoas usam o GraphQL
com [muitas linguagens de programação diferentes](http://graphql.org/code/), para aplicativos web e nativos.

A maioria das pessoas executa o GraphQL em um servidor para responder ao vivo a solicitações de
dados de clientes. Você define um schema (um schema é uma maneira formal de descrever
o formato dos seus dados) para o seu servidor GraphQL e, em seguida, seus resolvers GraphQL
recebem dados de bancos de dados e/ou outras APIs.

Gatsby usa o GraphQL em _build-time_ e _não_ para sites
ao vivo. Isso é único e significa que você não precisa executar serviços adicionais (por exemplo, um banco de dados
e um servidor Node.js) usar o GraphQL para sites de produção.

Gatsby é um ótimo framework para criar aplicativos, por isso é possível e incentivado
emparelhar o GraphQL nativo em tempo de construção do Gatsby com consultas GraphQL executando em
um servidor GraphQL ativo a partir do navegador.

## De onde vem o schema GraphQL do Gatsby?

A maioria dos usos do GraphQL envolve a criação manual de um schema GraphQL.

O Gatsby usa plugins que podem buscar dados de diferentes fontes. Esses dados são usados ​​para _inferir_ automaticamente um schema do GraphQL.

Se você fornecer dados ao Gatsby com esta aparência:

```json
{
  "title": "A long long time ago"
}
```

O Gatsby criará um schema parecido com isso:

```
title: String
```

Isso facilita a extração de dados de qualquer lugar e a escrita imediata
de consultas GraphQL nos seus dados.

Isso pode causar confusão, pois algumas fontes de dados permitem definir
um schema mesmo quando não há dados adicionados para partes ou todo o schema. Se partes dos dados não foram adicionadas, essas partes do schema podem não ser recriadas no Gatsby.

## Transformações de dados poderosas

O GraphQL habilita outro recurso exclusivo do Gatsby - permite controlar transformações de dados com argumentos para suas consultas. Alguns exemplos a seguir.

### Formatando datas

As pessoas costumam armazenar datas como "2018-01-05", mas desejam exibir a data de alguma outra forma, como "5 de janeiro de 2018". Uma maneira de fazer isso é carregar uma biblioteca JavaScript de formatação de data no navegador. Ou, com a camada GraphQL de Gatsby, você pode fazer a formatação no momento da consulta, como:

```graphql
{
  date(formatString: "MMMM Do, YYYY")
}
```

Veja a lista completa de opções de formatação, visualizando nossa [página de referência do GraphQL](/docs/graphql-reference/#dates).

### Markdown

O Gatsby possui plugins _transformer_ que podem transformar dados de um formato para outro. Um exemplo comum é markdown. Se você instalar [`gatsby-transformer-remark`](/packages/gatsby-transformer-remark/), então em suas consultas, você pode especificar se deseja a versão HTML transformada em vez da markdown:

```graphql
markdownRemark {
  html
}
```

### Imagens

Gatsby tem um rico suporte para o processamento de imagens. As imagens responsivas são uma grande parte da web moderna e geralmente envolvem a criação de miniaturas de mais de 5 tamanhos por foto. Com o [`gatsby-transformer-sharp`](/packages/gatsby-transformer-sharp/) do Gatsby, você pode _consultar_ suas imagens para versões responsivas. A consulta cria automaticamente todas as miniaturas responsivas necessárias e retorna os campos `src` e `srcSet` para adicionar ao seu elemento de imagem.

Combinado com um componente especial de imagem do Gatsby, [gatsby-image](/packages/gatsby-image/), você tem um conjunto muito poderoso de primitivas para criar sites com imagens.

É assim que um componente usando `gatsby-image` se parece:

```jsx
import React from "react"
import Img from "gatsby-image"
import { graphql } from "gatsby"

export default ({ data }) => (
  <div>
    <h1>Hello gatsby-image</h1>
    <Img fixed={data.file.childImageSharp.fixed} />
  </div>
)

export const query = graphql`
  query {
    file(relativePath: { eq: "blog/avatars/kyle-mathews.jpeg" }) {
      childImageSharp {
        # Specify the image processing specifications right in the query.
        # Makes it trivial to update as your page's design changes.
        fixed(width: 125, height: 125) {
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`
```

Veja também as seguintes postagens do blog:

- [Tornar a Construção de Sites Divertida](/blog/2017-10-16-making-website-building-fun/)
- [Otimização de Imagem Simplificada com Gatsby.js](https://medium.com/@kyle.robert.gill/ridiculously-easy-image-optimization-with-gatsby-js-59d48e15db6e)

## Avançado

### Fragmentos

Observe que no exemplo acima para [consultar imagens](#images), usamos `...GatsbyImageSharpFixed`, que é um fragmento de GraphQL, um conjunto reutilizável de campos para composição da consulta. Você pode ler mais sobre eles [aqui](http://graphql.org/learn/queries/#fragments).

Se você deseja definir seus próprios fragmentos para uso em seu aplicativo, pode usar exportações nomeadas para exportá-los para qualquer arquivo JavaScript, e eles serão processados ​​automaticamente pelo Gatsby para uso em suas consultas GraphQL.

Por exemplo, se eu colocar um fragmento em um componente auxiliar, posso usá-lo em qualquer outra consulta:

```jsx:title=src/components/PostItem.js
export const markdownFrontmatterFragment = graphql`
  fragment MarkdownFrontmatter on MarkdownRemark {
    frontmatter {
      path
      title
      date(formatString: "MMMM DD, YYYY")
    }
  }
`
```

Eles podem ser usados ​​em qualquer consulta GraphQL depois disso!

```graphql
query($path: String!) {
  markdownRemark(frontmatter: { path: { eq: $path } }) {
    ...MarkdownFrontmatter
  }
}
```

É uma boa prática para os seus componentes auxiliares definir e exportar um fragmento para os dados de que precisam. Por exemplo, em sua página de índice, você pode mapear todas as suas postagens para mostrá-las em uma lista.

```jsx:title=src/pages/index.jsx
import React from "react"
import { graphql } from "gatsby"

export default ({ data }) => {
  return (
    <div>
      <h1>Index page</h1>
      <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
      {data.allMarkdownRemark.edges.map(({ node }) => (
        <div key={node.id}>
          <h3>
            {node.frontmatter.title} <span>— {node.frontmatter.date}</span>
          </h3>
        </div>
      ))}
    </div>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
        }
      }
    }
  }
`
```

Se o componente index ficar muito grande, convém refatorá-lo em componentes menores.

```jsx:title=src/components/IndexPost.jsx
import React from "react"
import { graphql } from "gatsby"

export default ({ frontmatter: { title, date } }) => (
  <div>
    <h3>
      {title} <span>— {date}</span>
    </h3>
  </div>
)

export const query = graphql`
  fragment IndexPostFragment on MarkdownRemark {
    frontmatter {
      title
      date(formatString: "MMMM DD, YYYY")
    }
  }
`
```

Agora, você pode usar o componente junto com o fragmento exportado na sua página de índice.

```jsx:title=src/pages/index.jsx
import React from "react"
import IndexPost from "../components/IndexPost"
import { graphql } from "gatsby"

export default ({ data }) => {
  return (
    <div>
      <h1>Index page</h1>
      <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
      {data.allMarkdownRemark.edges.map(({ node }) => (
        <div key={node.id}>
          <IndexPost frontmatter={node.frontmatter} />
        </div>
      ))}
    </div>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          ...IndexPostFragment
        }
      }
    }
  }
`
```

## Leitura adicional

- [Por que o Gatsby usa o GraphQL](/docs/why-gatsby-uses-graphql/)
- [A anatomia de uma consulta GraphQL](https://blog.apollographql.com/the-anatomy-of-a-graphql-query-6dffa9e9e747)

### Introdução ao GraphQL

- http://graphql.org/learn/
- https://www.howtographql.com/
- https://reactjs.org/blog/2015/05/01/graphql-introduction.html
- https://services.github.com/on-demand/graphql/

### Leituras avançadas no GraphQL

- [Especificação GraphQL](https://facebook.github.io/graphql/October2016/)
- [Interfaces e Uniões](https://medium.com/the-graphqlhub/graphql-tour-interfaces-and-unions-7dd5be35de0d)
- [Compilador de retransmissão (que o Gatsby usa para processar consultas)](https://facebook.github.io/relay/docs/en/compiler-architecture.html)
