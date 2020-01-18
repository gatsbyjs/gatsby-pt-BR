---
title: Customizando o Schema GraphQL
---

Um dos principais pontos fortes de Gatsby é a capacidade de consultar dados de uma variedade de
fontes de maneira uniforme com o GraphQL. Para que isso funcione, um Schema GraphQL
que define a forma dos dados deve ser gerado.

Gatsby é capaz de inferir automaticamente um Schema GraphQL a partir de seus dados, e em
muitos casos, isso é realmente tudo que você precisa. No entanto, existem situações em que você
quer definir explicitamente a forma dos dados, ou adicionar funcionalidade personalizada
à camada de consulta - é isso que a API de Customização de Schema do Gatsby fornece.

O guia a seguir mostra alguns exemplos para demonstrar a API.

> Este guia é destinado a autores de plugins, usuários tentando corrigir Schemas do GraphQL
> criado por inferência automática de tipo, desenvolvedores que otimizam construções para sites
> maiores, e qualquer pessoa interessada em personalizar a geração de schemas do Gatsby.
> Como tal, o guia pressupõe que você esteja familiarizado com os tipos do GraphQL
> e com o uso de Node APIs do Gatsby. Para uma abordagem de alto nível sobre o uso de
> Gatsby com GraphQL, consulte a [referência da API](/docs/graphql-api/).

## Definindo tipos de dados explicitamente

O projeto de exemplo é um blog que obtém seus dados de arquivos Markdown locais que
fornece o conteúdo da postagem, bem como informações do autor no formato JSON. Há também
colaboradores convidados ocasionais cujas informações são mantidas em um arquivo JSON separado.

```markdown:title=src/data/post1.md
---
title: Sample Post
publishedAt: 2019-04-01
author: jane@example.com
tags:
  - wow
---

# Heading

Text
```

```json:title=src/data/author.json
[
  {
    "name": "Doe",
    "firstName": "Jane",
    "email": "jane@example.com",
    "joinedAt": "2018-01-01"
  }
]
```

```json:title=src/data/contributor.json
[
  {
    "name": "Doe",
    "firstName": "Zoe",
    "email": "zoe@example.com",
    "receivedSwag": true
  }
]
```

Para poder consultar o conteúdo desses arquivos com o GraphQL, eles precisam primeiro ser
carregados no armazenamento de dados interno do Gatsby. É isso que os plugins de fonte e transformadores
fazem - neste caso `gatsby-source-filesystem` e
`gatsby-transformer-remark` mais `gatsby-transformer-json`. Cada arquivo markdown de post
é transformado em um objeto "node" no armazenamento de dados interno com
um `id` único e com o tipo `MarkdownRemark`. Da mesma forma, um autor será
representado por um objeto node do tipo `AuthorJson`, e as informações do colaborador serão
transformadas em objetos node do tipo `ContributorJson`.

### A interface Node

Essa estrutura de dados é representada no schema GraphQL do Gatsby com a interface `Node`
, que descreve o conjunto de campos comuns aos objetos node criados por
plugins de fonte e transformadores (`id`, `parent`, `children`, bem como alguns
campos `internal` como `type`). Em GraphQL Schema Definition Language (SDL),
é algo parecido com isso:

```graphql
interface Node {
  id: ID!
  parent: Node!
  children: [Node!]!
  internal: Internal!
}

type Internal {
  type: String!
}
```

Os tipos criados pelos plugins de fonte e transformadores implementam essa interface. Por
exemplo, o tipo node criado por `gatsby-transformer-json` para `authors.json`
será representado no schema GraphQL como:

```graphql
type AuthorJson implements Node {
  id: ID!
  parent: Node!
  children: [Node!]!
  internal: Internal!
  name: String
  firstName: String
  email: String
  joinedAt: Date
}
```

> Uma maneira rápida de inspecionar o schema gerado pelo Gatsby é o GraphQL Playground.
> Inicie seu projeto com `GATSBY_GRAPHQL_IDE=playground gatsby develop`, abra o
> playground em `http://localhost:8000/___graphql` e inspecione a aba `Schema` à
> direita.

### Inferência automática de tipo

É importante observar que os dados em `author.json` não fornecem informações de tipo
dos campos _Author_ por si só. Para converter o formato dos dados
em definições de tipo GraphQL, o Gatsby precisa inspecionar o conteúdo de
todos os campos e verificar seu tipo. Em muitos casos, isso funciona muito bem e isso ainda é
o mecanismo padrão para criar um schema GraphQL.

