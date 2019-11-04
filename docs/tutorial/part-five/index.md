---
title: Plugins Nativos
typora-copy-images-to: ./
disableTableOfContents: true
---

> Esse tutorial faz parte da série sobre a camada de dados do Gatsby. Tenha certeza que já passou pela [parte 4](/tutorial/part-four/) antes de continuar.

## O que tem nesse tutorial?

Neste tutorial, você aprenderá como puxar dados para seu site Gatsby usando GraphQL e plugins nativos. Porém, antes de você aprender sobre esses plugins, você precisará saber como usar algo chamado GraphiQL, uma ferramenta que lhe ajudará a estruturar suas _queries_ corretamente.

## Introduzindo GraphiQL

GraphiQL é a _IDE_ (Ambiente de Desenvolvimento Integrado) do GraphQL. É uma poderosa e impressionante ferramenta que você utilizará com frequência enquanto estiver construindo websites em Gatsby.

Você pode acessá-lo quando o servidor de desenvolvimento estiver executando em
<http://localhost:8000/___graphql>.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Seu navegador não suporta o elemento HTML video.</p>
</video>

Explore o "tipo" `Site` já incluso e veja quais são os campos disponíveis nele -- incluindo o objeto `siteMetadata` que você recebeu na _query_ anteriormente. Tente abrir o GraphiQL e brinque com os seus dados! Aperte <kbd>Ctrl + Espaço</kbd> (ou use <kbd>Shift + Espaço</kbd> como um atalho alternativo do teclado) para trazer a janela de _autocomplete_ e <kbd>Ctrl + Enter</kbd> para executar a _query_ GraphQL. Você utilizará GraphiQL muito mais durante o restante desse tutorial.

## Usando o explorador do GraphiQL

O Explorador do GraphiQL permite que você construa interativamente _queries_ completar clicando nos campos e _inputs_ disponíveis sem o processo repetitivo de escrever essas _queries_ na mão

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer"
  lessonTitle="Build a GraphQL Query using Gatsby’s GraphiQL Explorer"
/>

## Plugins nativos

Dados em sites Gatsby podem vir de qualquer lugar: APIs, banco de dados, CMSs, arquivos locais, etc.

Plugins nativos buscam por dados através de sua origem. Por exemplo: o plugin nativo dos arquivos de sistema (_filesystem_) sabe como trazer os dados através de arquivos do sistema. O plugin do WordPress sabe como buscar os dados da API do WordPress.

Adicione o [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) e explore como ele funciona.

Primeiro, instale o plugin no diretório raiz do projeto:

```shell
npm install --save gatsby-source-filesystem
```

Então, adicione-o em `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    // highlight-end
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Salve o arquivo e reinicie o servidor de desenvolvimento do gatsby. Então, abra o GraphiQL novamente.

No painel de _Explorer_, você verá `allFile` e `file` disponíveis como opções:

![graphiql-filesystem](graphiql-filesystem.png)

Clique em `allFile` no menu _dropdown_. Posicione seu cursor depois de `allFile` na área de _query_, e então pressione <kbd>Ctrl + Enter</kbd>. Isso irá preencher uma _query_ para o id de cada arquivo. Aperte o botão "_Play_" para executar a _query_:

![filesystem-query](filesystem-query.png)

No painel _Explorer_, o campo `id` foi automaticamente selecionado. Faça seleções para mais campos selecionando a caixa de seleção do respectivo campo. Pressione "_Play_" para executar a _query_ novamente, agora com os novos campos:

![filesystem-explorer-options](filesystem-explorer-options.png)

Alternativamente, você pode adicionar campos usando o atalho de _autocomplete_ (<kbd>Ctrl + Espaço</kbd>). Isso irá mostrar os campos disponíveis na _query_ nos nós `File`.

![filesystem-autocomplete](filesystem-autocomplete.png)

Tente adicionar um número de campos na sua query, pressionando <kbd>Ctrl + Enter</kbd>
toda vez para executar novamente a _query_. Você verá os resultados atualizados da _query_:

![allfile-query](allfile-query.png)

O resultado é um vetor de nós do tipo `File` (nó é um nome chique para um objeto em um
"grafo"). Cada objeto nó `File` tem os campos que você solicitou na _query_.

## Construa uma página com uma _query_ GraphQL

A construção de novas páginas com o Gatsby geralmente começa no GraphiQL. Você primeiro fará um rascunho
da _query_ de dados explorando no GraphiQL para então fazer a cópia dele para um componente React
para começar a construir a interface do usuário.

Vamos tentar isso.

Crie um novo arquivo em `src/pages/my-files.js` com a _query_ GraphQL `allFile` que você acabou de
criar:

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data) // highlight-line
  return (
    <Layout>
      <div>Hello world</div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

A linha `console.log(data)` é destacada acima. Ela é geralmente útil quando se está
criando um novo componente para mostrar no console os dados que você está recebendo da _query_ GraphQL
para que então você consiga explorar os dados no seu navegador enquanto constrói a interface do usuário.

Se você visitar a nova página em `/my-files/` e abrir o console do seu navegador
você verá algo como:

![data-in-console](data-in-console.png)

O formato dos dados combinam com o formato da _query_ GraphQL.

Adicione um pouco de código no seu componente para imprimir os dados do arquivo.

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>My Site's Files</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

E agora visite [http://localhost:8000/my-files](http://localhost:8000/my-files)… 😲
![my-files-page](my-files-page.png)

## O que vem na sequência?

Agora você aprendeu como os plugins nativos trazem dados _para dentro_ do sistema de dados do Gatsby. No próximo tutorial, você aprenderá como plugins de transformação _transformam_ o conteúdo bruto trazido pelos plugins nativos. A combinaçào de plugins nativos com plugins de transformação pode lidar com toda origem e transformação de dados que você pode precisar quando está construindo um site Gatsby. Aprenda sobre plugins de transformação na [parte seis do tutorial](/tutorial/part-six/).
