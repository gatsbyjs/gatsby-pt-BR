---
title: Dados no Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Boas vindas a quarta parte do tutorial! Já estamos no meio do caminho! Esperamos que as coisas estejam começando a ficar familiares 😀

## Relembrando a primeira metade do tutorial

Até agora você aprendeu como utilizar React.js-o quão poderoso é ser capaz de 
criar seus _próprios_ componentes para agirem como componentes essenciais customizados para websites.

Você também explorou os componentes de estilo utilizando os módulos CSS.

## O que teremos nesse tutorial?

Nas próximas quatro partes do tutorial (incluindo esta), vocês estará mergulhando na camada de dados do Gatsby, uma funcionalidade poderosa que permite você criar sites facilmente a partir de Markdown, WordPress, CMSs puros, e qualquer outra fonte de dados.

**NOTA:** A camada de dados do Gatsby utiliza GraphQL. Para um tutorial aprofundado em
Graphql, nós recomendamos [How to GraphQL](https://www.howtographql.com/).

## Dados no Gatsby

Um website tem quatro partes: HTML, CSS, JS e dados. A primeira metade do
tutorial focou nos três primeiros. Agora vamos aprender como usar dados nos sites Gatsby.

**O que são dados?**

A resposta de um cientista da computação seria: dados são coisas como `"strings"`,
inteiros (`42`), objetos (`{ pizza: true }`), etc.

Entretanto, quando estamos trabalhando com Gatsby, uma resposta mais prática é
"tudo que vive fora de um componente React".

Até agora, você estava escrevendo texto e adicionando imagens _diretamente_ nos componentes.
Essa é uma forma _excelente_ de construir muitos websites. Mas, muitas vezes você quer armazenar
dados _fora_ dos componentes e, em seguida, trazer os dados _para_ dentro do componente quando
necessário.

Se você está construindo um site com WordPress (outros contribuidores
têm uma interface legal para adicionar e manter o conteúdo) e Gatsby, os _dados_
do site (páginas e posts) são em WordPress e você _extrai_ esses dados, quando 
necessário, para os componentes.

Dados também podem estar em arquivos Markdown, CSV, etc. bem como bancos
de dados e APIs de todos os tipos.

**A camada de dados do Gatsby permite você extrair dados dessas fontes (e quaisquer outras)
diretamente para os seus componentes**-na estrutura e forma que você quiser.

## Usandos Dados Desestruturados vs GraphQL

### Eu preciso utilizar GraphQL e plugins de extração para injetar dados nos sites Gatsby?

Claro que não! Você pode usar a API node `createPages` para injetar diretamente dados desestruturados nas páginas Gatsby, ao invés de utilizar a camada de dados GraphQL. Essa é uma ótima escolha para pequenos sites, embora GraphQL e plugins de extração podem ajudar a poupar tempo com sites mais complexos.

Veja o guia [Usando Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/) para aprender como injetar dados no seu site Gatsby utilizando a API node `createPages` e ver um site de exemplo!

### Quando eu uso dados desestruturados vs GraphQL?

Se você está construindo um pequeno site, uma forma eficiente de construi-lo é usar dados desestruturados conforme apresentado nesse guia, usando a API `createPages`, e caso o site se tornar mais complexo no futuro, você parte para a construção de sites mais complexos, ou caso você gostaria de transformar seus dados, siga esses passos:

1.  Confira a [Biblioteca de Plugins](/plugins/) para ver se os plugins de extração e/ou plugins de transformação que você gostaria de utilizar já existem.
2.  Se eles não existirem, leia o guia de [Autoria de Plugins](/docs/creating-plugins/) e considere construir você mesmo! 

### Como a camada de dados do Gatsby usa GraphQL para injetar dados nos componentes

Há muitas opções para injetar dados nos componentes React. Uma das mais 
populares e poderosas é a tecnologia chamada 
[GraphQL](http://graphql.org/).

GraphQL foi criado pelo Facebook para ajudar engenheiros de produto _injetar_ os dados necessários nos
componentes.

GraphQL é uma **q**uery **l**anguage (a parte _QL_ do seu nome), ou linguagem de consulta. Se você está
familiarizado com SQL, ela funciona de uma forma muito similar. Usando uma sintaxe especial, você descreve
quais dados você quer no seu componente e assim esses dados são entregues
a você.

Gatsby usa GraphQL para permitir que componentes declarem quais dados eles precisam.

## Crie um novo site de exemplo

Crie um novo site para essa parte do tutorial. Você vai construir um blog com Markdown chamado "Pandas Eating Lots". Ele é
dedicado a mostrar as melhores fotos e vídeos de pandas comendo um monte de comida. Ao longo do caminho, você vai dar uma olhada no GraphQL e no suporte do Gatsby para Markdown.

Abra uma nova janela de terminal e rode os seguintes comandos para criar um novo site Gatsby em um diretório chamado `tutorial-part-four`. Navegue para o novo diretório:

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

Instale algumas outras dependências necessárias na raiz do projeto. Você irá usar o tema de Tipografia
"Kirkham", e você vai experimentar uma biblioteca CSS-in-JS, ["Emotion"](https://emotion.sh/):

```shell
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```

Configure um site similar ao que você finalizou na [Parte Três](/tutorial/part-three). Esse site vai ter um componente de layout e dois componentes de página:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
  <div
    css={css`
      margin: 0 auto;
      max-width: 700px;
      padding: ${rhythm(2)};
      padding-top: ${rhythm(1.5)};
    `}
  >
    <Link to={`/`}>
      <h3
        css={css`
          margin-bottom: ${rhythm(2)};
          display: inline-block;
          font-style: normal;
        `}
      >
        Pandas Eating Lots
      </h3>
    </Link>
    <Link
      to={`/about/`}
      css={css`
        float: right;
      `}
    >
      About
    </Link>
    {children}
  </div>
)
```

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
      <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
      />
    </div>
  </Layout>
)
```

```jsx:title=src/pages/about.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>About Pandas Eating Lots</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)
```

```javascript:title=src/utils/typography.js
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

`gatsby-config.js` (precisa estar na raiz do seu projeto, não em src)

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
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

Adicione os arquivos acima e rode `gatsby develop`, como sempre, e você deve ver o seguinte:

![start](start.png)

Você tem outro pequeno site com um layout e duas páginas.

Agora você pode começar a consultar 😋

## A sua primeira consulta com GraphQL

Na construção de sites você provavelmente vai querer reutilizar partes comuns de dados -- como o _título do site_, por exemplo. Dê uma olhada na página `/about`. Você vai notar que o título do site (`Pandas Eating Lots`) tanto no componente de layout (o cabeçalho do site) quanto no `<h1 />` da página `about.js` (o cabeçalho da página).

Mas e se você quiser mudar o título do site no futuro? Você teria que procurar pelo título ao longo de todos os componentes e editar cada instância. Isso é trabalhoso e susceptível a erros, especialmente para sites maiores e mais complexos. Ao invés disso, você pode armazenar o título em um lugar e referenciar esse lugar de outros arquivos; altere o título em um único lugar e o Gatsby vai _injetar_ seu título atualizado nos arquivos que o referenciam.

O lugar para esses fragmentos comuns de dados é o objeto `siteMetadata` no arquivo `gatsby-config.js`. Adicione o título do seu site no arquivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  // highlight-start
  siteMetadata: {
    title: `Title from siteMetadata`,
  },
  // highlight-end
  plugins: [
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

Reinicie o servidor de desenvolvimento.

### Use a page query

Now the site title is available to be queried; Add it to the `about.js` file using a [page query](/docs/page-query):

```jsx:title=src/pages/about.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-next-line
export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1> {/* highlight-line */}
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)

// highlight-start
export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end
```

It worked! 🎉

![Page title pulling from siteMetadata](site-metadata-title.png)

The basic GraphQL query that retrieves the `title` in your `about.js` changes above is:

```graphql:title=src/pages/about.js
{
  site {
    siteMetadata {
      title
    }
  }
}
```

> 💡 In [part five](/tutorial/part-five/#introducing-graphiql), you'll meet a tool that lets us interactively explore the data available through GraphQL, and help formulate queries like the one above.

Page queries live outside of the component definition -- by convention at the end of a page component file -- and are only available on page components.

### Use a StaticQuery

[StaticQuery](/docs/static-query/) is a new API introduced in Gatsby v2 that allows non-page components (like your `layout.js` component), to retrieve data via GraphQL queries.
Let's use its newly introduced hook version — [`useStaticQuery`](/docs/use-static-query/).

Go ahead and make some changes to your `src/components/layout.js` file to use the `useStaticQuery` hook and a `{data.site.siteMetadata.title}` reference that uses this data. When you are done, your file will look like this:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
// highlight-next-line
import { useStaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"
// highlight-start
export default ({ children }) => {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  return (
    // highlight-end
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          {data.site.siteMetadata.title} {/* highlight-line */}
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
    // highlight-start
  )
}
// highlight-end
```

Another success! 🎉

![Page title and layout title both pulling from siteMetadata](site-metadata-two-titles.png)

Why use two different queries here? These examples were quick introductions to
the query types, how they are formatted, and where they can be used. For now,
keep in mind that only pages can make page queries. Non-page components, such as
Layout, can use StaticQuery. [Part 7](/tutorial/part-seven/) of the tutorial explains these in greater
depth.

But let's restore the real title.

One of the core principles of Gatsby is that _creators need an immediate connection to what they're creating_ ([hat tip to Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/)). In other words, when you make any change to code you should immediately see the effect of that change. You manipulate an input of Gatsby and you see the new output showing up on the screen.

So almost everywhere, changes you make will immediately take effect. Edit the `gatsby-config.js` file again, this time changing the `title` back to "Pandas Eating Lots". The change should show up very quickly in your site pages.

![Both titles say Pandas Eating Lots](pandas-eating-lots-titles.png)

## What's coming next?

Next, you'll be learning about how to pull data into your Gatsby site using
GraphQL with source plugins in [part five](/tutorial/part-five/) of the
tutorial.
