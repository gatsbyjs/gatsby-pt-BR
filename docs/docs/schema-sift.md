---
title: Consultas com Sift
---

> Este documento não está atualizado de acordo a última versão do Gatsby.
>
> Os recursos de [personalização do esquema](/docs/schema-customization) and [materialização do node](https://github.com/gatsbyjs/gatsby/pull/16091) fizeram alterações nessa parte do Gatsby.
>
> Você pode ajudar fazendo Pull Request para [atualizar esta documentação](https://github.com/gatsbyjs/gatsby/issues/14228).

## Sumário

Gatsby armazena todos os dados carregados durante a fase dos nós de origem no Redux. E isso permite que você escreva consultas GraphQL para consultar esses dados. Mas o Redux é um simples armazenamento de objetos JavaScript. Então, como o Gatsby consulta esses nós usando a linguagem de consulta GraphQL?

A resposta é que ele usa a biblioteca [sift.js](https://github.com/crcn/sift.js/tree/master). Abstraindo a linguagem de consulta do MongoDB para funcionar sobre objetos JavaScript. Pois a linguagem de consulta do MongoDB é muito compatível com o GraphQL.

A maior parte da lógica abaixo está no arquivo [run-sift.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/redux/run-sift.js), chamado a partir da função [ProcessedNodeType `resolve()`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/schema/build-node-types.js#L191).

## Função ProcessedNodeType Resolve 

Lembrando que, no momento no qual esta função de resolução é criado, iteramos por todos os `node.internal.type` distindos no namespace `nodes` do redux. Por exemplo, podemos estar no tipo `MarkdownRemark`. Portanto, a função `resolve()` fecha sobre esse tipo e tem acesso a todos os nós desse tipo.

A função `resolve()` chama `run-sift.js`, e fornece os seguintes argumentos:


- GraphQLArgs (como um objeto JavaScript). Dentro de um filtro. Por exemplo, `wordcount: { paragraphs: { eq: 4 } }`
- Todos os nodes em redux deste tipo. Por exemplo, onde `internal.type == MmarkdownRemark'`

- Contexto `path`, se está sendo chamado como parte de uma [page query](/docs/query-execution/#query-queue-execution). Por exemplo, `markdownRemark`
- gqlType. Veja mais em [more on gqlType](/docs/schema-gql-type)

Por exemplo:

```javascript
runSift({
  args: {
    filter: { // Exact args from GraphQL Query
      wordcount: {
        paragraphs: {
          eq: 4
        }
      }
    }
  },
  nodes: ${latestNodes},
  path: context.path, // E.g. /blogs/my-blog
  typeName: `markdownRemark`,
  type: ${gqlType}
})
```

## Run-sift.js

Os arquivos convertem Argumentos GraphQL em consultas sift e aplica na coleção de todos os nodes deste tipo. Os passos são:

1. Converter os argumentos da consulta para argumentos sift
1. Soltar folhas de argumentos
1. Resolver campos internos de consulta em todos os nodes
1. Rastrear campos recém criados
1. Executar consultas sift em todos os nodes
1. Criar dependências das páginas se necessário


### 1. Converter os argumentos da consulta para argumentos sift

Sift espera que todos os nomes dos campos sejam anexados por um `$`. A função [siftifyArgs](https://github.com/gatsbyjs/gatsby/blob/6dc8a14f8efc78425b1f225901dce7264001e962/packages/gatsby/src/redux/run-sift.js#L39) resolve isso. Eles percorrem a árvore de argumentos, executando as seguintes transformações para cada campo chave/valor do cenário.

- Se a chave do campo é `elmMatch`? Troque para `$elemMatch`. Recursivamente nos valores do objeto
- Se o valor do campo é uma regex? Aplique o limpador de regex
- Se o valor do campo é glob, use a biblioteca [minimatch](https://www.npmjs.com/package/minimatch) para converter em regex
- Se for um valor normal, acrescente `$` ao nome do campo.

Então a consulta acima se tornará:

```javascript
{
  `$wordcount`: {
    `$paragraphs`: {
      `$eq`: 4
    }
  }
}
```

### 2. Solte as folhas (e.g. `{eq: 4}`) dos argumentos

Para auxiliar na etapa 3, criamos uma versão dos argumentos siftificados chamada `fieldsToSift` isso faz com que todas as folhas da árvore de argumentos sejam trocadas por um valor booleano `true`. Isto é tratado pela função [extractFieldsToSift](https://github.com/gatsbyjs/gatsby/blob/6dc8a14f8efc78425b1f225901dce7264001e962/packages/gatsby/src/redux/run-sift.js#L65). `fieldsToSift` ficará assim depois que a função for aplicada

```javascript
{
  `wordcount`: {
    `paragraphs`: true
  }
}
```

### 3. Resolver campos internos de consulta em todos os nodes

A etapa 4 executará a consulta sift por todos os nodes, retornando o primeiro que corresponderá a consulta. Mas nos devemos lembrar que os nodes que estão apenas no redux incluem dados que foram criados explicitamente por seus plugins de origem ou de transformação. Se ao invés de criar um campo de dados, um plugin usou `setFieldsOnGraphQLNodeType` para definir um campo personalizado, então temos que manualmente chamar os resolvedores de campo para cada node. Os argumentos na etapa 2 são um ótimo exemplo. O campo wordcount é definido pelo plugin [gatsby-transformer-remark](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-transformer-remark/src/extend-node-type.js#L416), ao invés de ser criado durante a criação do node de observação.

A função [nodesPromise](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/redux/run-sift.js#L168) itera para todos os nós deste tipo. Então, para cada node, [resolveRecursive](https://github.com/gatsbyjs/gatsby/blob/6dc8a14f8efc78425b1f225901dce7264001e962/packages/gatsby/src/redux/run-sift.js#L135) desce percorrendo a árvore `siftToFields`, obtendo o nome do campo, e depois achando seu gqlType, e então chamando a função `resolve` para tipos manualmente. Pegando o exemplo acima, nós podemos achar o gqlField para seu `wordcount` e então chamar seu campo de resolução.


```javascript
markdownRemarkGqlType.resolve(node, {}, {}, { fieldName: `wordcount` })
```
Note que a biblioteca do graphql-js NÃO foi chamada ainda. Ao invés disso, nós estamos chamando a função de resolução apropriada gqlType manualmente.

O método de resolução neste caso irá retornar um node parágrafo, o qual também precisa ser resolvido adequadamente. Então descemos na árvore de argumento do `fieldsToSift` e realizamos a operação acima no node parágrafo(usando o parágrafo encontrado gqlType).

Após a conclusão do `resolvRecursive`, teremos "realizado" todos os campos da consulta em cada nó, dando-nos a confiança de que podemos executar a consulta com todos os dados.


### 4. Rastrear campos recém criados

Como novos campos no nó podem ter sido criados nesse processo, chamamos `trackInlineObjectsInRootNode()` para rastrear esses novos objetos. Consulte a documentação do [Node Tracking](/docs/node-tracking/) para obter mais informações.

### 5. Executar consultas sift em todos os nodes
Agora que percebemos todos os campos que precisam ser consultados, em todos os nós desse tipo, estamos finalmente prontos para aplicar a consulta sift. Esta etapa é tratada pelo [tempPromise](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/redux/run-sift.js#L214). E ele simplesmente concatena todos os objetos de nível superior na árvore de argumentos, junto com uma expressão sift `$and` e então itera por todos os nodes retornando o primeiro que satisfaz a expressão sift.

No caso em que `connection === true` (argumento passado pelo run-sift), então ao invés de apenas escolher o primeiro argumento, nós vamos selecionar TODOS os nodes que combinam com a consulta sift. Se a consulta GraphQL especificar os campos `sort`, `skip` ou `limit`, então nós usamos a biblioteca graphql-skip-limit](https://www.npmjs.com/package/graphql-skip-limit) para filtrar os resultados apropriados. Veja [Schema Connections](/docs/schema-connections) para mais informações.

### 6. Criar dependências das páginas se necessário

Supondo que encontramos um nó (ou vários, se a `connection` === true), finalizamos gravando a página que iniciou a consulta (no campo `path`) dependendo do nó encontrado. Mais sobre isso em [Page -> Node Dependencies](/docs/page-node-dependencies/).

## Nota sobre os efeitos colaterais do resolvedor de plugins

Como [mencionado acima](#3-resolver-campos-internos-de-consulta-em-todos-os-nodes), `run-sift` deve “realizar” todos os campos de consulta antes de consultar através deles. Isto envolve chamar os resolvedores personalizados **em cada node daquele tipo**. Portanto, se um _resolver_ retornar um efeito colateral, eles serão acionados, independentemente de o resultado do campo realmente corresponder à consulta.