No entanto, existem dois problemas com essa abordagem: (1) é bastante
demorado e, portanto, não escala muito bem e (2) se os valores em um
campo são de tipos diferentes, o Gatsby não pode decidir qual é o correto.
Uma conseqüência disso é que, se suas fontes de dados mudarem, a inferência de tipo pode
de repente falhar.

Ambos os problemas podem ser resolvidos fornecendo definições explícitas de tipos para o schema GraphQL
do Gatsby.

### Criando definições de tipo

Olhe primeiro para o último caso. Suponha que um novo autor entre na equipe, mas na
entrada do novo autor, há um erro de digitação no campo `joinAt`: "201-04-02" a qual
não é uma Data válida.

```diff:title=src/data/author.json
+  {
+    "name": "Doe",
+    "firstName": "John",
+    "email": "john@example.com",
+    "joinedAt": "201-04-02"
+  }
]
```

Isso confundirá a inferência de tipo de Gatsby, já que o campo `joinAt`
agora terá os valores Date e String.

#### Consertando tipos de campos

Para garantir que o campo sempre seja do tipo Date, você pode fornecer definições
explícitas de tipo para Gatsby com a action [`createTypes`](/docs/actions/#createTypes).
Ele aceita definições de tipo em GraphQL Schema Definition Language:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createTypes } = actions
  const typeDefs = `
    type AuthorJson implements Node {
      joinedAt: Date
    }
  `
  createTypes(typeDefs)
}
```

Observe que o restante dos campos (`name`, `firstName` etc.) não tem que ser
fornecidos, eles ainda serão tratados pela inferência de tipo do Gatsby.

> As actions para personalizar a geração de schemas do Gatsby são disponibilizadas nas APIs
> [`createSchemaCustomization`](/docs/node-apis/#createSchemaCustomization)
> (available in Gatsby v2.12 and above),
> e [`sourcesNodes`](/docs/node-apis/#sourceNodes).

#### Não optando pela inferência de tipo

No entanto, existem vantagens em fornecer definições completas para um tipo de node, e
ignorar completamente o mecanismo de inferência de tipo. Em projetos de menor escala,
a inferência geralmente não é um problema de desempenho, mas à medida que os projetos crescem,
a penalidade de desempenho de ter que verificar cada tipo de campo será perceptível.

Gatsby permite desativar a inferência com a diretiva de tipo `@dontInfer` - a qual
por sua vez, exige que você forneça explicitamente definições de tipo para todos os campos
que devem estar disponíveis para consulta:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createTypes } = actions
  const typeDefs = `
    type AuthorJson implements Node @dontInfer {
      name: String!
      firstName: String!
      email: String!
      joinedAt: Date
    }
  `
  createTypes(typeDefs)
}
```

Observe que você não precisa fornecer explicitamente os campos da interface do Node (`id`,
`parent`, etc.), Gatsby irá adicioná-los automaticamente para você.

> Se você está se perguntando sobre os pontos de exclamação - eles permitem
> [especificar anulabilidade](https://graphql.org/learn/schema/#lists-and-non-null)
> em GraphQL, ou seja, se é permitido que um valor de campo seja `null` ou não.

#### Tipos aninhados

Até o momento, o projeto de exemplo trata apenas de valores escalares (`String` e `Date`;
O GraphQL também conhece `ID`, `Int`, `Float`, `Boolean` e `JSON`). No entanto,
os campos podem também conter valores complexos de objetos. Para selecionar esses campos no GraphQL SDL, você
pode fornecer uma definição de tipo completa para o tipo aninhado, que pode ser arbitrariamente
nomeado (desde que o nome seja exclusivo no schema). No projeto de exemplo, o
campo `frontmatter` no tipo de node `MarkdownRemark` é um bom exemplo. Digamos que você
quer garantir que o `frontmatter.tags` sempre seja um array de strings.

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createTypes } = actions
  const typeDefs = `
    type MarkdownRemark implements Node {
      frontmatter: Frontmatter
    }
    type Frontmatter {
      tags: [String!]!
    }
  `
  createTypes(typeDefs)
}
```

Observe que, com `createTypes`, você não pode direcionar diretamente para um tipo de`Frontmatter`
sem especificar também que este é o tipo do campo `frontmatter` no
tipo `MarkdownRemark`, O seguinte falharia porque Gatsby não teria como
saber em qual campo o tipo `Frontmatter` deve ser aplicado:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createTypes } = actions
  const typeDefs = `
    # Isso vai falhar !!!
    type Frontmatter {
      tags: [String]!
    }
  `
  createTypes(typeDefs)
}
```

