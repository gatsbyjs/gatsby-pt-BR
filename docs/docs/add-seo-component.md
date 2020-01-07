---
title: "Adicionando um Componente SEO"
---

Todo site na web tem _meta-tags_ básicas, como o título, favicon ou descrição da página no elemento `<head>`. Essas informações são exibidas no navegador e são usadas quando alguém compartilha o seu site, por exemplo, no Twitter. Você pode fornecer dados adicionais aos usuários e aos sites para eles incorporarem — e é aí que entra esse guia para um componente de SEO. No final, você terá um componente que pode ser inserido no arquivo de layout e terá visualizações avançadas para outros clientes, usuários de smartphone e mecanismos de pesquisa.

_Nota: Esse componente usará StaticQuery. Se você não estiver familiarizado, consulte a [documentação do StaticQuery](/docs/static-query/). Você também precisa ter o `react-helmet` instalado, o qual você pode dar uma olhada [nesse guia](/docs/add-page-metadata)._

## gatsby-config.js

O Gatsby faz todos os dados colocados no `siteMetadata` do arquivo `gatsby-config` disponíveis automaticamente no GraphQL e, portanto, é uma boa ideia colocar suas informações para o componente nessa seção.

```js:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Severus Snape",
    titleTemplate: "%s · The Real Hero",
    description:
      "Hogwarts Potions master, Head of Slytherin house and former Death Eater.",
    url: "https://www.doe.com", // Não coloque uma barra no final
    image: "/images/snape.jpg", // Caminho para sua imagem que está na pasta 'static'
    twitterUsername: "@occlumency",
  },
}
```

## Componente de SEO

Crie um novo componente e coloque o seguinte código nele:

```jsx:title=src/components/SEO.js
import React from "react"
import { Helmet } from "react-helmet"
import PropTypes from "prop-types"
import { StaticQuery, graphql } from "gatsby"

const SEO = ({ title, description, image, pathname, article }) => ()

export default SEO

SEO.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string,
  image: PropTypes.string,
  pathname: PropTypes.string,
  article: PropTypes.bool,
}

SEO.defaultProps = {
  title: null,
  description: null,
  image: null,
  pathname: null,
  article: false,
}
```

**Nota:** `propTypes` são incluídas nesse exemplo para ajudar você a garantir que toda informação que você precisa está no componente, e para ajudar a servir como um guia enquanto faz a desestruturação/uso dessas propriedades.

Como o componente de SEO também deve ser usado em outros arquivos, por exemplo, um arquivo de template, o componente também aceita propriedades para as quais você define padrões sensíveis na seção `SEO.defaultProps`. Desse modo a informação que você colocar no `siteMetadata` é utilizada, a menos que você defina a propriedade explicitamente.

Agora defina a consulta (query) e coloque-a na StaticQuery (você também pode salvar a consulta em uma constante). Além disso, você poderia renomear os itens da consulta, para que, por exemplo, `title` utilize o alias de `defaultTitle`.

```jsx:title=src/components/SEO.js
const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={}
  />
)

export default SEO

const query = graphql`
  query SEO {
    site {
      siteMetadata {
        defaultTitle: title
        titleTemplate
        defaultDescription: description
        siteUrl: url
        defaultImage: image
        twitterUsername
      }
    }
  }
`;
```

A próxima etapa é desestruturar os dados da consulta e criar um objeto que verifique se os objetos foram usados - se não forem utilizados os valores padrão. Renomear os itens da consulta é útil aqui: evita colisões de dados.

```jsx:title=src/components/SEO.js
const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={({
      site: {
        siteMetadata: {
          defaultTitle,
          titleTemplate,
          defaultDescription,
          siteUrl,
          defaultImage,
          twitterUsername,
        }
      }
    }) => {
      const seo = {
        title: title || defaultTitle,
        description: description || defaultDescription,
        image: `${siteUrl}${image || defaultImage}`,
        url: `${siteUrl}${pathname || '/'}`,
      }

      return ()
    }}
  />
)

export default SEO
```

A última etapa é retornar a informação com ajuda do `Helmet`. Seu componente de SEO deve parecer com isso:

```jsx:title=src/components/SEO.js
import React from "react"
import { Helmet } from "react-helmet"
import PropTypes from "prop-types"
import { StaticQuery, graphql } from "gatsby"

const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={({
      site: {
        siteMetadata: {
          defaultTitle,
          titleTemplate,
          defaultDescription,
          siteUrl,
          defaultImage,
          twitterUsername,
        },
      },
    }) => {
      const seo = {
        title: title || defaultTitle,
        description: description || defaultDescription,
        image: `${siteUrl}${image || defaultImage}`,
        url: `${siteUrl}${pathname || "/"}`,
      }

      return (
        <>
          <Helmet title={seo.title} titleTemplate={titleTemplate}>
            <meta name="description" content={seo.description} />
            <meta name="image" content={seo.image} />
            {seo.url && <meta property="og:url" content={seo.url} />}
            {(article ? true : null) && (
              <meta property="og:type" content="article" />
            )}
            {seo.title && <meta property="og:title" content={seo.title} />}
            {seo.description && (
              <meta property="og:description" content={seo.description} />
            )}
            {seo.image && <meta property="og:image" content={seo.image} />}
            <meta name="twitter:card" content="summary_large_image" />
            {twitterUsername && (
              <meta name="twitter:creator" content={twitterUsername} />
            )}
            {seo.title && <meta name="twitter:title" content={seo.title} />}
            {seo.description && (
              <meta name="twitter:description" content={seo.description} />
            )}
            {seo.image && <meta name="twitter:image" content={seo.image} />}
          </Helmet>
        </>
      )
    }}
  />
)

export default SEO

SEO.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string,
  image: PropTypes.string,
  pathname: PropTypes.string,
  article: PropTypes.bool,
}

SEO.defaultProps = {
  title: null,
  description: null,
  image: null,
  pathname: null,
  article: false,
}

const query = graphql`
  query SEO {
    site {
      siteMetadata {
        defaultTitle: title
        titleTemplate
        defaultDescription: description
        siteUrl: url
        defaultImage: image
        twitterUsername
      }
    }
  }
`
```

## Exemplos

Você também pode colocar as _meta-tags_ do Facebook e Twitter em seus próprios componentes, adicionar favicons personalizados que você colocou na pasta `static` e adicionar dados do [schema.org](https://schema.org/) (o Google usará isso para os seus [dados estruturados](https://developers.google.com/search/docs/guides/intro-structured-data). Para ver como isso funciona, você pode dar uma olhada nesses dois exemplos:

- [marisamorby.com](https://github.com/marisamorby/marisamorby.com/blob/master/packages/gatsby-theme-blog-sanity/src/components/seo.js)
- [gatsby-starter-prismic](https://github.com/LeKoArts/gatsby-starter-prismic/blob/master/src/components/SEO/SEO.jsx)

Conforme mencionado no começo, você também pode usar o componente em modelos, como [neste exemplo](https://github.com/jlengstorf/marisamorby.com/blob/6e86f845185f9650ff95316d3475bb8ac86b15bf/src/templates/post.js#L12-L18).
