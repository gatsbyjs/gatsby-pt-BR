---
title: "Receitas: Requisitando dados"
tableOfContentsDepth: 1
---

O Gatsby permite que você acesse seus dados em todas as origens usando uma única interface em GraphQL.

## Requisitando dados com uma requisição de página

Você pode usar a tag `graphql` para requisitar dados nas páginas do seu site. Isso lhe dá acesso a tudo que esta incluso na camada de dados do Gatsby, tais quais os metadados do site, [plugins de origem](/tutorial/part-five), imagens e mais.

### Instruções

1. Importe `graphql` de `gatsby`.

2. Exporte uma constante chamada `query` e defina seu valor tal qual um template `graphql` com a requisição entre duas crases.

3. Passe uma prop para o componente chamada `data`.

4. A variável `data` contém os dados requisitados e pode ser referenciada em JSX para gerar HTML.

```jsx:title=src/pages/index.js
import React from "react"
// highlight-next-line
import { graphql } from "gatsby"

import Layout from "../components/layout"

// highlight-start
export const query = graphql`
  query PaginaInicialQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end

// highlight-next-line
const PaginaIndex = ({ data }) => (
  <Layout>
    // highlight-next-line
    <h1>{data.site.siteMetadata.title}</h1>
  </Layout>
)

