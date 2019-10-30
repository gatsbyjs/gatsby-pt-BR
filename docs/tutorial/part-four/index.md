---
title: Dados no Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Seja bem-vindo(a) a quarta parte do tutorial! Já estamos no meio do caminho! Esperamos que as coisas estejam começando a ficar familiares 😀

## Relembrando a primeira metade do tutorial

Até agora você aprendeu como utilizar React.js-o quão poderoso é ser capaz de 
criar seus _próprios_ componentes para agirem como componentes essenciais customizados para websites.

Você também explorou os componentes de estilo utilizando os módulos CSS.

## O que tem nesse tutorial?

Nas próximas quatro partes do tutorial (incluindo essa), vocês estará mergulhando na camada de dados do Gatsby, uma funcionalidade poderosa que permite você criar sites facilmente a partir de Markdown, WordPress, CMSs puros, e qualquer outra fonte de dados.

**NOTA:** A camada de dados do Gatsby utiliza GraphQL. Para um tutorial aprofundado em
Graphql, nós recomendamos [How to GraphQL](https://www.howtographql.com/).

## Dados no Gatsby

Um website tem quatro partes: HTML, CSS, JS e dados. A primeira metade do
tutorial focou nos três primeiros. Agora vamos aprender como usar dados nos sites Gatsby.

**O que são dados?**

A resposta de um cientista da computação seria: dados são coisas como `"strings"`,
inteiros (`42`), objetos (`{ pizza: true}`), etc.

Entretando, quando estamos trabalhando com Gatsby, uma resposta mais prática é
"tudo que vive fora de um componente React".

Até agora, você estava escrevendo texto e adicionando imagens _diretamente_ nos componentes.
Essa é uma forma _excelente_ de construir muitos websites. Mas, muitas vezes você quer armazenar
dados _fora_ dos componentes e, em seguida, trazer os dados _para_ o componente quando
necessário.

Se você está construindo um site com WordPress (outros contribuidores
têm uma interface legal para adicionar e manter o conteúdo) e Gatsby, os _dados_
do site (páginas e posts) são em WordPress e você _extrai_ esses dados, quando 
necessário, para os componentes.

Dados também podem estar em arquivos tipo Markdown, CSV, etc. bem como bancos
de dados e APIs de todos os tipos.

**A camada de dados do Gatsby permite você extrair dados dessas fontes (e quaisquer outras)
diretamente para os seus componentes**-na estrutura e forma que você quiser.

## Usandos Dados Desestruturados vs GraphQL

### Eu preciso utilizar GraphQL e plugins de extração para injetar dados nos sites Gatsby?

Claro que não! Você pode usar a API node `createPages` para injetar diretamente dados desestruturados nas páginas Gatsby, ao invés de utilizar a camada de dados GraphQL. Essa é uma ótima escolha para pequenos sites, embora GraphQL e plugins de extração podem ajudar poupar tempo com sites mais complexos.

Veja o guia [Usando Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/) para aprender como puxar dados para o seu site Gatsby utilizando a API node `createPages` e ver um site de exemplo!

### When do I use unstructured data vs GraphQL?

If you're building a small site, one efficient way to build it is to pull in unstructured data as outlined in this guide, using `createPages` API, and then if the site becomes more complex later on, you move on to building more complex sites, or you'd like to transform your data, follow these steps:

1.  Check out the [Plugin Library](/plugins/) to see if the source plugins and/or transformer plugins you'd like to use already exist
2.  If they don't exist, read the [Plugin Authoring](/docs/creating-plugins/) guide and consider building your own!

### How Gatsby's data layer uses GraphQL to pull data into components

There are many options for loading data into React components. One of the most
popular and powerful of these is a technology called
[GraphQL](http://graphql.org/).

GraphQL was invented at Facebook to help product engineers _pull_ needed data into
components.

GraphQL is a **q**uery **l**anguage (the _QL_ part of its name). If you're
familiar with SQL, it works in a very similar way. Using a special syntax, you describe
the data you want in your component and then that data is given
to you.

Gatsby uses GraphQL to enable components to declare the data they need.

## Create a new example site

Create another new site for this part of the tutorial. You're going to build a Markdown blog called "Pandas Eating Lots". It's dedicated to showing off the best pictures and videos of pandas eating lots of food. Along the way, you'll be dipping your toes into GraphQL and Gatsby's Markdown support.

Open a new terminal window and run the following commands to create a new Gatsby site in a directory called `tutorial-part-four`. Then navigate to the new directory:

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

Then install some other needed dependencies at the root of the project. You'll use the Typography theme
"Kirkham", and you'll try out a CSS-in-JS library, ["Emotion"](https://emotion.sh/):

```shell
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```

Set up a site similar to what you ended with in [Part Three](/tutorial/part-three). This site will have a layout component and two page components:

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

`gatsby-config.js` (must be in the root of your project, not under src)

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

Add the above files and then run `gatsby develop`, per usual, and you should see the following:

![start](start.png)

You have another small site with a layout and two pages.

Now you can start querying 😋

## Your first GraphQL query

When building sites, you'll probably want to reuse common bits of data -- like the _site title_ for example. Look at the `/about/` page. You'll notice that you have the site title (`Pandas Eating Lots`) in both the layout component (the site header) as well as in the `<h1 />` of the `about.js` page (the page header).

But what if you want to change the site title in the future? You'd have to search for the title across all your components and edit each instance. This is both cumbersome and error-prone, especially for larger, more complex sites. Instead, you can store the title in one location and reference that location from other files; change the title in a single place, and Gatsby will _pull_ your updated title into files that reference it.

The place for these common bits of data is the `siteMetadata` object in the `gatsby-config.js` file. Add your site title to the `gatsby-config.js` file:

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

Restart the development server.

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
