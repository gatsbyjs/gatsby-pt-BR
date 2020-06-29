---
title: Integrando a partir do Sanity
---

## O que é Sanity.io?

[Sanity](https://www.sanity.io/) é um backend para conteúdo estruturado com um editor criado em React para edição do painel administrador. Sanity tem uma poderosa API em tempo real para escrita e leitura de dados.

Você pode usar o Sanity como um *Headless CMS* onde os autores e editores podem criar e gerenciar conteúdo através de uma interface amigável ou simplesmente como uma banco de dados para seus projetos. Nós facilitamos a reutilização do conteúdo em múltiplos websites, apps, assistentes de voz e outras plataformas.

## Começando

Comece inicializando e configurando o seu projeto Gatsby. Se você quer começar do zero, o [Guia de início rápido](/docs/quick-start) é um excelente ponto de partida. Volte para este guia quando seu projeto estiver configurado.

Você também pode conferir este [exemplo de site institucional](https://github.com/sanity-io/example-company-website-gatsby-sanity-combo) que nós criamos. Ele foi construído com um backend configurado com o Sanity Studio e o frontend com Gatsby, que você pode usar para dar início ao seu projeto em poucos minutos. Esta pode ser uma boa referência de como construir um site usando conteúdo estruturado. Siga as instruções neste [README.md](http://readme.md/) para dar início ao seu projeto.

Este guia vai te ensinar como configurar e usar o plugin [`gatsby-source-sanity`](https://www.npmjs.com/package/gatsby-source-sanity).

## Início Rápido

```shell
npm install --save gatsby-source-sanity
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-source-sanity",
      options: {
        projectId: "abc123",
        dataset: "blog",
      },
    },
  ],
}
```

A partir daqui você pode (e provavelmente deveria) [configurar uma API GraphQL](https://www.sanity.io/help/graphql-beta) para o seu projeto Sanity caso você ainda não tenha feito isso. Isto ajudará o plugin a identificar quais tipos de dados e campos existem no seu projeto, assim você pode consultar os campos mesmo que eles ainda não estejam presentes no seu projeto Gatsby.

Acesse [http://localhost:8000/___graphql](http://localhost:8000/___graphql) logo após executar `gatsby develop` no seu terminal para visualizar e entender os dados criados. Crie uma nova consulta e confira as coleções e campos disponíveis usando o auto completar (`CTRL + ESPAÇO`).

## Opções

| Opções       | Tipo    | Padrão | Descrição                                                                                                                                    |
| ------------- | ------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| projectId     | string  |         | **[obrigatório]** ID do seu projeto no Sanity                                                                                                        |
| dataset       | string  |         | **[obrigatório]** O dataset a ser utilizado                                                                                                       |
| token         | string  |         | Token de autenticação para obter dados de datasets privados, ou quando usando `overlayDrafts` [Saiba mais](https://www.sanity.io/docs/http-auth) |
| overlayDrafts | boolean | `false` | Defina como true para que os rascunhos sejam utilizados no lugar das suas versões publicadas. Por padrão, os rascunhos serão ignorados.                                      |
| watchMode     | boolean | `false` | Defina como true para que os rascunhos sejam utilizados no lugar das suas versões publicadas. Por padrão, os rascunhos serão ignorados.                                                          |

## Campos inexistentes

Obtendo erros como este?

> Cannot query field "allSanityBlogPost"
> Unknown field `preamble` on type `BlogPost`

Ao [implantar uma API GraphQL](https://www.sanity.io/help/graphql-beta) no seu projeto, o Sanity pode inspecionar entender quais tipos e campos estão disponíveis no seu esquema de dados e disponibiliza-los para evitar este problema. Uma vez que a sua API está implantada ela será aplicada de forma transparente no seu projeto. Se você já implantou sua API e ainda esta tendo problemas similares, lembre-se que caso o seu esquema de dados tenha mudado, você deve implantar sua API novamente.

Um pouco mais sobre este problema:

O Gatsby não consegue saber quais os campos e tipos de dados sem ter documentos dos tipos de dados que você quer pesquisar. Este é um [problema comum](https://github.com/gatsbyjs/gatsby/issues/3344) com o Gatsby - felizmente existem diversos esforços para solucionar este problema, o que vai nos levar a esquema de dados mais simples e com menor repetição de código.

## Usando Imagens

Campos de imagem terão a url final da imagem disponíveis através da chave `field.asset.url`, mas você também pode usar o plugin [gatsby-image](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-image) para uma melhor experiência. Gatsby-image é um componente React que permite o uso de imagens responsivas e de técnicas avançadas de carregamento de imagens. Funciona perfeitamente com este plugin sem necessitar de nenhuma configuração adicional.

Existem dois tipos de imagens suportados *fixed* e *fluid*. Para decidir entre as duas, pergunte a você mesmo: "Eu sei exatamente qual será o tamanho desta imagem no meu projeto?". Caso sim, você provavelmente deverá usar o *fixed*. Do contrário, se a altura ou largura da imagem será diferente de acordo com o tamanho da tela, então você deve optar pelo *fluid*.

### Fluid

```jsx
import React from "react"
import Img from "gatsby-image"

const Person = ({ data }) => (
  <article>
    <h2>{data.sanityPerson.name}</h2>
    <Img fluid={data.sanityPerson.profileImage.asset.fluid} />
  </article>
)

export default Person

export const query = graphql`
  query PersonQuery {
    sanityPerson {
      name
      profileImage {
        asset {
          fluid(maxWidth: 700) {
            ...GatsbySanityImageFluid
          }
        }
      }
    }
  }
`
```

### Fixed

```jsx
import React from "react"
import Img from "gatsby-image"

const Person = ({ data }) => (
  <article>
    <h2>{data.sanityPerson.name}</h2>
    <Img fixed={data.sanityPerson.profileImage.asset.fixed} />
  </article>
)

export default Person

export const query = graphql`
  query PersonQuery {
    sanityPerson {
      name
      profileImage {
        asset {
          fixed(width: 400) {
            ...GatsbySanityImageFixed
          }
        }
      }
    }
  }
`
```

### Fragmentos disponíveis

Estes são fragmentos disponíveis nas imagens, que facilitam o uso e identificação dos campos necessários para o funcionamento do gatsby-image em vários modos:

- `GatsbySanityImageFixed`
- `GatsbySanityImageFixed_noBase64`
- `GatsbySanityImageFixed_withWebp`
- `GatsbySanityImageFixed_withWebp_noBase64`
- `GatsbySanityImageFluid`
- `GatsbySanityImageFluid_noBase64`
- `GatsbySanityImageFluid_withWebp`
- `GatsbySanityImageFluid_withWebp_noBase64`

## Sobrepondo rascunhos

Eventualmente você pode querer trabalhar em um novo conteúdo que ainda não foi puplicado para ter certeza que ele funciona corretamente no seu projeto Gatsby. Configurando a opcão `overlayDrafts` para `true` os seus rascunhos irão sobrepor a versão publicada do seu documento. Para simplificar: o Gatsby irá _substituir_ a versão publicada pelo seu rascunho.

Lembre-se apenas que rascunhos não precisam necessariamente obedecer nenhuma regra de validação do Sanity, portanto é fundamental que o seu front-end garanta que todas as propriedades existam antes de tentar utiliza-las para evitar erros.

## Modo de Monitoramento

Durante o desenvolvimento, pode ser útil receber atualizações de conteúdo sem a necessidade de reiniciar o processo no terminal. Configurando o `watchMode` para `true`, este plugin irá monitorar qualquer altação de conteúdo no CMS. Quando uma alteração é detectada, o documento em questão é atualizado em tempo real e você poderá ver a alteração imediatamente.

Caso você tenha adicionado um [token no seu ambiente](#using-env-variables) e configurou a opção `overlayDrafts` para `true`, qualquer alteração por menor que seja será imediatamente aplicada.

## Criando Páginas

Diferente de outros CMS o Sanity não tem um conceito de "páginas", já que ele foi criado para ser totalmente agnóstico em como e onde você quer apresentar seu conteúdo. Porém, já que você está usando Gatsby, você certamente quer criar algumas páginas!

Como em qualquer site Gatsby, você deve criar um arquivo `gatsby-node.js` na raiz do repositório do seu site Gatsby (caso ele ainda não exista) e declarar a função `createPages`. Com isso, você usará GraphQL para consultar os dados necessários para a criação das páginas.

Por exemplo, caso você tenha um tipo de documento chamado `project` no Sanity que você gostaria de usar para criar páginas, você pode fazer algo similar a este exemplo:

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  const result = await graphql(`
    {
      allSanityProject(filter: { slug: { current: { ne: null } } }) {
        edges {
          node {
            title
            description
            tags
            launchDate(format: "DD.MM.YYYY")
            slug {
              current
            }
            image {
              asset {
                url
              }
            }
          }
        }
      }
    }
  `)

  if (result.errors) {
    throw result.errors
  }

  const projects = result.data.allSanityProject.edges || []
  projects.forEach((edge, index) => {
    const path = `/project/${edge.node.slug.current}`

    createPage({
      path,
      component: require.resolve("./src/templates/project.js"),
      context: { slug: edge.node.slug.current },
    })
  })
}
```

A consulta acima vai buscar por todos os projetos que possuem o campo `slug.current` definido, e gerar as páginas para cada um deles, disponível como `/project/ <slug-do-projeto>` usando o template definido em `src/templates/project.js` como a base para estas páginas.

A maioria dos [Gatsby starters](/starters/?v=2) possuem algum exemplo de como gerar páginas, o que você pode consultar e modificar conforme a sua necessidade.

Lembre-se de usar a interface do GraphQL para ajuda-lo a escrever a consulta que você necessita. Normalmente ela está disponível em `http://localhost:8000/___graphql` quando você executa `gatsby develop`.

## Campos "Raw”

Arrays e objetos na raiz do documento receberão um campo "raw JSON" adicional, representado através do `_raw<NomeDoCampo>`. Por exemplo, um campo chamado de `body` será mapeado para `_rawBody`. É importante lembrar que isto só acontece para items no topo da estrutura de dados (documentos).

## Texto Transportável / Bloco de Conteúdo

Textos com formatação no Sanity são normalmente representados como [Texto Transportável (Portable Text)](https://www.portabletext.org/) — anteriormente conhecido como "Bloco de Texto".

Estas estruturas de dados podem ter bastante profundidade e ser uma dor de cabeça para consultar (especificando cada um dos campos possíveis). Conforme [mencionado acima](#raw-fields), existe uma alternativa "raw" disponível para estes campos, o que é normalmente o que você deverá utilizar.

Para isso você pode instalar o pacote [block-content-to-react](https://www.npmjs.com/package/@sanity/block-content-to-react) disponível no npm e usa-lo no seu projeto Gatsby para serializar o *Portable Text*. Isso permite que você use seus próprios componentes React para sobrepor os padrões existentes e renderizar tipos de conteúdo customizado. [Saiba mais sobre *Portable Text* na documentação](https://www.sanity.io/docs/content-studio/what-you-need-to-know-about-block-text).

## Usando variávels de ambiente (.env)

Caso você não queira atribuir o ID do seu projeto no Sanity ao seu repositório, você facilmente consegue armazena-los em variáveis de ambiente com a extensão *.env*. Confira o exemplo:

```text:title=.env
SANITY_PROJECT_ID = abc123
SANITY_DATASET = production
SANITY_TOKEN = my-super-secret-token
```

```js:title=gatsby-config.js
require('dotenv').config({
  path: `.env.${process.env.NODE_ENV}`
})

module.exports = {
  plugins: [
    {
      resolve: 'gatsby-source-sanity',
      options: {
        projectId: process.env.SANITY_PROJECT_ID,
        dataset: process.env.SANITY_DATASET
        token: process.env.SANITY_TOKEN
      }
    }
  ]
}
```

Este exemplo é baseado na implementação encontrada na [nesta documentação](/docs/environment-variables/).