É útil pensar nos seus dados e no schema GraphQL correspondente, 
sempre iniciando nos tipos de Node criados pelos plugins de fonte e de transformação.

> Observe que o tipo `Frontmatter` não deve implementar a interface Node já que
> não é um tipo de alto nível criado por plugins de fonte ou transformador: não tem
> o campo `id`, e existe apenas para descrever a forma dos dados em um campo aninhado.

#### Construtores de Tipo Gatsby

Em muitos casos, o GraphQL SDL fornece uma maneira sucinta de fornecer definições de tipo
para o seu schema. Se, no entanto, você precisar de mais flexibilidade, `createTypes` também
aceita definições de tipo fornecidas com a ajuda de Construtores de Tipo Gatsby, os quais
são mais flexíveis que a sintaxe SDL, mas menos detalhados que `graphql-js`. Eles são
acessíveis no argumento `schema` passado para as APIs do Node.

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions, schema }) => {
  const { createTypes } = actions
  const typeDefs = [
    schema.buildObjectType({
      name: "ContributorJson",
      fields: {
        name: "String!",
        firstName: "String!",
        email: "String!",
        receivedSwag: {
          type: "Boolean",
          resolve: source => source.receivedSwag || false,
        },
      },
      interfaces: ["Node"],
    }),
  ]
  createTypes(typeDefs)
}
```

Os Construtores de Tipo do Gatsby permitem referênciar tipos como strings simples, e aceitam configurações
de campo completas (`type`, `args`, `resolve`). Ao definir tipos de alto nível, não esqueça
de passar `interfaces: ['Node']`, que faz o mesmo para os Construtores de Tipo assim como adicionar
`implements Node` faz para tipos definidos por SDL. Também é possível optar por não usar inferência
de tipo com Construtores de Tipo configurando a extensão de tipo `infer` como `false`:

```diff
schema.buildObjectType({
  name: "ContributorJson",
  fields: {
    name: "String!",
  },
  interfaces: ["Node"],
+ extensions: {
+   // Enquanto em SDL, você tem duas diretivas diferentes, @infer e @dontInfer para
+   // controlar comportamento de inferência, Construtores de Tipo do Gatsby recebem um única extensão 
+   // `infer` que aceita um Boolean
+   infer: false
+ },
}),
```

> Os Construtores de Tipo também existem para os tipos Input, Interface e Union:
> `buildInputType`, `buildInterfaceType`, e `buildUnionType`.
> Note que a action `createTypes` também aceita tipos `graphql-js` diretamente,
> mas geralmente SDL ou Construtores de Tipo são as melhores alternativas.

#### Campos de chave estrangeira

A inferência automática de tipo do Gatsby tem um truque na manga: para cada campo
que termina em `___NODE` ele interpretará o valor do campo como um `id` e cria uma
relação de chave estrangeira.

> Nota: Antes da introdução das APIs de personalização de Schema no Gatsby v2.2,
> havia dois mecanismos para criar links entre tipos de node: um autor de plugin usaria a convenção de
> nome de campo `___NODE` (para plugins), e um usuário definiria [mapeamentos](/docs/gatsby-config/#mapping-node-types) entre campos em `gatsby-config.js`. Ambos, usuários e autores de plugins agora podem usar a extensão `@link` descrita abaixo.

Criar relações de chaves estrangeiras com a action `createTypes`,
ou seja, sem depender da inferência de tipo e da convenção de nomenclatura de campo
`___NODE`, requer um pouco de configuração manual.

No projeto de exemplo, o campo `frontmatter.author` nos nodes
`MarkdownRemark` expande o valor do campo fornecido para um node completo `AuthorJson`.
Para que isso funcione, é necessário fornecer um _resolver_ de campo personalizado. (veja abaixo para
mais informações sobre `context.nodeModel`)

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions, schema }) => {
  const { createTypes } = actions
  const typeDefs = [
    "type MarkdownRemark implements Node { frontmatter: Frontmatter }",
    schema.buildObjectType({
      name: "Frontmatter",
      fields: {
        author: {
          type: "AuthorJson",
          resolve: (source, args, context, info) => {
            // Se você estivesse linkando por ID, poderia usar `getNodeById` para
            // encontrar o autor correto:
            // return context.nodeModel.getNodeById({
            //   id: source.author,
            //   type: "AuthorJson",
            // })
            // Mas como o exemplo está usando o email do autor como chave estrangeira,
            // você pode usar `runQuery`, ou obter todos os nodes de autores
            // com `getAllNodes` e procurar manualmente pelo node do autor
            // linkado:
            return context.nodeModel
              .getAllNodes({ type: "AuthorJson" })
              .find(author => author.email === source.author)
          },
        },
      },
    }),
  ]
  createTypes(typeDefs)
}
```

