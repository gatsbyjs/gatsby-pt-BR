---
title: Adicionando pesquisa
overview: true
---

Veja abaixo uma lista de guias nessa sessão, ou continue lendo para uma visão geral sobre como adicionar a funcionalidade de pesquisa no seu _site_.
<GuideList slug={props.slug} />

## Visão geral de busca no _site_

Antes de seguirmos com as etapas para adicionar pesquisa no seu _website_ Gatsby, vamos examinar os componentes necessários para adicionar pesquisa a um _website_.

São necessários três componentes para adicionar pesquisa ao seu _website_ Gatsby:

1. Índice
2. Motor
3. UI

## Componentes de pesquisa do _site_

### Índice de pesquisa

O índice de pesquisa é uma cópia de seus dados armazenados em um formato amigável para busca. Um índice serve para otimizar a velocidade e o desempenho ao executar uma consulta de pesquisa. Sem um índice, cada pesquisa teria que escanear todas as páginas no seu _site_, o que se torna rapidamente ineficiente.

### Motor de busca

O motor de busca realiza uma consulta de pesquisa, executa-a através do índice de pesquisa e retorna quaisquer documentos correspondentes.

### UI de busca

O componente de UI provê uma interface ao usuário, no que permite a eles escreverem consultas de pesquisa e ver os resultados de cada consulta.

## Adicionando pesquisa ao seu _site_

Agora que você sabe sobre os três componentes requisitados, existem algumas maneiras de abordar busca no seu _site_ alimentado pelo Gatsby.

### Use um motor de busca _open source_

Usar um mecanismo de busca _open source_ é sempre grátis e permite que você ative pesquisa _offline_ para o seu _site_. Observe que você precisa ter cuidado com a pesquisa _offline_, porque todo o índice de pesquisa precisa ser trazido para o cliente, o que pode afetar significativamente o tamanho do pacote.

Bibliotecas _open source_ como [`elasticlunr`](https://www.npmjs.com/package/elasticlunr),[`flexsearch`](https://github.com/nextapps-de/flexsearch) ou [`js-search`](https://github.com/bvaughn/js-search) podem ser utilizadas para possibilitar pesquisa para o seu _site_.

Isso exigirá que você crie um índice de busca quando o seu _site_ for construído. Para [`elasticlunr`](https://www.npmjs.com/package/elasticlunr), existe um _plugin_ chamado [`gatsby-plugin-elasticlunr-search`](https://github.com/gatsby-contrib/gatsby-plugin-elasticlunr-search) que cria um índice de pesquisa automaticamente. Para [`flexsearch`](https://github.com/nextapps-de/flexsearch) existe um plugin chamado [`gatsby-plugin-flexsearch`](https://github.com/tmsss/gatsby-plugin-flexsearch).

Para outras bibliotecas, você pode utilizar a combinação de [`onCreateNode`](/docs/node-apis/#onCreateNode), [`setFieldsOnGraphQLNodeType`](/docs/node-apis/#setFieldsOnGraphQLNodeType) e [`sourceNodes`](/docs/node-apis/#sourceNodes)  da API do Gatsby node para criar o índice de pesquisa e disponibilizá-lo no GraphQL. Para mais informação em como fazer isso, confira [o código fonte do `gatsby-plugin-elasticlunr-search`'s](https://github.com/gatsby-contrib/gatsby-plugin-elasticlunr-search/blob/master/src/gatsby-node.js#L96-L131).

Outra opção é gerar o índice de pesquisa no final da construção, utilizando o [`onPostBuild`](/docs/node-apis/#onPostBuild) da API node. Essa abordagem é utilizada pelo [`gatsby-plugin-lunr`](https://github.com/humanseelabs/gatsby-plugin-lunr) para construir índices multi-idiomas.

Depois de construír o índice de busca e inclui-lo na camada de dados do Gatsby, você vai precisar permitir o usuário a pesquisar o seu _website_. Isso geralmente é feito utilizando uma entrada de texto para capturar a consulta de busca e, em seguida, usando uma das bibliotecas mencionadas acima para recuperar o(s) documento(s) desejado(s).

### Use um motor de busca baseado em API

Outra opção é utilizar um motor de busca externo. Essa solução é muito mais escalável, pois visitantes do seu _site_ não precisam baixar todo o seu índice de pesquisa (que poderá se tornar enorme a medida que o _site_ cresce) para pesquisar no seu _site_. A desvantagem é que você precisará pagar para hospedar o mecanismo de busca ou pagar por um serviço de pesquisa comercial.

Existem várias opções disponíveis, sejam as de código aberto onde você mesmo pode hospedar ou então opções de hospedagem comercial.

- [ElasticSearch](https://www.elastic.co/products/elasticsearch) — OSS e tem hospedagem comercial disponível
- [Solr](http://lucene.apache.org/solr/) — OSS e tem hospedagem comercial disponível
- [Algolia](https://www.algolia.com/) — Comercial

Se você está construíndo um _website_ de documentação, pode usar a [funcionalidade DocSearch do Algolia](https://community.algolia.com/docsearch/). Ele criará automaticamente um índice de pesquisa a partir do conteúdo de suas páginas.

Se seu _website_ não se qualifica como documentação, você precisa coletar o índice de pesquisa no momento da criação e enviá-lo usando [`gatsby-plugin-algolia`](https://github.com/algolia/gatsby-plugin-algolia).

Ao usar o Algolia, eles hospedam o índice de pesquisa e o motor de busca para você. Suas consultas de pesquisa serão enviadas aos seus servidores que responderão com quaisquer resultados. Você vai precisar implementar sua própria UI; Algolia provê uma [biblioteca React](https://github.com/algolia/react-instantsearch) que pode dispor componentes que você gostaria de usar.

Elasticsearch possui diversas bibliotecas de componentes React para pesquisa, por exemplo https://github.com/appbaseio/reactivesearch