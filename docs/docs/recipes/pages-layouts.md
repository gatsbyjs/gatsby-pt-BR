---
title: "Receitas: Páginas e Layouts"
tableOfContentsDepth: 1
---

Adicione páginas ao seu site Gatsby, e use layouts para gerenciar elementos comuns entre essas páginas.

## Estrutura do projeto

Dentro de um projeto Gatsby, você verá algum ou todos os diretórios e arquivos abaixo:

```text
|-- /.cache
|-- /plugins
|-- /public
|-- /src
    |-- /pages
    |-- /templates
    |-- html.js
|-- /static
|-- gatsby-config.js
|-- gatsby-node.js
|-- gatsby-ssr.js
|-- gatsby-browser.js
```

Alguns arquivos importantes e suas definições:

- `gatsby-config.js` — configure opções para um site Gatsby, com metadados do projeto, como título, descrição, plugin e etc.
- `gatsby-node.js` — implemente as APIs em Node.js do Gatsby para, customizar e extender configurações padrão que, afetam o processo de compilação
- `gatsby-browser.js` — personalize e, extenda as configurações padrão que afetam o navegador, utilizando as APIs do Gatsby para navegadores.
- `gatsby-ssr.js` — utilize as APIs de SSR (_server-side rendering_) do Gatsby para, customizar configurações padrão que, afetam a renderização no lado do servidor

### Recursos adicionais

- Para conhecer todos os arquivos e pastas comuns, leia a documentação em [Estrutura de um projeto em Gatsby](/docs/docs/gatsby-project-structure.md)
- Para comandos comuns, confira a documentação da [CLI do Gatsby](/docs/docs/gatsby-cli.md)
- Confira a [Tabela de referência](/docs/docs/cheat-sheet.md) do Gatsby para dicas e comandos

## Criando páginas automaticamente

O Gatsby transforma automaticamente, componentes React no diretório `src/pages`, em páginas com URLs.
Por exemplo, componentes nos diretórios `src/pages/index.js` e `src/pages/about.js`, criam páginas automaticamente a partir dos nomes desses arquivos, para a página index (`/`) e `/about` do site.

### Pré-requisitos

- Um [site Gatsby](/docs/docs/quick-start.md)
- A [CLI do Gatsby](/docs/gatsby-cli) instalada

### Etapas

1. Crie um diretório para as páginas, nomeado `src/pages`, se seu site ainda não possuir um.

2. Adicione o arquivo `about.js` no diretório `src/pages`:

```jsx:title=src/pages/about.js
import React from "react"

const AboutPage = () => (
  <main>
    <h1>About the Author</h1>
    <p>Welcome to my Gatsby site.</p>
  </main>
)

export default AboutPage
```

3. Execute o comando `gatsby develop` para iniciar o servidor de desenvolvimento.
4. Visite sua nova página no navegador: `http://localhost:8000/about`

### Recursos adicionais

- [Criando e modificando páginas](/docs/docs/creating-and-modifying-pages.md)

## Criando um link entre páginas

O roteamento de links internos do seu site Gatsby baseia-se no componente `<Link />`

### Pré-requisitos

- Um site Gatsby com dois componentes de página: `index.js` e `contact.js`
- A [CLI do Gatsby](/docs/docs/gatsby-cli.md) instalada.

### Etapas

1. Abra o componente da página index (`src/pages/index.js`), e importe o componente `<Link />` do Gatsby. Adicione o componente `<Link />` no JSX, e passe a propriedade `to` com o valor `"/contact/"`, para exibir um link HTML melhorado do Gatsby.

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line

