---
title: GraphQL API
tableOfContentsDepth: 2
---

import { GraphqlApiQuery } from "../../www/src/components/api-reference/doc-static-queries"
import APIReference from "../../www/src/components/api-reference"

Uma grande vantagem de usar o Gatsby é uma camada de dados embutida que combina todas as fontes de dados que você configura. Os dados são coletados em [tempo de build](/docs/glossary#build) da aplicação e são montados automaticamente em um [schema](/docs/glossary#schema) que define como os dados podem ser consultados no seu site. 

Este documento é uma referência para as características GraphQL inclusas no Gatsby, incorporando métodos para consulta e obtenção de dados, e personalização do GraphQL conforme a necessidade de seu site.

## Começando com GraphQL

GraphQL está disponível no Gatsby sem precisar instalar nada: um schema é automaticamente gerado quando você executa `gatsby develop` ou `gatsby build`. Quando o site compila, esta camada de dados pode ser explorada em: `http://localhost:8000/___graphql`

## Obtendo dados

Os dados precisam ser [fornecidos](/docs/content-and-data/) ou adicionados ao schema GraphQL - para serem consultados e inseridos em páginas usando GraphQL. Gatsby utiliza [plugins nativos](/plugins/?=gatsby-source) para trazer os dados.

**Nota**: O GraphQL não é necesssário, você também pode [utilizar o Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/).

Para obter os dados com um plugin existente você precisa instalar todos os pacotes necessários. 
Além disso, você deve adicionar o plugin no array de plugins no `gatsby-config` com todas as configurações adicionais.
Se você deseja obter dados do sistema de arquivos para usar com o GraphQL, como arquivos de Markdown, imagens e outros, consulte os [documentos para obtenção de dados do sistema de arquivos](/docs/sourcing-from-the-filesystem/) e [receitas](/docs/recipes/sourcing-data).

Para instruções sobre a instalação de plugins usando o npm, olhe a documentalção sobre [a utilização de plugins no seu site](/docs/using-a-plugin-in-your-site/).

Você também pode [criar plugins personalizados](/docs/creating-plugins/) para ajustar-se aos seus próprios casos de uso e extrair dados da maneira que desejar.

## Consultando componentes e hooks

Dados podem ser consultados dentro de páginas, ou do arquivo `gatsby-node.js` utilizando uma das seguintes opções:

- O componente `pageQuery`
- O componente `StaticQuery`
- O hook `useStaticQuery`

**Nota**: Devido à forma de como o Gatsby processa as consultas GraphQL, você não pode misturar consultas de página e consultas estáticas no mesmo arquivo. Você também não pode ter mais de uma consulta de página ou consulta estática por arquivo.

Para obter informações sobre componentes de página e componentes que não são de página e quanto às suas consultas, consulte o guia sobre [construindo com componentes](/docs/building-with-components/#how-does-gatsby-use-react-components).

### `pageQuery`

`pageQuery` é um componente interno que recupera informações da camada de dados nas páginas do Gatsby. Você pode ter somente uma consulta de página por página. Este componente pode ter argumentos do GraphQL para variáveis ​​em suas consultas.

Uma [página é criada no Gatsby](/docs/page-creation/) por qualquer componente React que esteja na pasta `src/pages`, ou chamando a ação `createPage`, usando um componente nas opções `createPage` -- isto significa que um `pageQuery` não funcionará em componente algum, somente nos componentes que atendem a esse critério.

Além disso, consulte o [guia sobre consulta de dados em páginas com consulta](/docs/page-query/).

#### Parâmetros

Uma consulta de página não é um método, é mais como uma variável exportada que recebe uma string chamada `graphql` e uma consulta válida como seu valor:

```javascript
export const pageQuery = graphql`
  query HomePageQuery {
    site {
      siteMetadata {
        description
      }
    }
  }
`
```

**Nota**: A consulta exportada em um `const` não precisa ser chamada de` pageQuery`. Na verdade, o Gatsby procura uma string `graphql` exportada do arquivo.

#### Returnos

Quando inclusa em um arquivo de componente da página, uma consulta de página retorna um objeto de dados que é passado automaticamente para o componente como uma propriedades.

```jsx
// highlight-start
const HomePage = ({ data }) => {
  // highlight-end
  return (
    <div>
      Hello!
      {data.site.siteMetadata.description} // highlight-line
    </div>
  )
}
```

### `StaticQuery`

StaticQuery é um componente interno para recuperar dados da camada de dados do Gatsby em componentes que não são de página, como um cabeçalho, navegação ou qualquer outro componente filho.

Você pode ter apenas um `StaticQuery` por página: para incluir os dados de fontes diferentes, você pode usar uma consulta com vários [campos raiz](/docs/graphql-concepts/#query-fields). Não é possível aceitar variáveis ​​como argumentos.

Ademais, consulte o [guia sobre consulta de dados em componentes com consulta estática](/docs/static-query/).

#### Parâmetros

O componente `StaticQuery` necessita de duas propriedades em JSX:

- `query`: uma string de consulta `graphql`
- `render`: um componente com acesso aos dados retornados

```jsx
<StaticQuery
  query={graphql` //highlight-line
    query HeadingQuery {
      site {
        siteMetadata {
          title
        }
      }
    }
  `}
  render={(
    data //highlight-line
  ) => (
    <header>
      <h1>{data.site.siteMetadata.title}</h1>
    </header>
  )}
/>
```

#### Returnos

O componente StaticQuery returna `data` em uma proriedade `render`:

```jsx
<StaticQuery
  // ...
  // highlight-start
  render={data => (
    <header>
      <h1>{data.site.siteMetadata.title}</h1>
    </header>
  )}
  // highlight-end
/>
```

### `useStaticQuery`

O hook `useStaticQuery` pode ser usado semelhantemente ao `StaticQuery` em qualquer componente ou página, mas não requer um componente e nem uma propriedade render.

Por ser um hook do React, as [regras dos hooks](https://reactjs.org/docs/hooks-rules.html) se aplicam e você precisará usá-las com o React e o ReactDOM versão 16.8.0 ou posterior. Devido à forma de como as consultas atualmente funcionam no Gatsby, apenas uma instância do `useStaticQuery` é suportada em cada arquivo.

Refira-se ao [guia sobre consulta de dados em componentes com useStaticQuery](/docs/use-static-query/) para saber mais.

#### Parâmetros

O hook `useStaticQuery` utiliza um argumento:

- `query`: uma string de consulta `graphql`

```javascript
const data = useStaticQuery(graphql`
  query HeaderQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`)
```

#### Returnos

O hook `useStaticQuery` retorna os dados em um objeto:

```jsx
const data = useStaticQuery(graphql`
  query HeaderQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`)
return (
  // highlight-start
  <header>
    <h1>{data.site.siteMetadata.title}</h1>
  </header>
  // highlight-end
)
```

## Estrutura de Consulta


Consultas são escritas no mesmo formato que você quer que os dados sejam retornados. Os dados de origem determinarão os nomes dos campos nos quais você pode consultar, com base nos nós que eles adicionam ao esquema do GraphQL.

Para compreender mais sobre as partes de uma consulta, considere ler o [guia conceitual](/docs/graphql-concepts/#understanding-the-parts-of-a-query).

### Argumentos de uma consulta em GraphQL

Consultas em GraphQL podem ter argumentos para alterar como os dados serão retornados. A lógica para estes argumentos é internamente tratada pelo Gatsby. Os argumentos podem ser passados nos campos em qualquer nível de consulta.

Diferentes nós podem usar diferentes argumentos baseados na natureza do nó.

Os argumentos que você pode passar para coleções (como arrays ou longas listas de dados - por exemplo, `allFile` ou` allMdx`) são:

- [`filter`](/docs/graphql-reference#filter)
- [`limit`](/docs/graphql-reference#limit)
- [`sort`](/docs/graphql-reference#sort)
- [`skip`](/docs/graphql-reference#skip)

Os argumentos que você pode passar para um campo `date` são:

- [`formatString`](/docs/graphql-reference#dates)
- [`locale`](/docs/graphql-reference#dates)

Os argumentos que você pode transmitir para um campo `excerpt` são:

- [`pruneLength`](/docs/graphql-reference#excerpt)
- [`truncate`](/docs/graphql-reference#excerpt)

### Operações de consulta em Graphql

Outras configurações internas podem ser usadas em consultas:

- [`Alias`](/docs/graphql-reference#alias)
- [`Group`](/docs/graphql-reference#group)

Para exemplos, consulte o guia de [consulta de receitas](/docs/recipes/querying-data) e [Guia de referência das opções de consulta do GraphQL](/docs/graphql-reference/).

## Fragmentos de Query

Os fragmentos permitem reutilizar partes das consultas do GraphQL. Eles também permitem que você divida consultas complexas em componentes menores e mais fáceis de entender.

Para mais informações, consulte o guia de documentos sobre [usando fragmentos no Gatsby](/docs/using-graphql-fragments/).

### Lista de fragmentos no Gatsby

Alguns fragmentos são inclusos nos plugins do Gatsby, como fragmentos para retornar dados de imagem otimizados em vários formatos com `gatsby-image` e` gatsby-transformer-sharp` ou fragmentos de dados com `gatsby-source-contentful`.

#### Fragments do Image Sharp 

Os seguintes fragmentos estão disponíveis em qualquer site com o `gatsby-transformer-sharp` instalado e incluso no seu ` gatsby-config.js`.

As informações sobre consultas com esses fragmentos também são listadas em profundidade nos [documentos da API de imagem do Gatsby](/docs/gatsby-image/), incluindo opções como redimensionar e recolorir.

<GraphqlApiQuery>
  {data => (
    <APIReference
      relativeFilePath={data.transformerSharp.nodes[0].relativePath}
      docs={data.transformerSharp.nodes[0].childrenDocumentationJs}
    />
  )}
</GraphqlApiQuery>

#### Fragmentos de Contentful

Os seguintes fragmentos estão disponíveis em qualquer site com o `gatsby-source-contentful` instalado e incluído no seu` gatsby-config.js`. Esses fragmentos geralmente refletem os outros fragmentos descritos no pacote `gatsby-transformador-sharp`.

<GraphqlApiQuery>
  {data => (
    <APIReference
      relativeFilePath={data.contentfulFragments.nodes[0].relativePath}
      docs={data.contentfulFragments.nodes[0].childrenDocumentationJs}
    />
  )}
</GraphqlApiQuery>

**Nota**: Os fragmentos acima são de projetos starters de Gatsby mantidos oficialmente; outros plugins como `gatsby-source-datocms` e` gatsby-source-sanity` utilizam fragmentos próprios. Uma lista desses fragmentos pode ser encontrada em [`gatsby-image` README](/packages/gatsby-image#fragments).

## Personalização avançada

Você pode personalizar os dados originados na camada GraphQL e criar relacionamentos entre os nós com as [APIs do Node do Gatsby](/docs/node-apis/).

O esquema do GraphQL pode ser personalizado para casos de uso mais avançados: leia mais sobre isso nos [documentos da API de personalização de esquemas](/docs/schema-customization/).
