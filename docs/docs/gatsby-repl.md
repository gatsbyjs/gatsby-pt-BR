---
title: Gatsby REPL
---

O REPL ("read-eval-print loop") do Gatsby está disponível através do comando `gatsby repl`. Esse comando fornece acesso a um shell REPL interativo dentro do contexto do seu ambiente Gatsby. Podemos usá-lo para extrair dados gerais e interagir programaticamente com eles. Se você tem uma sugestão para um novo comando, sinta-se livre para criar um PR para ele!

Esse documento dará uma breve descrição de cada comando REPL, a saida esperada, e um exemplo do que podemos fazer com o comando para manipular dados. Os exemplos usam o [Gatsby Starter Blog](/starters/gatsbyjs/gatsby-starter-blog/) como ambiente de demonstração, já que atualmente é o starter mais conceituado e também por prover uma saida padrão para a maioria desses comandos.

Para iniciar, no seu terminal, após ter realizado a configuração inicial do site [aqui](/docs/quick-start), rode o comando `gatsby repl` para entrar no shell interativo. Se você estiver escrevendo uma função, você pode escreve-la em múltiplas linhas, contanto que você não use ponto e vírgula ou feche um parêntesis ou uma chave prematuramente. Isso é útil para rodar buscas no GraphQL e funções callback.

## Comandos REPL

- [`babelrc`](#babelrc)
- [`components`](#components)
- [`getNode`](#getNode)
- [`getNodes`](#getNodes)
- [`nodes`](#nodes)
- [`pages`](#pages)
- [`schema`](#schema)
- [`siteConfig`](#siteConfig)
- [`staticQueries`](#staticQueries)

### `babelrc`

Retorna um objeto com as configurações globais do `babelrc`.

Uso: `babelrc`

Exemplo:

```js
// Comando:
gatsby > babelrc
// Retorno:
{ stages:
   { develop: { plugins: [], presets: [], options: [Object] },
     'develop-html': { plugins: [], presets: [], options: [Object] },
     'build-html': { plugins: [], presets: [], options: [Object] },
     'build-javascript': { plugins: [], presets: [], options: [Object] } } }
```

### `components`

Retorna um objeto Map com todos os componentes no seu ambiente Gatsby (consulte a documentação da MDN sobre [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) para mais informação sobre objetos Map e como usar eles). Propriedades que são retornadas: `name`, `componentPath`, `query`, `pages`, e `isInBootstrap:`.

Uso: `components`

Exemplo:

```js
// Comando:
gatsby > for( var [key, value] of components ) { console.log(key + ' = ' + value.pages); }
// Retorno: uma lista de componentes e as páginas onde eles estão sendo usados...
.../my-blog-starter/src/templates/blog-post.js = /hi-folks/,/my-second-post/,/hello-world/
.../my-blog-starter/src/pages/404.js = /404/,/404.html
.../my-blog-starter/src/pages/index.js = /
.../my-blog-starter/.cache/dev-404-page.js = /dev-404-page/
```

### `getNode()`

Pega um único nó pelo seu ID, normalmente uma string.

Uso: `getNode(<id>)`

Exemplo:

```js
// Comando:
gatsby > getNode('SitePage /404.html')
// Retorno:
{ internalComponentName: 'Component404Html',
  path: '/404.html',
  ...
  id: 'SitePage /404.html',
  ...
  internal:
   { type: 'SitePage',
     contentDigest: '3688d3ee613222ebfe3f44bbdaeb8ca0',
     description: 'f795702c-a3b8-5a88-88ee-5d06019d44fa',
     owner: 'internal-data-bridge' } }
```

### `getNodes()`

Retorna um array de objetos (os nós)

Uso: `getNodes()`

Exemplos:

```js
// Comando:
gatsby > getNodes().map(node=>node.internal.type)
// Retorno:
[ 'SitePage',
  'SitePlugin',
  'SitePlugin',
  'SitePlugin',
  'SitePlugin',...] // Um array dos tipos internos de cada nó.

// Comando:
gatsby > getNodes().filter(node=> {if('MarkdownRemark' == node.internal.type) return node}).map(node=> node.frontmatter.title)
// Retorno:
[ 'Hello World', 'My Second Post!', 'New Beginnings' ] // Primeiro retorna um array de nós que sejam do tipo MarkdownRemark, então cria um array de títulos (postagens de blog).
```

### `nodes`

`nodes` é como `getNodes()`, mas retorna um array **indexado** de objetos (os nós). Também podemos passar o índice do nó desejado, com isso teremos o retorno de um array com um único objeto de nó.

Uso: `nodes` retorna o array, ou `nodes[<id>]` retorna um array com um objeto de nó.

Exemplos:

```js
// Comando:
gatsby > nodes.length
// Retorno:
48 // O tamanho do array de nós.

// Comando
gatsby > nodes[47]
// Retorno:
[ 47,
  { internalComponentName: 'Component404Html',
    path: '/404.html',
    ...
    componentPath: '.../my-blog-starter/src/pages/404.js',
    id: 'SitePage /404.html',
    ...
    internal:
     { type: 'SitePage',
       contentDigest: '1047b0e301924ae75175482834ef7b1a',
       description: 'f795702c-a3b8-5a88-88ee-5d06019d44fa',
       owner: 'internal-data-bridge' } } ]
```

### `pages`

Retorna um array indexado de arrays. Cada array contém uma chave que é o slug, e um valor que é o objeto de nó da página.

Uso: `pages` ou `pages[<index>]`

Exemplo:

```js
// Comando:
gatsby > pages[0]
// Retorno:
[ '/hi-folks/',
  { internalComponentName: 'ComponentHiFolks',
    path: '/hi-folks/',
    ...
    componentPath:
     '.../my-blog-starter/src/templates/blog-post.js' } ]
```

### `schema`

Retorna o schema GraphQL do seu ambiente Gatsby como um objeto.

Uso: `schema` ou `schema[<property>]`

Exemplo:

```js
// Comando:
gatsby > schema._implementations
// Retorno:
[Object: null prototype] {
  Node:
   [ File,
     MarkdownRemark,
     ImageSharp,
     SitePage,
     SitePlugin,
     Site,
     Directory ] } // Retorna o valor da propriedade das implementações.
```

### `siteConfig`

Retorna as configurações encontradas no arquivo `gatsby-config.js` do seu site como um objeto.

Uso: `siteConfig` ou `siteConfig[<property>]`

Exemplo:

```js
// Comando:
gatsby > siteConfig.siteMetadata
// Retorno:
{ title: 'Gatsby Starter Blog',
  author: 'Kyle Mathews',
  description: 'A starter blog demonstrating what Gatsby can do.',
  siteUrl: 'https://gatsby-starter-blog-demo.netlify.com/',
  social: { twitter: 'kylemathews' } } // Retorna apenas o valor da propriedade siteMetadata da config
```

### `staticQueries`

Retorna um objeto Map com todas as buscas estáticas no seu ambiente Gatsby. Propriedades que são retornadas: `name`, `componentPath`, `id`, `query`, e `hash`.

Uso: `staticQueries`

Exemplo:

```js
// Comando:
gatsby > for( var [key, value] of staticQueries ) { console.log(key + ' = ' + value.componentPath); }
// Retorno:
sq--src-components-seo-js = .../my-blog-starter/src/components/seo.js
sq--src-components-bio-js = .../my-blog-starter/src/components/bio.js
```