O que está acontecendo aqui é que você fornece um _resolver_ de campo personalizado que pergunta
ao armazenamento de dados interno do Gatsby sobre o objeto completo de _node_ com o
`id` e `type` especificados.

Porque criar relações de chave estrangeira é um caso de uso tão comum, Gatsby
felizmente, também fornece uma maneira muito mais fácil de fazer isso -- com a ajuda de
extensões ou diretivas. Seria algo semelhante a isso:

```graphql
type MarkdownRemark implements Node {
  frontmatter: Frontmatter
}
type Frontmatter {
  author: AuthorJson @link # relação de chave estrangeira padrão por `id`
  reviewers: [AuthorJson] @link(by: "email") # relação de chave estrangeira por campo personalizado
}
type AuthorJson implements Node {
  posts: [MarkdownRemark] @link(by: "frontmatter.author.email", from: "email") # referência fácil
}
```

Você fornece uma diretiva `@link` em um campo o Gatsby internamente irá
adicionar um _resolver_ que é bastante semelhante ao escrito manualmente acima. Se nenhum
argumento for fornecido, o Gatsby usará o campo `id` como chave estrangeira,
caso contrário, a chave estrangeira deve ser fornecida com o argumento `by`. O
argumento opcional `from` permite obter o campo no tipo atual que atua como chave estrangeira no campo especificado em `by`.
em outras palavras, você cria um `link` **em** `from` **para** `by`. Isso torna o `from` especialmente útil ao adicionar um campo para linkar de volta.

> Observe que ao usar `createTypes` para corrigir inferência de tipo para um campo de chave estrangeira
> criado por um plugin, os dados subjacentes provavelmente existirão em um campo com
> um sufixo `___NODE`. Use o argumento `from` para apontar a extensão `link` para
> o nome do campo correto. Por exemplo: `author: [AuthorJson] @link(from: "author___NODE")`.

#### Extensões e diretivas

Por padrão, Gatsby fornece [quatro extensões](/docs/actions/#createTypes)
que permitem adicionar funcionalidade personalizada aos campos sem precisar escrever
_resolvers_ de campo manualmente: a extensão `link` já foi discutida acima,
`dateformat` permite adicionar opções de formatação de data, `fileByRelativePath` é
similar a `link` mas resolverá os caminhos relativos quando linkada a nodes `File`,
e `proxy` é útil ao lidar com dados que contêm nomes de campos com
caracteres que são inválidos em GraphQL.

Para adicionar uma extensão a um campo, você pode usar uma diretiva no SDL ou a
propriedade `extensions` ao usar Construtores de Tipo do Gatsby:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ action, schema }) => {
  const { createTypes } = actions
  const typeDefs = [
    "type MarkdownRemark implements Node { frontmatter: Frontmatter }",
    `type Frontmatter {
      publishedAt: Date @dateformat(formatString: "DD-MM-YYYY")
    }`
    schema.buildObjectType({
      name: 'AuthorJson',
      fields: {
        joinedAt: {
          type: 'Date',
          extensions: {
            dateformat: {}
          }
        }
      }
    })
  ]
  createTypes(typeDefs)
}
```

O exemplo acima adiciona [opções de formatação de data](/docs/graphql-reference/#dates)
para os campos `AuthorJson.joinedAt` e `MarkdownRemark.frontmatter.publishedAt`.
Essas opções estão disponíveis como argumentos de campo ao consultar esses campos:

```graphql
query {
  allAuthorJson {
    joinedAt(fromNow: true)
  }
}
```

`publishedAt` também recebe uma `formatString` padrão, a qual será usada
quando nenhuma opção de formatação explícita é fornecida na consulta.

#### Definindo valores de campo padrão

Para definir valores de campo padrão, o Gatsby atualmente (ainda) não fornece uma
extensão pronta para uso, então resolver um campo para um valor padrão (ao invés de
`null`) requer a adição manual de um _resolver_ de campo. Por exemplo, para adicionar uma tag
padrão para todos posts do blog:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ action, schema }) => {
  const { createTypes } = actions
  const typeDefs = [
    "type MarkdownRemark implements Node { frontmatter: Frontmatter }",
    schema.buildObjectType({
      name: "Frontmatter",
      fields: {
        tags: {
          type: "[String!]",
          resolve(source, args, context, info) {
            // Para uma solução mais genérica, você pode escolher o valor do campo em
            // `source[info.fieldName]`
            const { tags } = source
            if (source.tags == null || (Array.isArray(tags) && !tags.length)) {
              return ["uncategorized"]
            }
            return tags
          },
        },
      },
    }),
  ]
  createTypes(typeDefs)
}
```

