---
title: APIs de ciclo de vida do Gatsby
---


import LayerModel from "../../www/src/components/layer-model"

Gatsby fornece um conjunto rico de APIs de ciclo de vida para se conectar ao bootstrap
e operações de compilação e tempo de execução.

Gatsby provides a rich set of lifecycle APIs to hook into its bootstrap,
build, and client runtime operations.


Os princípios de design do Gatsby incluem:

- Convenções > escrever código, mas use primitivas de baixo nível para criar
  convenções com código.
- A extração da lógica e da configuração em [plugins](/docs/plugins/) deve ser
  trivial e encorajado.
- Os plugins são facéis de abrir e reutilizar. Eles são apenas pacotes NPM.   


# Visão geral de alto nível

## High level Overview


O modelo a seguir fornece uma visão geral conceitual de como os dados são originados e transformados no processo de construção de um site Gatsby:

<LayerModel />

## Sequência do Bootstrap 


Durante o "bootstrap" o Gatsby:

- lê o `gatsby-config.js` para carregar a sua lista de plugins
- inicializa seu cache (armazenado em `/.cache`)
- extrai e pré-processa os dados (origina e transforma os nós) em um esquema GraphQL
- cria páginas na memória
  - da sua pasta `/pages`
  - do seu `gatsby-config.js` se você implementar `createPages`/`createPagesStatefully` por exemplo.
  - de qualquer plugin que implemente `createPages`/`createPagesStatefully`
- extrai, executa e substitui consultas graphql para páginas e `StaticQuery`s
- grava as páginas para armazenar em cache

During the main bootstrap sequence, Gatsby (in this order):

- reads and validates `gatsby-config.js` to load in your list of plugins (it doesn't run them yet).
- deletes HTML and CSS files from previous builds (public folder)
- initializes its cache (stored in `/.cache`) and checks if any plugins have been updated since the last run, if so it deletes the cache
- sets up `gatsby-browser` and `gatsby-ssr` for plugins that have them
- starts main bootstrap process
  - runs [onPreBootstrap](/docs/node-apis/#onPreBootstrap). e.g. implemented by [`gatsby-plugin-typography`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-typography/src/gatsby-node.js)
- runs [sourceNodes](/docs/node-apis/#sourceNodes) e.g. implemented by [`gatsby-source-wikipedia`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-wikipedia/src/gatsby-node.js)
  - within this, `createNode` can be called multiple times, which then triggers [onCreateNode](/docs/node-apis/#onCreateNode)
- creates initial GraphQL schema
- runs [resolvableExtensions](/docs/node-apis/#resolvableExtensions) which lets plugins register file types or extensions e.g. [`gatsby-plugin-typescript`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-typescript/src/gatsby-node.js)
- runs [createPages](/docs/node-apis/#createPages) from the gatsby-node.js in the root directory of the project e.g. implemented by [`page-hot-reloader`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/bootstrap/page-hot-reloader.js)
  - within this, `createPage` can be called any number of times, which then triggers [onCreatePage](/docs/node-apis/#onCreatePage)
- runs [createPagesStatefully](/docs/node-apis/#createPagesStatefully)
- runs source nodes again and updates the GraphQL schema to include pages this time
- runs [onPreExtractQueries](/docs/node-apis/#onPreExtractQueries) e.g. implemented by [`gatsby-transformer-sharp`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-transformer-sharp/src/gatsby-node.js) and [`gatsby-source-contentful`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-contentful/src/gatsby-node.js), and extracts queries from pages and components (`StaticQuery`)
- compiles GraphQL queries and creates the Abstract Syntax Tree (AST)
- runs query validation based on schema
- executes queries and stores their respective results
- writes page redirects (if any) to `.cache/redirects.json`
- the [onPostBootstrap](/docs/node-apis/#onPostBootstrap) lifecycle is executed


No desenvolvimento, esse é um processo de execução desenvolvido com o [Webpack](https://github.com/gatsbyjs/gatsby/blob/dd91b8dceb3b8a20820b15acae36529799217ae4/packages/gatsby/package.json#L128) e [`react-hot-loader`](https://github.com/gatsbyjs/gatsby/blob/dd91b8dceb3b8a20820b15acae36529799217ae4/packages/gatsby/package.json#L104), para que as alterações em qualquer arquivo sejam reexecutadas pela sequência novamente, com [smart cache invalidation](https://github.com/gatsbyjs/gatsby/blob/ffd8b2d691c995c760fe380769852bcdb26a2278/packages/gatsby/src/bootstrap/index.js#L141). Por exemplo, `gatsby-source-filesystem` observa os arquivos quanto a alterações, e cada alteração aciona consultas reexecutadas. Outros plugins também podem executar esse serviço.
Isso também vale para as consultas, portanto se você modificar uma consulta, seu aplicativo de desenvolvimento é recarregado. 

O núcleo do processo de bootstrap é o "api-runner", que ajuda a executar APIs em sequência, com o estado gerenciado no Redux. O Gatsby expõe várias APIs do ciclo de vida que podem ser implementadas por você (ou por qualquer um de seus plugins configurados) em `gatsby-node.js`,` gatsby-browser.js` ou `gatsby-ssr.js`.


A sequência dos ciclos de vida da API do nó bootstrap **main** é:

- [na pré-inicialização](/docs/node-apis/#onPreBootstrap) Ex.: implementado por [`gatsby-plugin-typography`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-typography/src/gatsby-node.js)
- [Nós de origem](/docs/node-apis/#sourceNodes) Ex.: implementado por [`gatsby-source-wikipedia`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-wikipedia/src/gatsby-node.js)
  - Dentro deste pode ser chamado várias vezes, o que aciona o `createNode` [onCreateNode](/docs/node-apis/#onCreateNode).
- (A primeira compilação de esquema acontece aqui)
- [Extensões resolvíveis](/docs/node-apis/#resolvableExtensions) para extensões de tipo de arquivo / idioma,  Ex.: [`gatsby-plugin-typescript`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-typescript/src/gatsby-node.js)
- [criar páginas](/docs/node-apis/#createPages) Ex.: implementado por [`page-hot-reloader`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/bootstrap/page-hot-reloader.js)
  - dentro deste `createPage` pode ser chamado várias vezes, o que aciona [onCreatePage](/docs/node-apis/#onCreatePage)
- [na pré-extração de consultas](/docs/node-apis/#onPreExtractQueries) Ex.: implementado por [`gatsby-transformer-sharp`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-transformer-sharp/src/gatsby-node.js) e [`gatsby-source-contentful`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-contentful/src/gatsby-node.js)
- (atualização de esquema acontece aqui)
- **extrair consultas de componentes** onde o [compilador de consultas](https://github.com/gatsbyjs/gatsby/blob/6de0e4408e14e599d4ec73948eb4153dc3cde849/packages/gatsby/src/internal-plugins/query-runner/query-compiler.js#L189) substitui as consultas da página GraphQL e o `StaticQueries`
- As [consultas são executadas](https://github.com/gatsbyjs/gatsby/blob/6de0e4408e14e599d4ec73948eb4153dc3cde849/packages/gatsby/src/internal-plugins/query-runner/page-query-runner.js#L120), e [as páginas são gravadas](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/query/redirects-writer.js)
- [onPostBootstrap](/docs/node-apis/#onPostBootstrap) é chamado (mas não é frequentemente usado)

## Sequência de compilação

## Build sequence


(para ser escrito)

## Sequência de cliente

(para ser escrito)

---

Consulte os links à esquerda em "REFERENCE" para obter a documentação completa da API.
