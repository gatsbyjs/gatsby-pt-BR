---
title: APIs de ciclo de vida do Gatsby
---

import LayerModel from "../../www/src/components/layer-model"

Gatsby fornece um conjunto rico de APIs de ciclo de vida para se conectar ao bootstrap
e operações de compilação e tempo de execução.

Os princípios de design do Gatsby incluem:

- Convenções > escreva códigos, mas use primitivas de baixo nível para criar
  convenções com código.
- A extração da lógica e da configuração em [plugins](/docs/plugins/) deve ser
  trivial e encorajado.
- Os plugins são facéis de abrir e reutilizar. Eles são apenas pacotes do NPM.   

# Visão geral de alto nível

O modelo a seguir fornece uma visão geral conceitual de como os dados são originados e transformados no processo de construção de um site de Gatsby:

<LayerModel />

## Sequência do Bootstrap 

Durante o "bootstrap" o Gatsby:

- lê o `gatsby-config.js` para carregar a sua lista de plugins
- inicializa seu cache(armazenado em `/.cache`)
- extrai e pré-processa os dados (origina e transforma os nós) em um esquema GraphQL
- cria páginas na memória
  - da sua pasta `/pages`
  - do seu `gatsby-config.js` se você implementar `createPages`/`createPagesStatefully` por exemplo.
  - de qualquer plugin que implemente `createPages`/`createPagesStatefully`
- extrai, executa e substitui consultas graphql para páginas e `StaticQuery`s
- grava as páginas para armazenar em cache  

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
- [no Post Bootstrap](/docs/node-apis/#onPostBootstrap) is called (mas não é frequentemente usado)

## Sequência de compilação

(para ser escrito)

## Sequência de cliente

(para ser escrito)

---

Consulte os links à esquerda em "REFERENCE" para obter a documentação completa da API.