#### Criando extensões personalizadas

Com a action [`createFieldExtension`](/docs/actions/#createFieldExtension)
é possível definir extensões personalizadas como uma maneira de adicionar funcionalidade reutilizável
para campos. Digamos que você queira adicionar um campo `fullName` ao `AuthorJson`
e ao `ContributorJson`.

É claro que você poderia escrever um `fullNameResolver` e usá-lo em dois lugares:

```js:title=gatsby-node.js
const fullNameResolver = source => `${source.firstName} ${source.name}`

exports.createSchemaCustomization = ({ actions, schema }) => {
  actions.createTypes([
    {
      name: "AuthorJson",
      interfaces: ["Node"],
      fields: {
        fullName: {
          type: "String",
          resolve: fullNameResolver,
        },
      },
    },
    {
      name: "ContributorJson",
      interfaces: ["Node"],
      fields: {
        fullName: {
          type: "String",
          resolve: fullNameResolver,
        },
      },
    },
  ])
}
```

No entanto, para disponibilizar essa funcionalidade para outros plugins também, e fazê-la ser
usável em SDL, você pode registrá-la como uma extensão de campo.

Uma definição de extensão de campo requer um nome e uma função `extend`, a qual
deve retornar uma configuração de campo (parcial) (um objeto com `type`, `args`, `resolve`)
que será mesclado na configuração existente do campo.

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createFieldExtension, createTypes } = actions

  createFieldExtension({
    name: "fullName",
    extend(options, prevFieldConfig) {
      return {
        resolve(source) {
          return `${source.firstName} ${source.name}`
        },
      }
    },
  })

  createTypes(`
    type AuthorJson implements Node {
      fullName: String @fullName
    }
    type ContributorJson implements Node {
      fullName: String @fullName
    }
  `)
}
```

Essa abordagem se torna muito mais poderosa quando os plugins fornecem extensões de campo
personalizadas. Um plugin transformador de markdown _muito_ básico poderia por exemplo fornecer
uma extensão para converter strings de markdown para html:

```js:title=gatsby-transformer-basic-md/src/gatsby-node.js
const remark = require(`remark`)
const html = require(`remark-html`)

exports.createSchemaCustomization = ({ actions }) => {
  actions.createFieldExtension({
    name: "md",
    args: {
      sanitize: {
        type: "Boolean!",
        defaultValue: true,
      },
    },
    // A extensão `args` (acima) é passada a `extend` como
    // o primeiro argumento (`options` abaixo)
    extend(options, prevFieldConfig) {
      return {
        args: {
          sanitize: "Boolean",
        },
        resolve(source, args, context, info) {
          const fieldValue = context.defaultFieldResolver(
            source,
            args,
            context,
            info
          )
          const shouldSanitize =
            args.sanitize != null ? args.sanitize : options.sanitize
          const processor = remark().use(html, { sanitize: shouldSanitize })
          return processor.processSync(fieldValue).contents
        },
      }
    },
  })
}
```

Ela pode ser usada em qualquer chamada `createTypes` simplesmente adicionando a diretiva/extensão
ao campo:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  actions.createTypes(`
    type BlogPost implements Node {
      content: String @md
    }
  `)
}
```

