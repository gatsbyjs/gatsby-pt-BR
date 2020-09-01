---
title: Consultando dados do GraphCMS
---

## O jeito Headless do GraphCMS

[GraphCMS](https://graphcms.com?ref="gatsby-headless-docs-top") é um _headless CMS_, otimizado para ser utilizado com o GraphQL. Estruturas como posts, autores, produtos, entre outras, são divididas em tipos de conteúdos, chamados "_models_". Esses _models_, são consultados com a sintaxe já conhecida do GraphQL.

Um dos benefícios do GraphCMS quando utilizado com Gatsby, é que ele suporta o GraphQL nativamente, o que permite que as consultas sejam testadas antes mesmo de iniciar seu projeto Gatsby.

## Introdução

Neste guia você vai criar um projeto completo, capaz de consultar dados do GraphCMS.

### Instalando o boilerplate

Para começar, vamos criar um site Gatsby utilizando o template `gatsby-starter-default`.

```shell
gatsby new gatsby-site https://github.com/gatsbyjs/gatsby-starter-default
```

Acesse o diretório do projeto com `cd gatsby-site`.

### Adicione o plugin do GraphQL

Além disso, você precisa adicionar a biblioteca `gatsby-source-graphql` no projeto. Já que o GraphCMS utiliza GraphQL nativamente, você aproveitará a capacidade do Gatsby de simplesmente unificar duas APIs do GraphQL, reduzindo o tempo necessário para transformar o conteúdo. Não é necessário usar um plugin especial `gatsby-source-X-cms`, o plugin do GraphQL é tudo o que você precisa.

Você pode instalar esse plugin com o comando:

```shell
  # Opcional: `yarn add`
  npm install --save gatsby-source-graphql
```

### Configure o plugin

A última etapa antes de poder consultar os dados, é configurar o plugin `gatsby-source-graphql`. Abra o arquivo `gatsby-config.js` e adicione o objeto abaixo no array `plugins`. Esse exemplo usa uma API aberta do GraphCMS, mas você pode substituir pela sua própria API e fornecer o valor de `fieldName` com o que fizer mais sentido para o seu projeto. [Clique aqui para mais informações sobre as APIs do GraphCMS.](https://docs.graphcms.com/developers/api)

```js
{
    resolve: "gatsby-source-graphql",
        options: {
        // Nome arbitrário para o tipo do `schema`, pode ser o que você quiser.
        typeName: "GCMS",
        // Campo que será utilizado para acessar o `schema`, também pode ser o que você quiser.
        fieldName: "gcms",
        // O endereço da sua API, exibido no dashboard e nas configurações.
        // Por enquanto você pode usar essa API que contém as montanhas dos Estados Unidos.
        url: "https://api-euwest.graphcms.com/v1/cjm7tab4c04ro019omujh708u/master",
    },
},
```

Se tudo estiver configurado corretamente, agora os seus dados do GraphCMS foram adicionados à API nativa do Gatsby.

### Consultando os dados

A partir da pasta raíz do seu projeto, execute o comando `gatsby develop` para iniciar o site em modo de desenvolvimento. Assim que o servidor iniciar, se nenhum erro for apresentado, você poderá acessar o seguinte endereço no seu navegador:

`http://localhost:8000/___graphql`

Uma interface será exibida, onde você poderá testar os dados da sua nova API.

Tente executar essa consulta:

```graphql
query {
  gcms {
    mountains {
      title
      elevation
      image {
        url
      }
    }
  }
}
```

Novamente, se tudo estiver correto, o retorno será exibido no seguinte formato:

```json
{
  "data": {
    "gcms": {
      "mountains": [
        {
          "title": "Denali",
          "elevation": 6190,
          "image": {
            "url": "https://media.graphcms.com//J0rGKdjuSwCk7QrFxVDQ"
          }
        },
        {
          "title": "Mount Elbert",
          "elevation": 4401,
          "image": {
            "url": "https://media.graphcms.com//JNonajrqT6SOyUKgC4L2"
          }
        }
        // ...more results
      ]
    }
  }
}
```

### Obtendo o conteúdo na página

Para o propósito deste tutorial, todos os componentes que abrangem o template _starter_ do Gatsby foram removidos, como layout, SEO, link, entre outros. Esses componentes ainda existem, e 99% dos usuários irão optar por colocá-los novamente quando entenderem o que está acontecendo no código. Isso é apenas a ponta do iceberg, existem outras possibilidades a serem exploradas. Abra o arquivo `src/pages/index.js` e substitua o conteúdo por este trecho de código:

```jsx
import React from "react"
import { StaticQuery } from "gatsby"

const IndexPage = () => (
  <StaticQuery
    query={graphql`
      query {
        gcms {
          mountains {
            title
            elevation
          }
        }
      }
    `}
    render={(data) => (
      <div>
        <h1>USA Mountains</h1>
        <ul>
          {data.gcms.mountains.map((mountain) => {
            const { title, elevation } = mountain
            return (
              <li>
                <strong>{title}:</strong>
                {elevation}
              </li>
            )
          })}
        </ul>
      </div>
    )}
  />
)

export default IndexPage
```

Com esse código, você:

1. Adicionou o componente `StaticQuery` em uma página, que permite consultar dados da API do GraphQL.
2. Consultou alguns dados da API das montanhas, mais especificamente, _title_ e _elevation_.
3. Renderizou a lista utilizando a _render prop_ do componente `StaticQuery`.

## Sumário

Espera-se que você tenha visto o quão fácil é começar um projeto com GraphCMS e Gatsby. Com projetos de todos os tamanhos sendo beneficiados pela _JAM stack_, agora é o melhor momento para aprender Gatsby. Utilizar a API do GraphCMS no backend fornece um CMS escalável que você pode começar a utilizar em poucos minutos e continuar usando durante toda a vida útil do seu projeto.

[Confira o GraphCMS hoje e construa "sites rápidos", rápido!](https://graphcms.com?ref="gatsby-headless-docs-bottom")
