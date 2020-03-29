---
title: Build Cache
---

Plugins podem armazenar dados em cache como objetos JSON e recuperá-los em builds consecutivas.

Armazenamento em Cache já é usado pelo Gatsby e plugins, por exemplo:

- qualquer nó criado por plugin nativo/transformador é armazenado em cache.
- o `gatsby-plugin-sharp` armazena em cache as miniaturas construidas.

Os dados são armazenados no diretório `.cache` na raíz do seu projeto.

## A API de cache

A API de cache é passada para [APIs de Nó do Gatsby](/docs/node-apis/) que é tipicamente implementada por plugins.

```js
exports.onPostBootstrap = async function({ cache, store, graphql }) {}
```

As duas funções que você pode utilizar são:

### `set`

Armazena Valor no cache

`cache.set(key: string, value: any) => Promise<any>`

### `get`

Devolve o valor do cache

`cache.get(key: string) => Promise<any>`

A documentação [Node API helpers](/docs/node-api-helpers/#cache) oferece informações mais detalhadas sobre a API.

## Exemplo de plugin

No seu arquivo de plugin `gatsby-node.js`, você pode acessar o argumento `cache` dessa maneira:

```js:title=gatsby-node.js
exports.onPostBuild = async function({ cache, store, graphql }, { query }) {
  const cacheKey = "some-key-name"
  let obj = await cache.get(cacheKey)

  if (!obj) {
    obj = { created: Date.now() }
    const data = await graphql(query)
    obj.data = data
  } else if (Date.now() > obj.lastChecked + 3600000) {
    /* Recarrega depois de um dia */
    const data = await graphql(query)
    obj.data = data
  }

  obj.lastChecked = Date.now()

  await cache.set(cacheKey, obj)

  /* Faz algo com os dados ... */
}
```

## Limpando o cache

Assumindo que os arquivos de cache são armazenados no diretório `.cache`, simplesmente deletando essa pasta irá limpar toda a cache. Você também pode usar o [`gatsby clean`](/docs/gatsby-cli/#clean) para deletar os diretórios `.cache` e `public`.

O cache também é invalidado pelo Gatsby em alguns casos, especificamente:

- Se há mudanças no arquivo `package.json`, no caso de adicionar ou atualizar uma dependência 
- Se há mudanças no arquivo `gatsby-config.js`, por exemplo se um plugin foi adicionado ou modificado
- Se há mudanças no arquivo `gatsby-node.js`, no caso se você invocar uma nova API de nó, ou alterar uma chamada `createPage`

## Conclusão

Com a API de cache você poderá manter dados entre builds, o que ajuda bastante enquanto você desenvolve um site com Gatsby (a medida que você executa varias vezes `gatsby develop`). Operações pesadas de desempenho (como transformações de imagem) ou download de dados podem diminuir a velocidade de inicialização do Gatsby significativamente e adicionar essa otimização ao seu plugin pode ser uma grande melhoria para seus usuários finais. Você também pode dar uma olhada nos seguintes exemplos que implementaram a API de cache: [gatsby-source-contentful](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-source-contentful/src/download-contentful-assets.js), [gatsby-source-shopify](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-source-shopify/src/nodes.js#L23-L54), [gatsby-source-wordpress](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-source-wordpress/src/normalize.js#L471-L537), [gatsby-transformer-remark](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-transformer-remark/src/extend-node-type.js), [gatsby-source-tmdb](https://github.com/LekoArts/gatsby-source-tmdb/blob/e12c19af5e7053bfb7737e072db9e24acfa77f49/src/add-local-image.js).