Observe que no exemplo acima, houve opções adicionais de configuração fornecidas
com `args`. Este exemplo é útil para fornecer argumentos de campo padrão:

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  actions.createTypes(`
    type BlogPost implements Node {
      content: String @md(sanitize: false)
    }
  `)
}
```

Observe também que as extensões de campo podem decidir se um _resolver_ de campo existente
deve ser quebrado ou substituído. Os exemplos acima decidiram simplesmente retornar
uma nova função `resolve`. Porque a função `extend` recebe a configuração atual
de campo como seu segundo argumento, uma extensão também pode decidir envolver um _resolver_ existente:

```diff
extend(options, prevFieldConfig) {
+  const { resolve } = prevFieldConfig
+  return {
+    async resolve(source, args, context, info) {
+      const resultFromPrevResolver = await resolve(source, args, context, info)
      /* ... */
+      return processor.processSync(resultFromPrevResolver).contents
+    }
+  }
}
```

Se várias extensões de campo forem adicionadas a um campo, os _resolvers_ serão processados ​​nesta ordem:
primeiro um _resolver_ personalizado adicionado com `createTypes` (ou `createResolvers`) executa, então os
 _resolvers_ de extensão de campo são executados da esquerda para a direita.

Por fim, observe que, para obter o fieldValue atual, você usa `context.defaultFieldResolver`.

## API createResolvers

Embora seja possível passar diretamente `args` e `resolvers` pelas definições
de tipo usando Construtores de Tipo do Gatsby, uma abordagem alternativa, especificamente
adaptada para adicionar _resolvers_ personalizados aos campos, é a API de Node
`createResolvers`

```js:title=gatsby-node.js
exports.createResolvers = ({ createResolvers }) => {
  const resolvers = {
    Frontmatter: {
      author: {
        resolve(source, args, context, info) {
          return context.nodeModel.getNodeById({
            id: source.author,
            type: "AuthorJson",
          })
        },
      },
    },
  }
  createResolvers(resolvers)
}
```

Observe que `createResolvers` permite adicionar novos campos aos tipos, modificar `args`
e `resolver` -- mas não substituindo o tipo do campo. Isto é porque
`createResolvers` é executado por último na geração de schema, e modificar um tipo de campo
significaria ter que regenerar os tipos de entrada correspondentes (`filter`, `sort`),
algo que vocẽ quer evitar. Se possível, a especificação dos tipos de campo deve ser feita com
a action `createTypes`.

### Acessando o armazenamento de dados do Gatsby a partir de resolvers de campo

Como mencionado acima, os recursos internos de consulta e armazenamento de dados de Gatsby estão
disponíveis para _resolvers_ de campo customizados no argumento `context.nodeModel` passado
para todos os _resolvers_. Acessar node(s) pelo `id` (e opcionalmente `type`) é possível
com [`getNodeById`](/docs/node-model/#getNodeById) e
[`getNodesByIds`](/docs/node-model/#getNodesByIds). Para obter todos os nodes ou todos os
nodes de um certo tipo, use [`getAllNodes`](/docs/node-model/#getAllNodes).
E executar uma consulta de dentro das funções do _resolver_ pode ser realizada
com [`runQuery`](/docs/node-model/#runQuery), que aceita os argumentos de consulta
`filter` e `sort`.

Você pode, por exemplo, adicionar um campo ao tipo `AuthorJson` que lista todas as
postagens recentes de um autor:

```js:title=gatsby-node.js
exports.createResolvers = ({ createResolvers }) => {
  const resolvers = {
    AuthorJson: {
      recentPosts: {
        type: ["MarkdownRemark"],
        resolve(source, args, context, info) {
          return context.nodeModel.runQuery({
            query: {
              filter: {
                frontmatter: {
                  author: { eq: source.email },
                  date: { gt: "2019-01-01" },
                },
              },
            },
            type: "MarkdownRemark",
            firstOnly: false,
          })
        },
      },
    },
  }
  createResolvers(resolvers)
}
```

Ao usar o `runQuery` para classificar os resultados da consulta, esteja ciente de que ambos `sort.fields`
e `sort.order` são campos `GraphQLList`. Além disso, campos aninhados em `sort.fields`
tem que ser fornecidos em notação de ponto (não separado por sublinhado triplo).
Por exemplo:

```js
context.nodeModel.runQuery({
  query: {
    sort: {
      fields: ["frontmatter.publishedAt"],
      order: ["DESC"],
    },
  },
  type: "MarkdownRemark",
})
```

### Campos de consulta personalizados

Uma abordagem poderosa habilitada pelo `createResolvers` é adicionar campos de consulta raiz
personalizados. Enquanto os campos de consulta raiz padrão adicionados por Gatsby (por exemplo
`markdownRemark` e `allMarkdownRemark`) fornecem toda a gama de opções
de consultas, campos de consulta criados especificamente para o seu projeto podem ser úteis. Por
exemplo, você pode adicionar um campo de consulta para todos os colaboradores externos ao blog de exemplo
que receberam seus presentes:

```js:title=gatsby-node.js
exports.createResolvers = ({ createResolvers }) => {
  const resolvers = {
    Query: {
      contributorsWithSwag: {
        type: ["ContributorJson"],
        resolve(source, args, context, info) {
          return context.nodeModel.runQuery({
            query: {
              filter: {
                receivedSwag: { eq: true },
              },
            },
            type: "ContributorJson",
            firstOnly: false,
          })
        },
      },
    },
  }
  createResolvers(resolvers)
}
```

Porque você também pode estar interessado no reverso - quais colaboradores não
receberam seus presentes ainda - por que não adicionar um argumento de consulta personalizado (obrigatório)?

```js:title=gatsby-node.js
exports.createResolvers = ({ createResolvers }) => {
  const resolvers = {
    Query: {
      contributors: {
        type: ["ContributorJson"],
        args: {
          receivedSwag: "Boolean!",
        },
        resolve(source, args, context, info) {
          return context.nodeModel.runQuery({
            query: {
              filter: {
                receivedSwag: { eq: args.receivedSwag },
              },
            },
            type: "ContributorJson",
            firstOnly: false,
          })
        },
      },
    },
  }
  createResolvers(resolvers)
}
```

Também é possível fornecer tipos de entrada personalizados mais complexos que podem ser definidos
diretamente no SDL. Você poderia, por exemplo, adicionar um campo ao tipo `ContributorJson`
que conta o número de postagens de um colaborador e então adiciona um campo de consulta
raiz personalizado `contributors` que aceita argumentos `min` ou `max` para retornar apenas
colaboradores que escreveram pelo menos `min` ou no máximo `max` postagens:

```js:title=gatsby-node.js
exports.createResolvers = ({ createResolvers }) => {
  const resolvers = {
    Query: {
      contributors: {
        type: ["ContributorJson"],
        args: {
          postsCount: "input PostsCountInput { min: Int, max: Int }",
        },
        resolve(source, args, context, info) {
          const { max, min = 0 } = args.postsCount || {}
          const operator = max != null ? { lte: max } : { gte: min }
          return context.nodeModel.runQuery({
            query: {
              filter: {
                posts: operator,
              },
            },
            type: "ContributorJson",
            firstOnly: false,
          })
        },
      },
    },
    ContributorJson: {
      posts: {
        type: `Int`,
        resolve: (source, args, context, info) => {
          return context.nodeModel
            .getAllNodes({ type: "MarkdownRemark" })
            .filter(post => post.frontmatter.author === source.email).length
        },
      },
    },
  }
  createResolvers(resolvers)
}
```

### Cuidando do hot reloading

Ao criar _resolvers_ de campos personalizados, é importante garantir que o Gatsby
conheça os dados de que uma página depende para que o hot reloading funcione corretamente. Quando
você recebe nodes do armazenamento com métodos [`context.nodeModel`](/docs/node-model/),
geralmente não é necessário fazer nada manualmente, porque o Gatsby registrará
dependências para os resultados da consulta automaticamente. A exceção é `getAllNodes`
que _não_ registrará dependências de dados por padrão. Isso ocorre porque
solicitar a repetição de consultas quando qualquer node de um determinado tipo é alterado é
potencialmente uma operação muito cara. Se você tem certeza de que realmente precisa disso,
você pode adicionar uma dependência de dados da página programaticamente com
[`context.nodeModel.trackPageDependencies`](/docs/node-model/#trackPageDependencies), ou com:

```js
context.nodeModel.getAllNodes(
  { type: "MarkdownRemark" },
  { connectionType: "MarkdownRemark" }
)
```

## Interfaces e Uniões Personalizadas

Por fim, digamos que você queira ter uma página no blog de exemplo que lista todos os
membros do time (autores e colaboradores). O que você pode fazer é ter duas consultas,
uma para `allAuthorJson` e uma para `allContributorJson` e mesclá-las
manualmente. No entanto, o GraphQL fornece uma solução mais elegante para esses tipos de
problemas com "tipos abstratos" (interfaces e uniões). Como autores e
colaboradores na verdade, compartilham a maioria dos campos, você pode abstraí-los em
uma interface `TeamMember` e adicionar um campo de consulta personalizado para todos os membros da equipe
(bem como um _resolver_ personalizado para nomes completos):

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createTypes } = actions
  const typeDefs = `
    interface TeamMember {
      name: String!
      firstName: String!
      email: String!
    }

    type AuthorJson implements Node & TeamMember {
      name: String!
      firstName: String!
      email: String!
      joinedAt: Date
    }

    type ContributorJson implements Node & TeamMember {
      name: String!
      firstName: String!
      email: String!
      receivedSwag: Boolean
    }
  `
  createTypes(typeDefs)
}

exports.createResolvers = ({ createResolvers }) => {
  const fullName = {
    type: "String",
    resolve(source, args, context, info) {
      return source.firstName + " " + source.name
    },
  }
  const resolvers = {
    Query: {
      allTeamMembers: {
        type: ["TeamMember"],
        resolve(source, args, context, info) {
          return context.nodeModel.getAllNodes({ type: "TeamMember" })
        },
      },
    },
    AuthorJson: {
      fullName,
    },
    ContributorJson: {
      fullName,
    },
  }
  createResolvers(resolvers)
}
```