export default PaginaIndex
```

### Recursos adicionais

- [GraphQL e Gatsby](/docs/graphql/): compreendendo a estrutura esperada dos seus dados
- [Mais sobre como requisitar dados em páginas com GraphQL](/docs/page-query/)
- [Documentação de Tagged Template Literals no MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals), que nem os usados em GraphQL

## Requisitando dados com o componente StaticQuery

`StaticQuery` é um componente para buscar dados da camada de dados de Gatsby em [componentes que não representam páginas](/docs/static-query/), tal qual um cabeçalho, navegação ou qualquer outro componente filho.

### Instruções

1. O componente `StaticQuery` pede duas propriedades de renderização: `query` e `render`.

```jsx:title=src/components/ComponenteFilho.js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const ComponenteFilho = () => (
  <StaticQuery
    query={graphql` // highlight-line
      query ComponenteFilhoReq {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={(
      data // highlight-line
    ) => (
      <h1>
        requisição do o título de ComponenteFilho com StaticQuery:
        {data.site.siteMetadata.title}
      </h1>
    )}
  />
)

export default ComponenteFilho
```

2. Agora você pode usar esse componente como faria com [qualquer outro](/docs/building-with-components#non-page-components), importando-o para uma página composta por outros componentes JSX e marcação HTML.

## Requisitado dados com o hook useStaticQuery

Desde a v2.1.0 do Gatsby, você pode usar o hook `useStaticQuery` para requisitar dados com uma função JavaScript ao invés de usar um componente exclusivo para os dados. A sintaxe do hook elimina a necessidade de um componente `<StaticQuery>` para encapsular tudo, simplificando a forma de escrever para algumas pessoas.

O hook `useStaticQuery` pega uma requisição GraphQL e retorna os dados solicitados. Ele pode ser armazenado em uma variável e usado posteriormente em seus templates JSX.

### Pré-requisitos

- Você precisará do React e do ReactDOM 16.8.0 ou posterior (manter o Gatsby atualizado garate disso)
- Leitura recomendada: as [Regras dos Hooks em React](https://reactjs.org/docs/hooks-rules.html)

### Instruções

1. Importe `useStaticQuery` e `graphql` de `gatsby` para usar a requisição de hook para pegar os dados.

2. No início de um componente funcional sem estado, atribua uma variável ao valor de `useStaticQuery` com a requisição `graphql` passada como um argumento.

3. No código JSX retornado de seu componente, você pode referenciar essa variável para lidar com os dados retornados.

```jsx:title=src/components/ComponenteFilho.js
import React from "react"
import { useStaticQuery, graphql } from "gatsby" //highlight-line

const ComponenteFilho = () => {
  // highlight-start
  const data = useStaticQuery(graphql`
    query ComponenteFilhoReq {
      site {
        siteMetadata {
          title
        }
      }
    }
  `)
  // highlight-end
  return (
    <h1>
      Requisição do título de ComponenteFilho: {data.site.siteMetadata.title}{" "}
      //highlight-line
    </h1>
  )
}

export default ComponenteFilho
```

### Recursos adicionais

- [Mais sobre Static Query para requisitar dados em componentes](/docs/static-query/)
- [A diferença entre uma requisição estática e uma requisição de página](/docs/static-query/#how-staticquery-differs-from-page-query)
- [Mais sobre o hook useStaticQuery](/docs/use-static-query/)
- [Visualize seus dados com GraphiQL](/docs/introducing-graphiql/)

## Limitando com GraphQL

Ao requisitar dados com GraphQL, você pode limitar o número de resultados retornados com um valor específico. Isso é útil caso você precise só de alguns dados ou se precisar [paginar os dados](/docs/add-pagination/).

Para limitar os dados, você precisará de um site com alguns nós na camada de dados GraphQL. Todos os sites têm alguns nós como `allSitePage` e `sitePage` criados automaticamente: mais podem ser adicionados instalando plugins de origem como `gatsby-source-filesystem` em `gatsby-config.js`.

### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)

### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra uma guia em seu navegador em: `http://localhost:8000/___graphql`.
3. Adicione uma requisição no editor com os seguintes campos em `allSitePage` para começar:

```graphql
{
  allSitePage {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

4. Adicione um argumento `limit` ao campo `allSitePage` e dê a ele um valor inteiro `3`.

```graphql
{
  allSitePage(limit: 3) { // highlight-line
    edges {
      node {
        id
        path
      }
    }
  }
}
```

5. Clique no botão reproduzir no GraphiQL e os dados no campo `edges` serão limitados ao número especificado.

### Recursos adicionais

- Saiba mais sobre [nós na API de dados GraphQL de Gatsby](/docs/node-interface/)
- [Referência Gatsby GraphQL para limite de dados](/docs/graphql-reference/#limit)
- Exemplo ao vivo:

<iframe
  title="Limitando dados retornados"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(limit%3A%203)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

## Ordenação com GraphQL

A ordem de seus resultados pode ser especificada através do argumento `sort` no GraphQL. Você pode especificar quais campos classificar e a ordem de classificação.

Para esta receita, você precisará de um site Gatsby com uma coleção de nós para classificar na camada de dados GraphQL. Todos os sites têm alguns nós como `allSitePage` criados automaticamente: mais podem ser adicionados instalando plugins de origem.

### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Campos requisitáveis prefixados com `all`, por exemplo `allSitePage`

### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o GraphiQL em uma guia do navegador em: `http://localhost:8000/___graphql`
3. Adicione uma requisição no editor com os seguintes campos em `allSitePage` para começar:

```graphql
{
  allSitePage {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

4. Adicione um argumento `sort` ao campo`allSitePage` e dê a ele um objeto com os atributos `fields` e `order`. O valor para `fields` pode ser um campo ou uma matriz de campos para classificar (este exemplo usa o campo`path`), a `ordem` pode ser`ASC` ou `DESC` para ascendente e descendente respectivamente.

```graphql
{
  allSitePage(sort: {fields: path, order: ASC}) { // highlight-line
    edges {
      node {
        id
        path
      }
    }
  }
}

```

5. Clique no botão play na página GraphiQL e os dados retornados serão classificados em ordem crescente pelo campo `path`.

### Recursos adicionais

- [Referência Gatsby GraphQL para ordenação](/docs/graphql-reference/#sort)
- Saiba mais sobre [nós na API de dados GraphQL de Gatsby](/docs/node-interface/)
- Exemplo ao vivo:

<iframe
   title = "Ordenando dados"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(sort%3A%20%7Bfields%3A%20path%2C%20order%3A%20ASC%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

## Filtrando com GraphQL

Os resultados requisitados podem ser filtrados com operadores como `eq` (igual), `ne` (não igual), `in` e `regex` em campos especificados.

Para esta receita, você precisará de um site Gatsby com uma coleção de nós para filtrar na camada de dados GraphQL. Todos os sites têm alguns nós como `allSitePage` criados automaticamente: mais podem ser adicionados instalando plugins de fonte e transformador como `gatsby-source-filesystem` e `gatsby-transformer-mark` em `gatsby-config.js` para produzir `allMarkdownRemark`.

### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Campos consultáveis prefixados com `all`, por exemplo `allSitePage` ou `allMarkdownRemark`

### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o GraphiQL em uma guia do navegador em: `http://localhost:8000/___graphql`
3. Adicione uma requisição no editor usando um campo prefixado por 'all', como `allMarkdownRemark` (o que significa que retornará uma lista de nós)

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          title
          categories
        }
      }
    }
  }
}
```

4. Adicione um argumento `filter` (filtro) ao campo `allMarkdownRemark` e dê a ele um objeto com os campos que você deseja filtrar. Neste exemplo, o conteúdo Markdown é filtrado pelo atributo `categories` nos metadados do frontmatter. O próximo valor é o operador: neste caso, `eq` (igual) com um valor de 'criaturas mágicas'.

```graphql
{
  allMarkdownRemark(filter: {frontmatter: {categories: {eq: "magical creatures"}}}) { // highlight-line
    edges {
      node {
        frontmatter {
          title
          categories
        }
      }
    }
  }
}
```

5. Clique no botão de reprodução na página GraphiQL. Os dados que correspondem aos parâmetros do filtro devem ser retornados, neste caso, apenas arquivos Markdown de origem marcados com uma categoria de 'criaturas mágicas'.

### Recursos adicionais

- [Referência Gatsby GraphQL para filtragem](/docs/graphql-reference/#filter)
- [Lista completa de operadores possíveis](/docs/graphql-reference/#complete-list-of-possible-operators)
- Saiba mais sobre [nós na API de dados GraphQL de Gatsby](/docs/node-interface/)
- Exemplo ao vivo:

<iframe
  title="Filtrando dados"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allMarkdownRemark(filter%3A%20%7Bfrontmatter%3A%20%7Bcategories%3A%20%7Beq%3A%20%22magical%20creatures%22%7D%7D%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20categories%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

## Alias de Requisição GraphQL

Você pode renomear qualquer campo em uma requisição GraphQL com um alias.

Se você deseja executar duas requisiçãos na mesma fonte de dados, pode usar um alias para evitar uma colisão de nomes com duas requisiçãos com o mesmo nome.

### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o GraphiQL explorer em uma guia do navegador em: `http://localhost:8000/___graphql`
3. Adicione uma requisição no editor usando dois campos com o mesmo nome como `allFile`.

