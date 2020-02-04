---
title: Criação de Página
---

Uma página é criada chamando a função [createPage](/docs/actions/#createPage). Existem três principais consequências que ocorrem quando uma página é criada.

<<<<<<< HEAD
1. O namespace redux das `páginas` é atualizado
2. O namespace redux dos `componentes` é atualizado
3. A API `onCreatePage` é executada

## Atualizar redux namespace das páginas

O namespace redux das `páginas` é um mapa do `caminho` da página para o objeto da página. O [pages reducer](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/redux/reducers/pages.js) é responsável por atualizar a página utilizando a ação `CREATE_PAGE`. Ele também cria uma [Referência de Chave Estrangeira](/docs/schema-gql-type/#foreign-key-reference-___node) no plugin que criou a página, adicionando um campo `pluginCreator___NODE`.

## Atualizar redux namespace dos componentes

O namespace redux dos `components` é um mapa do [componentPath](/docs/behind-the-scenes-terminology/#component) (arquivo com o componente React) para o objeto de um componente. Um objeto de um componente é simplesmente o objeto da página, mas com uma string de consulta vazia (que será definida durante [Extração de Consulta](/docs/query-extraction/#store-queries-in-redux)).
=======
1. The `pages` Redux namespace is updated
1. The `components` Redux namespace is updated
1. `onCreatePage` API is executed

## Update pages Redux namespace

The `pages` Redux namespace is a map of page `path` to page object. The [pages reducer](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/redux/reducers/pages.js) takes care of updating this on a `CREATE_PAGE` action. It also creates a [Foreign Key Reference](/docs/schema-gql-type/#foreign-key-reference-___node) to the plugin that created the page by adding a `pluginCreator___NODE` field.

## Update components Redux namespace

The `components` Redux namespace is a map of [componentPath](/docs/behind-the-scenes-terminology/#component) (file with React component) to the Component object. A Component object is simply the Page object but with an empty query string (that will be set during [Query Extraction](/docs/query-extraction/#store-queries-in-redux)).
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

## API onCreatePage

Sempre que uma página é criada, os plugins têm a oportunidade de manipular seu evento [onCreatePage](/docs/node-apis/#onCreatePage). Isso é usado para coisas como a criação de nós `SitePage` no [Internal Data Bridge](/docs/internal-data-bridge/), e para plugins relacionados ao "caminho", como [gatsby-plugin-create-client-paths](/packages/gatsby-plugin-create-client-paths/) e [gatsby-plugin-remove-trailing-slashes](/packages/gatsby-plugin-remove-trailing-slashes/).