Para usar o campo de consulta raiz recém adicionado em uma consulta de página para obter
os nomes completos de todos os membros da equipe, você pode escrever:

```js
export const query = graphql`
  {
    allTeamMembers {
      ... on AuthorJson {
        fullName
      }
      ... on ContributorJson {
        fullName
      }
    }
  }
`
```

### Interfaces consultáveis ​​com a extensão `@nodeInterface`

Desde o Gatsby 2.13.22, você pode obter o mesmo que foi mencionado acima adicionando a extensão
`@nodeInterface` à interface `TeamMember`. Isso tratará a interface como um tipo de
alto nível normal que implementa a interface `Node`, e, assim, adiciona automaticamente
campos de consulta raiz à interface.

```js:title=gatsby-node.js
exports.createSchemaCustomization = ({ actions }) => {
  const { createTypes } = actions
  const typeDefs = `
    interface TeamMember @nodeInterface {
      id: ID!
      name: String!
      firstName: String!
      email: String!
    }

    type AuthorJson implements Node & TeamMember {
      name: String!
      firstName: String!
      email: String!
      joinedAt: Date
    }

    type ContributorJson implements Node & TeamMember {
      name: String!
      firstName: String!
      email: String!
      receivedSwag: Boolean
    }
  `
  createTypes(typeDefs)
}
```

