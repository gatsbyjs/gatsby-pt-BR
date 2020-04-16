---
title: APIs de ciclo de vida do Gatsby
---



Gatsby fornece um conjunto rico de APIs de ciclo de vida para se conectar ao bootstrap
e operações de compilação e tempo de execução.



Os princípios de design do Gatsby incluem:

- Convenções > escrever código, mas use primitivas de baixo nível para criar
  convenções com código.
- A extração da lógica e da configuração em [plugins](/docs/plugins/) deve ser
  trivial e encorajado.
- Os plugins são facéis de abrir e reutilizar. Eles são apenas pacotes NPM.   


# Visão geral de alto nível



O modelo a seguir fornece uma visão geral conceitual de como os dados são originados e transformados no processo de construção de um site Gatsby:

<LayerModel />

## Sequência do Bootstrap 


Durante o "bootstrap" o Gatsby:

- lê e valida o `gatsby-config.js` para carregar na sua lista de plugins (ainda não os executa).
- exclui arquivos HTML e CSS de compilações anteriores (pasta pública)
- inicializa seu cache (armazenado em `/ .cache`) e verifica se algum plug-in foi atualizado desde a última execução, caso contrário, ele exclui o cache
- configura `gatsby-browser` e` gatsby-ssr` para plugins que os possuem
- inicia o processo principal de inicialização
  - executa [onPreBootstrap] (/docs/node-apis/#onPreBootstrap). Ex.: implementado por [`gatsby-plugin-typography`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-typography/src/gatsby-node.js)
- executa [sourceNodes] (/docs/node-apis/#sourceNodes) Ex.: implementado por [`gatsby-source-wikipedia`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-wikipedia/src/gatsby-node.js)
  - dentro disso, o `createNode` pode ser chamado várias vezes, o que aciona o [onCreateNode] (/docs/node-apis/#onCreateNode)
- cria esquema inicial do GraphQL
- executa [resolvableExtensions] (/docs/node-apis/#resolvableExtensions) que permite que plug-ins registrem tipos ou extensões de arquivo, por exemplo [`gatsby-plugin-typescript`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-typescript/src/gatsby-node.js)
- executa [createPages] (/docs/node-apis/#createPages) a partir do gatsby-node.js no diretório raiz do projeto, Ex.: implementado por [`page-hot-reloader`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/bootstrap/page-hot-reloader.js)
  - com isso, `createPage` pode ser chamado várias vezes, o que aciona [onCreatePage] (/ docs / node-apis / # onCreatePage)
- executa [createPagesStatefully] (/docs/node-apis/#createPagesStatefully)
- executa nós de origem novamente e atualiza o esquema GraphQL para incluir páginas dessa vez
- executa [onPreExtractQueries] (/docs/node-apis/#onPreExtractQueries) Ex.: implementado por [`gatsby-transformer-sharp`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-transformer-sharp/src/gatsby-node.js) e [` gatsby-source -contentful`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-contentful/src/gatsby-node.js) e extrai consultas de páginas e componentes (`StaticQuery`)
- compila consultas GraphQL e cria a Árvore de Sintaxe Abstrata (ASA)
- executa validação de consulta com base no esquema
- executa consultas e armazena seus respectivos resultados
- escreve redirecionamentos de página (se houver) para `.cache / redirects.json`
- o ciclo de vida [onPostBootstrap] (/docs/node-apis/#onPostBootstrap) é executado


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



(para ser escrito)

## Sequência de cliente

(para ser escrito)

---

Consulte os links à esquerda em "REFERENCE" para obter a documentação completa da API.