```graphql
{
  allFile {
    totalCount
  }
  allFile {
    pageInfo {
      currentPage
    }
  }
}
```

4. Adicione o nome que deseja usar para qualquer campo antes do nome do campo em seu esquema GraphQL, separado por dois pontos. (Por exemplo, `[alias-name]: [original-name]`)

```graphql
{
  fileCount: allFile { // highlight-line
    totalCount
  }
  filePageInfo: allFile { // highlight-line
    pageInfo {
      currentPage
    }
  }
}
```

5. Clique no botão play na página GraphiQL e 2 objetos com nomes de alias que você forneceu devem ser produzidos.

### Recursos adicionais

- [Referência sobre alias em Gatsby GraphQL](/docs/graphql-reference/#aliasing)
- Exemplo ao vivo:

<iframe
  title="Usando alias"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20fileCount%3A%20allFile%20%7B%20%0A%20%20%20%20totalCount%0A%20%20%7D%0A%20%20filePageInfo%3A%20allFile%20%7B%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20currentPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

## Fragmentos de requisição GraphQL

Fragmentos GraphQL são pedaços compartilháveis de uma requisição que podem ser reutilizados.

Você pode querer usá-los para compartilhar vários campos entre as requisiçãos ou para colocar um componente com os dados que ele usa.

### Instruções

1. Declare uma string de template `graphql` com um fragmento nela. O fragmento deve ser composto pela palavra-chave `fragment`, um nome, o tipo GraphQL ao qual está associado (neste caso do tipo`Site`, como demonstrado por `no Site`), e os campos que compõem o fragmento:

```jsx
export const query = graphql`
  // highlight-start
  fragment SiteInformation on Site {
    title
    description
  }
  // highlight-end
`
```

2. Agora, inclua o fragmento em uma requisição para um campo do tipo especificado pelo fragmento. Isso inclui esses campos sem a necessidade de declará-los um a um:

```diff
export const pageQuery = graphql`
  query SiteQuery {
    site {
-     title
-     description
+   ...SiteInformation
    }
  }
`
```

** Nota **: Os fragmentos não precisam ser importados no Gatsby. Exportar uma requisição com um fragmento torna esse fragmento disponível em _todas_ as requisiçãos em seu projeto.

Os fragmentos podem ser aninhados dentro de outros fragmentos e vários fragmentos podem ser usados ​​na mesma requisição.

### Recursos adicionais

- [Exemplo simples de repositório usando fragmentos](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-fragments)
- [Referência Gatsby GraphQL para fragmentos](/docs/graphql-reference/#fragments)
- [Fragmentos de imagem de Gatsby](/docs/gatsby-image/#image-query-fragments)
- [Exemplo de repo com dados com localização compartilhada](https://github.com/gatsbyjs/gatsby/tree/master/examples/gatsbygram)

## Requisição dos dados no cliente com `fetch`

Os dados não precisam apenas ser requisitados no momento da construção e permanecerem exclusivamente estáticos. Você pode requisitar dados em tempo de execução da mesma forma que pode buscar dados em um aplicativo React normal.

### Pré-requisitos

- [Um site Gatsby](/docs/quick-start/)
- Um componente de página, como `index.js`

### Instruções

1. Em um arquivo com um componente React definido, como uma página em `src/pages` ou um componente de layout, importe os hooks React para `useState` e `useEffect`.

```jsx:title=src/pages/index.js
import React, { useState, useEffect } from "react"
```

2. Dentro do componente, envolva uma função de busca de dados em um hook `useEffect` para que recupere os dados de forma assíncrona quando o componente for montado no cliente do navegador. Então, espere o resultado usando a API `fetch`, e chame a função set do hook `useState` (neste caso`setStarsCount`) para salvar a variável de estado (`starsCount`) com os dados retornados em `fetch`.

```jsx:title=src/pages/index.js
import React, { useState, useEffect } from "react"

const PaginaIndex = () => {
  // highlight-start
  const [starsCount, setStarsCount] = useState(0)
  useEffect(() => {
    // get data from GitHub api
    fetch(`https://api.github.com/repos/gatsbyjs/gatsby`)
      .then(response => response.json()) // parse JSON from request
      .then(resultData => {
        setStarsCount(resultData.stargazers_count)
      }) // set data for the number of stars
  }, [])
  // highlight-end

  return (
    <section>
      // highlight-start
      <p>Runtime Data: Star count for the Gatsby repo {starsCount}</p>
      // highlight-end
    </section>
  )
}

export default PaginaIndex
```

### Recursos adicionais

- Guia sobre [busca de dados no cliente](/docs/data-fetching/)
- [Site de exemplo](https://gatsby-data-fetching.netlify.com/)