Ao consultar, use fragmentos embutidos para os campos específicos dos tipos
que implementam a interface (ou seja, campos que não são compartilhados):

```js
export const query = graphql`
  {
    allTeamMember {
      nodes {
        name
        firstName
        email
        __typeName
        ... on AuthorJson {
          joinedAt
        }
        ... on ContributorJson {
          receivedSwag
        }
        ... on Node {
          parent {
            id
          }
        }
      }
    }
  }
`
```

A inclusão do campo de introspecção `__typeName` permite verificar o tipo de node ao
iterar nos resultados da consulta em seu componente:

```js
data.allTeamMember.nodes.map(node => {
  switch (node.__typeName) {
    case `AuthorJson`:
      return <Author {...node} />
    case `ContributorJson`:
      return <Contributor {...node} />
  }
})
```

> Nota: Todos os tipos que implementam uma interface com a extensão `@nodeInterface`
> também devem implementar a interface `Node`.

## Estendendo tipos de terceiros

Até agora, os exemplos têm lidado com tipos criados a partir de dados disponíveis localmente.
No entanto, o Gatsby também permite integrar e modificar schemas GraphQL de terceiros.

Geralmente, esses schemas de terceiros são recuperados de fontes remotas via consulta de
introspecção com o plugin do Gatsby `gatsby-source-graphql`. Para personalizar tipos integrados de
um schema de terceiros, você pode usar a API [`createResolvers`](/docs/node-apis/#createResolvers).

### Alimentando imagens remotas no `gatsby-image`

Como exemplo, você pode olhar para [using-gatsby-source-graphql](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-gatsby-source-graphql/gatsby-node.js) para ver como você poderia usar `createResolvers` para alimentar imagens de um CMS no `gatsby-image` (a suposição é que `gatsby-source-graphql` foi configurado
para prefixar todos os tipos do schema de terceiros com `CMS`):

```js:title=gatsby-node.js
exports.createResolvers = ({
  actions,
  cache,
  createNodeId,
  createResolvers,
  store,
  reporter,
}) => {
  const { createNode } = actions
  createResolvers({
    CMS_Asset: {
      imageFile: {
        type: `File`,
        resolve(source, args, context, info) {
          return createRemoteFileNode({
            url: source.url,
            store,
            cache,
            createNode,
            createNodeId,
            reporter,
          })
        },
      },
    },
  })
}
```

Você cria um novo campo `imageFile` no tipo `CMS_Asset`, o que criará nodes `File`
de todos os valores no campo `url`. Como os nodes `File` têm automaticamente
campos de conveniência `childImageSharp` disponíveis, você pode alimentar as imagens do CMS
no `gatsby-image` simplesmente consultando:

```graphql
query {
  cms {
    post {
      # Neste exemplo, o campo `post.image` é do tipo `CMS_Asset`
      image {
        # É importante incluir todos os campos na consulta que você deseja
        # acessar no resolver. Neste exemplo, certifique-se de incluir
        # o campo `url`. No futuro, Gatsby poderá fornecer uma extensão `@projection`
        # para incluir automaticamente esses campos.
        url
        imageFile {
          childImageSharp {
            fixed {
              ...GatsbyImageSharpFixed
            }
          }
        }
      }
    }
  }
}
```
