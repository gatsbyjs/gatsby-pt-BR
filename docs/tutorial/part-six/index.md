---
title: Transformer plugins
typora-copy-images-to: ./
disableTableOfContents: true
---

> Este tutorial é uma parte da série sobre a camada de dados do Gatsby. Tenha certeza que você completou a [parte 4](/tutorial/part-four/) e [parte 5](/tutorial/part-five/) antes de continuar aqui.

## O que está neste tutorial?

O tutorial anterior mostrou como os plugins de origem trazem dados para _dentro_ do Gatsby. Neste tutorial, você irá aprender como os plugins de _transform_ transformam o conteúdo obtido pelos plugins de origem. A combinação de _plugins_ de origem e _plugins_ transformadores pode lidar com toda a fonte de dados e transformação de dados que você pode precisar ao criar um site com Gatsby.

## Plugins transformadores

Geralmente, o formato dos dados que você obtém a partir dos plugins de origem não é o que você deseja usar para a criação do seu site. O plugin de sistema de arquivos permite você consultar os dados sobre arquivos, mas e se você quiser consultar dados dentro de arquivos?

Para fazer isso possível, Gatsby suporta plugins de transformação que usam conteúdo de um plugin de origem e transformá-lo em algo mais utilizável.

Por exemplo, arquivos _markdown_. _Markdown_ é legal escrever, mas quando você constrói uma página, você precisa que o _markdown_ seja HTML.

Adicione um arquivo _markdown_ no seu site em `src/pages/sweet-pandas-eating-sweets.md` (Esta será sua primeira publicação em _markdown_ no blog) e aprenda como transformar isso em HTML usando um plugin transformador e GraphQL.

```markdown:title=src/pages/sweet-pandas-eating-sweets.md
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Os pandas são realmente doces.

Aqui está um vídeo de um panda comendo doces.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

Uma vez que você salvou o arquivo, olhe em `/my-files/` novamente - o novo arquivo de _markdown_ está na tabela. Isso é uma funcionalidade muito poderosa do Gatsby. Como o exemplo anterior do `siteMetadata`, os plugins de origem podem recarregar os dados em tempo real. O `gatsby-source-filesystem` está sempre procurando por novos arquivos a serem adicionados e quando estiverem, executa novamente suas consultas.

Adicione um plugin transformador que pode transformar os arquivos _markdown_:

```shell
yarn add gatsby-transformer-remark
```

Em seguida, adicione no `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas comem muito`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`, // highlight-line
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Reinicie o servidor de desenvolvimento, em seguida atualize (ou abra novamente) o GraphiQL e observe o autocomplete:

![markdown-autocomplete](markdown-autocomplete.png)

Selecione `allMarkdownRemark` novamente e execute-o assim como você fez para `allFile`. Você verá o arquivo de _markdown_ adicionado recentemente. Explore os campos que estão disponíveis no nó `MarkdownRemark`.

![markdown-query](markdown-query.png)

Ok! Felizmente, alguns princípios estão começando a se encaixar. Plugins de origem trazem dados para o sistema de manipulação de dados do Gatsby e os plugins transformadores (`transformer`) transformam o conteúdo bruto trazido pelos plugins de origem. Esse padrão pode lidar com todas as fontes e transformações de dados que você pode precisar ao construir um site com Gatsby.

## Crie uma lista de dos arquivos _markdown_ do seu site `src/pages/index.js`

Agora você irá criar uma lista de arquivos _markdown_ na primeira página. Como muitos blogs, você deseja terminar com uma lista de links na primeira página apontando para cada publicação do blog. Com o GraphQL, você pode consultar (`query`) a lista atual de publicações de blog de remarcação para não precisar manter a lista manualmente.

Como na página `src/pages/my-files.js`, substitua `src/pages/index.js` pelo seguinte para adicionar uma consulta GraphQL com algum estilo e HTML inicial.

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import { css } from "@emotion/core"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
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
          </div>
        ))}
      </div>
    </Layout>
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
          excerpt
        }
      }
    }
  }
`
```

Agora a página deve se parecer com:

![frontpage](frontpage.png)

Mas sua unica publicação parece estar um pouco solitária. Então, vamos adicionar outra em 
`src/pages/pandas-and-bananas.md`

```markdown:title=src/pages/pandas-and-bananas.md
---
title: "Pandas and Bananas"
date: "2017-08-21"
---

Os Pandas comem bananas? Veja este pequeno vídeo que mostra que sim! Pandas parecem realmente gostar de bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

![two-posts](two-posts.png)

Parece ótimo! Exceto... a ordem das publicações está errada.

Mas isso é fácil de resolver. Ao consultar uma conexão de algum tipo, você pode passar uma variedade de parâmetros para a consulta GraphQL. Você pode ordenar (`sort`) e filtrar (`filter`) nós, defina quantos nós devem ser ignorados (`skip`), e escolha o limite (`limit`) de quandos nós recuperar. Com esse poderosos conjunto de operadores, você pode selecionar qualquer data que você quiser no formato que você precisa.

Na consulta GraphQL da página de índice, muda `allMarkdownRemark` para `allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC })`. _Nota: Há 3 sublinhados entre `frontmatter` and `date`._ Salve isso e a ordem de classificação deve ser corrigida.

Tente abrir o GraphiQL e jogar com diferentes opções de classificação. Você pode classificar a conexão `allFile` junto com outras conexões.

Para obter mais informação sobre nossos operadores de consulta, explore nosso [Guia de referência de GraphQL.](/docs/graphql-reference/)

## Desafio

Tente criar uma nova página contendo um publicações do blog e veja o que acontece com a lista de publicações do blog na página inicial!

## O que está por vir?

Isso é ótimo! Você acabou de criar uma página onde está consultando seus arquivos de _markdown_ e produzindo uma lista de títulos e trechos de publicações do blog. Mas você não quer ver textos apenas, você quer página reais para seus arquivos _markdown_.

Você pode continuart criando páginas colocando os componentes React em `src/pages`. No entando, você aprenderá a criar _programaticamente_ páginas a partir de dados. Gatsby _não_ se limita a criar páginas a partir de arquivos como muitos geradores de sites estáticos. Gatsby permite que você utilize GraphQL para consultar seus dados e mapear os resultados da consulta para as páginas - tudo no momento da criação (`build`). Esta é uma ideia realmente poderosa. Você explorará suas implicações e caminhos de usá-lo no próximo tutorial, onde você irá aprender a [criar páginas programaticamente a partir de dados](/tutorial/part-seven/). 
