---
title: Trabalhando com imagens dentro de Postagens e Páginas Markdown
---

Quando estiver construindo sites com o Gatsby que são compostos primariamente de páginas ou posts com Markdown, a inserção de imagens pode melhorar o conteúdo. Você pode adicionar imagens de diversas formas. 

## Imagens em destaque como metadados Frontmatter

Em sites como blogs, talvez você queira inserir uma imagem em destaque para que ela apareça no topo da página, por exemplo. Uma forma de fazer isso é utilizar o nome do arquivo da imagem em um campo frontmatter e então transformá-lo por meio do `gatsby-plugin-sharp` em uma query GraphQL.

Essa solução presume que você já possua páginas de Markdown sendo geradas automaticamente por meio de renderizadores como `gatsby-transformer-remark` ou `gatsby-plugin-mdx`. Senão, leia a [parte 7 do tutorial de Gatsby](/tutorial/part-seven/). Isso será desenvolvido durante o tutorial, nesse exemplo será utilizado o `gatsby-transformer-remark`.

> Nota: Isso pode ser feito de forma similar utilizando [MDX](/docs/mdx/). Ao invés de usar nodes `markdownRemark` no GraphQL, o `Mdx` pode ser trocado e deverá funcionar também.

Para iniciar, faça o download dos plugins do Gatsby-image, como mencionado em [Usando gatsby-image](/docs/using-gatsby-image/).

```shell
npm install --save gatsby-image gatsby-transformer-sharp gatsby-plugin-sharp
```

Talvez você também queira ter instalado o  `gatsby-source-filesystem`. Então, faça a configuração dos vários plugins no arquivo `gatsby-config`.

### Configurando para imagens e posts no mesmo diretório

Se as imagens e arquivos Markdown estiverem no mesmo diretório, a utilização das imagens pode ser feita com apenas uma configuração. Por exemplo, se seus arquivos Markdown e imagens estão em um mesmo diretório `/pages`, ambos os conteúdos serão automaticamente selecionados pelo GraphQL como parte da camada de dados do Gatsby.
 
```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    `gatsby-transformer-sharp`,
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`, // Linha mais importante
      },
    },
  ],
}
```

Então, em um exemplo de um arquivo Markdown, adicione um campo chamado `featuredImage`:

```markdown:title=src/pages/Meus-Dogs-Favoritos.md
---
title: Meus Dogs Favoritos
featuredImage: cachorro-fofinho.png
---

O conteúdo será inserido aqui!
```

O próximo passo é incorporar os dados em um modelo usando uma query GraphQL, que será vista futuramente nesse guia.

### Configurando para imagens e posts em diretórios diferentes

Em algumas ocasiões você as imagens e seus posts ou páginas Markdown vão estar em diretórios diferentes, como em um diretório externo `/images`. Você pode definir isso ao especificar duas origens distintas, uma para as páginas e outra para as imagens:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    `gatsby-transformer-sharp`,
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`, // Linha mais importante
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/images`, // Linha mais importante
      },
    },
  ],
}
```

Então, no arquivo Markdown, o caminho para o campo `featuredImage` será relativo ao arquivo da página (nesse caso, na pasta `/images` que está um nível acima).

```markdown:title=src/pages/about.md
---
title: About
featuredImage: ../images/equipe-gatos.png
---

O conteudo será inserindo aqui!
```

### Consultando imagens para Frontmatter

Agora que você já definiu a origem do Markdown e os dados da imagem, você poderá consultar por imagens em destaque no GraphQL. Se o caminho apontado for uma imagem, ele será transformado em um node `File` no GraphQL e então você poderá obter os dados da imagem utilizando o campo `childImageSharp`.

Isso pode ser adicionado a uma query GraphQL em um arquivo modelo de Markdown. Neste exemplo, a [Query flúida](/docs/gatsby-image#images-that-stretch-across-a-fluid-container) é usada para deixar a imagem responsiva.

```jsx:title=src/templates/blog-post.js
export const query = graphql`
  query PostQuery($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
        // highlight-start
        featuredImage {
          childImageSharp {
            fluid(maxWidth: 800) {
              ...GatsbyImageSharpFluid
            }
          }
        }
        // highlight-end
      }
    }
  }
`
```

Também, no post modelo de Markdown, importe o pacote `gatsby-image` e passe os resultados da query GraphQL em um componente `<Img />`.

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
// highlight-start
import Img from "gatsby-image"
// highlight-end

export default ({ data }) => {
  let post = data.markdownRemark

  // highlight-start
  let featuredImgFluid = post.frontmatter.featuredImage.childImageSharp.fluid
  // highlight-end

  return (
    <Layout>
      <div>
        <h1>{post.frontmatter.title}</h1>
        // highlight-start
        <Img fluid={featuredImgFluid} />
        // highlight-end
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query PostQuery($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
        featuredImage {
          childImageSharp {
            fluid(maxWidth: 800) {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`
```

Sua imagem em destaque deverá aparecer diretamente no topo da postagen gerada. Tada!

## Imagens Inline com `gatsby-remark-images`

Você também pode incluir imagens diretamente no corpo do Markdown. O plugin [gatsby-remark-images](/packages/gatsby-remark-images) será útil nesse caso.

Inicie instalando `gatsby-remark-images` e `gatsby-plugin-sharp`.

```shell
npm install --save gatsby-remark-images gatsby-plugin-sharp
```

Tenha certeza que o `gatsby-source-filesystem` está instalado e que ele esteja apontando para o diretório onde suas imagens estarão localizadas.

Configure os plugins em seu arquivo `gatsby-config`. Como no exemplo anterior, ambos `Remark` ou `MDX` podem ser usados.

### Usando o Plugin MDX

O plugin `gatsby-plugin-mdx` será utilizado no exemplo abaixo. Insira o plugin `gatsby-remark-images` dentro do campo `gatsbyRemarkPlugins` que faz parte das opções do`gatsby-plugin-mdx`.

> Nota: Esse exemplo de configuração assume que suas imagens e Markdowns estão originando do mesmo diretório. Confira a seção no [configurando para diretórios diferentes](#Configurando-para-imagens-e-posts-em-diretórios-diferentes) para ajuda adicional.


```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        gatsbyRemarkPlugins: [
          {
            resolve: `gatsby-remark-images`,
            options: {
              maxWidth: 1200,
            },
          },
        ],
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`,
      },
    },
  ],
}
```

### Utilizando o Plugin Transformer Remark

Abaixo está um exemplo similar utilizando o plugin `gatsby-transformer-remark` ao invés do `gatsby-plugin-mdx`. Insira o plugin `gatsby-remark-images` dentro do campo `plugins` que faz parte das opções do `gatsby-transformer-remark`.

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    {
      resolve: `gatsby-transformer-remark`,
      options: {
        plugins: [
          {
            resolve: `gatsby-remark-images`,
            options: {
              maxWidth: 800,
            },
          },
        ],
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/posts`,
      },
    },
  ],
}
```

Com as configurações acima, você poderá utilizar a sintaxe padrão para imagens no Markdown. Elas serão processadas pelo `Sharp` e irão aparecem como se você tivesse às inserido em um componente `gatsby-image`.

```markdown
![George o Gato](./george-cat.png)
```