export default function Home() {
  return (
    <main>
      <h1>What a world.</h1>
      <p>
        <Link to="/contact/">Contact</Link> // highlight-line
      </p>
    </main>
  )
}
```

2. Execute o comando `gatsby develop` e navegue para a página index do site. Note que um link é exibido, e ao clicar nele, você é redirecionado para a página contatos.

> **Nota**: O componente `<Link />` do Gatsby envolve o [componente Link do `@reach/router`](https://reach.tech/router/api/Link). Ele gera um link HTML quando renderizado no browser, utilizando JavaScript para um melhor desempenho. Para mais informações, consulte [a API do componente `<Link />`](/docs/docs/gatsby-link.md)

### Recursos adicionais

- [Guia para criar links entre páginas](/docs/docs/linking-between-pages.md)
- [API de navegação do Gatsby](/docs/docs/gatsby-link.md)

## Criando um componente para o layout

É comum envolver páginas com um componente React de layout, o que possibilita compartilhar HTML, estilos e funcionalidades entre múltiplas páginas.

### Pré-requisitos

- [Um site Gatsby](/docs/docs/quick-start.md)

### Etapas

1. Crie um componente de layout no diretório `src/components`, onde componentes filhos serão passados como propriedade:

```jsx:title=src/components/layout.js
import React from "react"

export default function Layout({ children }) {
  return (
    <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
      {children}
    </div>
  )
}
```

2. Importe e use o componente de layout em uma página:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby"
import Layout from "../components/layout"

export default function Home() {
  return (
    <Layout>
      <Link to="/contact/">Contact</Link>
      <p>What a world.</p>
    </Layout>
  )
}
```

### Recursos adicionais

- Crie um componente de layout no [tutorial parte três](/docs/tutorial/part-three/index.md#crie-seu-primeiro-componente-de-layout)
- Estilização com [Componentes de Layout](/docs/docs/layout-components.md)

## Criando páginas programaticamente com a API createPage

Você pode criar páginas de forma programática no arquivo `gatsby-node.js` com os métodos auxiliares que o Gatsby fornece.

### Pré-requisitos

- Um [site Gatsby](/docs/docs/quick-start.md)
- Um arquivo `gatsby-node.js`

### Etapas

1. No arquivo `gatsby-node.js`, adicione um _export_ para o método `createPages`

```javascript:title=gatsby-node.js
// highlight-start
exports.createPages = ({ actions }) => {
  // ...
}
// highlight-end
```

2. Declare a propriedade `createPage` via desestruturação do objeto `actions`, para que seja possível executar essa função diretamente, e crie um objeto para os dados ou consulte de alguma API

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  // highlight-start
  const { createPage } = actions
  // pull in or use whatever data
  const dogData = [
    {
      name: "Fido",
      breed: "Sheltie",
    },
    {
      name: "Sparky",
      breed: "Corgi",
    },
  ]
  // highlight-end
}
```

3. Faça uma iteração entre os dados e forneça o caminho, template e _context_ (dados que serão passados via propriedade `pageContext`) para o método `createPage` para cada execução.

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  const { createPage } = actions

  const dogData = [
    {
      name: "Fido",
      breed: "Sheltie",
    },
    {
      name: "Sparky",
      breed: "Corgi",
    },
  ]
  // highlight-start
  dogData.forEach((dog) => {
    createPage({
      path: `/${dog.name}`,
      component: require.resolve(`./src/templates/dog-template.js`),
      context: { dog },
    })
  })
  // highlight-end
}
```

4. Crie um componente React para servir como template da página usada no método `createPage`

```jsx:title=src/templates/dog-template.js
import React from "react"

export default function DogTemplate({ pageContext: { dog } }) {
  return (
    <section>
      {dog.name} - {dog.breed}
    </section>
  )
}
```

5. Execute o comando `gatsby develop`, e navegue até o caminho de uma das páginas que você criou (como `http://localhost:8000/Fido`), para ver os seus dados serem exibidos na página

### Recursos adicionais

- Sessão do tutorial em [Crie páginas programaticamente a partir de dados](/docs/tutorial/part-seven/index.md)
- Guia de referência em [usando Gatsby sem GraphQL](/docs/docs/using-gatsby-without-graphql.md)
- [Repositório exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-createPage) para este tutorial
