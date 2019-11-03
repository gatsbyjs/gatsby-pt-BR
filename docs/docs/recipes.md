---
title: Recipes
tableOfContentsDepth: 2
---

<!-- Basic template for a Gatsby recipe:

## Task to accomplish.
1-2 sentences about it. The more concise and focused, the better!

### Prerequisites
- System/version requirements
- Everything necessary to set up the task
- Including setting up accounts at other sites, like Netlify
- See [docs templates](/docs/docs-templates/) for formatting tips

### Directions
Step-by-step directions. Each step should be repeatable and to-the-point. Anything not critical to the task should be omitted.

#### Live example (optional)
A live example may not be possible depending on the nature of the recipe, in which case it is fine to omit.

### Additional resources
- Tutorials
- Docs pages
- Plugin READMEs
- etc.

See [docs templates](/docs/docs-templates/) in the contributing docs for more help.
-->

Desejando um meio termo entre [tutoriais completos](/tutorial/) e rastreando os [docs](/docs/)? Aqui está um livro de receitas orientadoras sobre como construir coisas, no estilo Gatsby.

## 1. Páginas e Layouts

### Estrutura do projeto

Dentro de um projeto Gatsby, você pode ver algumas ou todas as seguintes pastas e arquivos:

```
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

Alguns arquivos notáveis e suas definições:

- `gatsby-config.js` — configurar opções para um site do Gatsby, com metadados para o título do projeto, descrição, plugins, etc.
- `gatsby-node.js` — implementar APIs Node.js do Gatsby para personalizar e estender as configurações padrão que afetam o processo de criação.
- `gatsby-browser.js` — personalizar e estender as configurações padrão que afetam o navegador, usando as APIs do navegador do Gatsby.
- `gatsby-ssr.js` — use as APIs de server-side rendering (SSR) do Gatsby para personalizar as configurações padrão que afetam a server-side rendering (SSR).

#### Contéudo adicional

- Para realizar um tour em todas as pastas e arquivos comuns, leia os documentos em [Gatsby's Project Structure](/docs/gatsby-project-structure/).
- Para comandos comuns, consulte o [Gatsby CLI docs](/docs/gatsby-cli).
- Confira a [Gatsby Cheat Sheet](/docs/cheat-sheet/) para obter informações de download.

### Criando páginas automaticamente

O Gatsby core transforma automaticamente os componentes React dentro de `src/pages` em páginas com URLs. Por exemplo, componentes em `src/pages/index.js` e` src/pages/about.js` criam páginas automaticamente seguindo os nomes dos arquivos para a página de índice do site (`/`) e `/about`.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- O [Gatsby CLI](/docs/gatsby-cli) instalado

#### Instruções

1. Crie um diretório para `src/pages` se o seu site ainda não tiver um.
2. Adicione um novo componente ao diretório de páginas:

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

3. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
4. Visite sua nova página no navegador: `http://localhost:8000/about`

#### Contéudo adicional

- [Criando e modificando páginas](/docs/creating-and-modifying-pages/)

### Vinculando páginas

O roteamento no Gatsby depende do componente `<Link />`.

#### Pré-requisitos

- Um site do Gatsby com dois componentes de página: `index.js` e` contact.js`
- O componente `<Link />` do Gatsby
- O [Gatsby CLI](/docs/gatsby-cli/) para executar o comando `gatsby develop`

#### Instruções

1. Abra o componente da página de índice (`src/pages/index.js`), importe o componente `<Link />` do Gatsby, adicione um componente `<Link />` e insira uma propriedade `to` com o valor de `"/contact/"` para o nome do caminho:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link>
    <p>What a world.</p>
  </div>
)
```

2. Execute `gatsby develop` e navegue até a página de índice. Você deve ter um link que o leve à página de contato quando clicado!

> **Nota**: O componente `<Link />` do Gatsby é um invólucro em torno do componente Link do [`@reach/router`](https://reach.tech/router/api/Link). Para obter mais informações sobre o componente `<Link />` de Gatsby, consulte a [Referência da API](/docs/gatsby-link/).

### Criando um componente de layout

É comum agrupar páginas com um componente de layout React, o que possibilita o compartilhamento de marcação, estilos e funcionalidade em várias páginas.

#### Pré-requisitos

- A Gatsby Site

#### Instruções

1. Crie um componente de layout em `src/components`, onde os componentes filhos serão transmitidos como props:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

2. Importe e use o componente de layout em uma página:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <Link to="/contact/">Contact</Link>
    <p>What a world.</p>
  </Layout>
)
```

#### Contéudo adicional

- Crie um componente de layout no [tutorial parte três](/tutorial/part-three/#your-first-layout-component)
- Estilizando com [componentes de layout](/docs/layout-components/)

### Criando páginas programaticamente com createPage

Você pode criar páginas programaticamente no arquivo `gatsby-node.js` com os métodos auxiliares que o Gatsby fornece.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Um arquivo `gatsby-node.js`

#### Instruções

1. Em `gatsby-node.js`, adicione uma exportação para` createPages`

```javascript:title=gatsby-node.js
// highlight-start
exports.createPages = ({ actions }) => {
  // ...
}
// highlight-end
```

2. Faça uma desestruturação da ação `createPage`, para que possa ser chamada sozinha e você adicione ou obtenha dados

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

3. Faça um loop pelos dados em `gatsby-node.js` e forneça o caminho, o modelo e o contexto (dados que serão passados no pageContext dos objetos) para` createPage` para cada chamada

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
  dogData.forEach(dog => {
    createPage({
      path: `/${dog.name}`,
      component: require.resolve(`./src/templates/dog-template.js`),
      context: { dog },
    })
  })
  // highlight-end
}
```

4. Crie um componente React para servir como modelo para sua página que foi usada em `createPage`

```jsx:title=src/templates/dog-template.js
import React from "react"

export default ({ pageContext: { dog } }) => (
  <section>
    {dog.name} - {dog.breed}
  </section>
)
```

5. Execute `gatsby develop` e navegue até o caminho de uma das páginas que você criou (como em` http://localhost:8000/Fido`) para ver os dados que você passou exibidos na página

#### Contéudo adicional

- Seção do tutorial sobre [criar páginas programaticamente a partir de dados](/tutorial/part-seven/)
- Guia de referência para [usar o Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/)
- [Repositória exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-createPage) para esta receita

## 2. Estilizando com CSS

Existem muitas maneiras de adicionar estilos ao seu site; O Gatsby suporta quase todas as opções possíveis, através de plugins oficiais e da comunidade.

### Usando arquivos CSS globais sem um componente de Layout

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente de página de índice
- Um arquivo `gatsby-browser.js`

#### Instruções

1. Crie um arquivo CSS global como `src/styles/global.css` e cole o seguinte trecho de código no arquivo:

```css:title=src/styles/styles/global.css
html {
  background-color: lavenderblush;
}

p {
  color: maroon;
}
```

2. Importe o arquivo CSS global no arquivo `gatsby-browser.js`, da seguinte maneira:

```javascript:gatsby-browser.js
import "./src/styles/global.css"
```

> **Nota:** Você também pode usar `require('./src/styles/global.css')` para importar o arquivo CSS global no seu arquivo `gatsby-config.js`.

3. Execute `gatsby-develop` para observar o estilo global sendo aplicado em seu site.

> **Nota:** Essa abordagem não é a melhor opção se você estiver usando CSS-in-JS para estilizar seu site. Nesse caso, uma página de layout com todos os componentes compartilhados deve ser usada. Isso é abordado na próxima receita.

#### Contéudo adicional

- Mais sobre [adicionando estilos globais sem um componente de layout](/docs/global-css/#adding-global-styles-without-a-layout-component)

### Usando estilos globais em um componente de layout

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente da página de índice

#### Instruções

Você pode adicionar estilos globais a um [componente de layout compartilhado](/tutorial/part-three/#your-first-layout-component). Esse componente é usado para coisas comuns em todo o site, como um cabeçalho ou rodapé.

1. Se você ainda não possui um, crie um novo diretório em seu site em `/src/components`.

2. Dentro do diretório de componentes, crie dois arquivos: `layout.css` e` layout.js`.

3. Adicione o seguinte trecho de código ao arquivo `layout.css`:

```css:title=/src/components/layout.css
body {
  background: red;
}
```

4. Edite `layout.js` para importar o arquivo CSS e estilizar o layout:

```jsx:title=/src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

5. Agora edite a página inicial do seu site em `/src/pages/.js` e use o novo componente de layout:

```jsx:title=/src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

#### Contéudo adicional

- [Estilização padrão com arquivos CSS globais](/docs/global-css/)
- [Mais sobre componentes de layout](/tutorial/part-three)

### Usando Styled Components

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente da página de índice
- [gatsby-plugin-styled-components, styled-components, e babel-plugin-styled-components](/packages/gatsby-plugin-styled-components/) instalados no seu `package.json`

#### Instruções

1. Dentro do seu arquivo `gatsby-config.js`, adicione` gatsby-plugin-style-components`

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

2. Abra o componente da página de índice (`src/pages/index.js`) e importe o pacote` styled-components`

3. Estilize os componentes criando blocos de estilo para cada tipo de elemento

4. Aplique à página incluindo componentes estilizados no JSX

```jsx:title=src/pages/index.js
import React from "react"
import styled from "styled-components" //highlight-line

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const Avatar = styled.img`
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const User = props => (
  <>
    <Avatar src={props.avatar} alt={props.username} />
    <Username>{props.username}</Username>
  </>
)

export default () => (
  <Container>
    <h1>About Styled Components</h1>
    <p>Styled Components is cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
    />
  </Container>
)
```

4. Execute `gatsby develop` para ver as alterações

#### Contéudo adicional

- [Mais sobre o uso de Styled Components](/docs/styled-components/)
- [Lições Egghead](https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components)

### Usando CSS Modules

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente de página de índice

#### Instruções

1. Crie um módulo CSS como `src/pages/index.module.css` e cole o seguinte trecho de código no módulo:

```css:title=src/components/index.module.css
.feature {
  margin: 2rem auto;
  max-width: 500px;
}
```

2. Importe o módulo CSS como um objeto JSX `style` no arquivo` index.js` modificando a página para que ela se pareça com o seguinte:

```jsx:title=src/pages/index.js
import React from "react"

// highlight-start
import style from "./index.module.css"

export default () => (
  <section className={style.feature}>
    <h1>Using CSS Modules</h1>
  </section>
)
// highlight-end
```

3. Execute `gatsby develop` para ver as alterações.

**Nota:**
Observe que a extensão do arquivo é `.module.css` em vez de` .css`, o que informa ao Gatsby que este é um CSS module.

#### Contéudo adicional

- Mais sobre como [usar CSS Modules](/tutorial/part-two/#css-modules)
- [Exemplo ao vivo usando CSS modules](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-css-modules)

### Usando Sass/SCSS

Sass é uma extensão do CSS que oferece recursos mais avançados, como regras aninhadas, variáveis, mixins e muito mais.

O Sass possui 2 sintaxes. A sintaxe mais usada é "SCSS" e é um superconjunto de CSS. Isso significa que toda sintaxe CSS válida é sintaxe SCSS válida. Os arquivos SCSS usam a extensão .scss

O Sass compilará arquivos .scss e .sass em arquivos .css para você, para que você possa escrever suas folhas de estilo com recursos mais avançados.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/).

#### Instruções

1. Instale o plug-in Gatsby [gatsby-plugin-sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/) e o `node-sass`.

`npm install --save node-sass gatsby-plugin-sass`

2. Inclua o plugin no seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

3.  Escreva suas folhas de estilo como arquivos `.sass` ou` .scss` e importe-as. Se você não sabe importar estilos, dê uma olhada em [Estilizando com CSS](/docs/recipes/#2-styling-with-css)

```css:title=styles.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css:title=styles.sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```javascript
import "./styles.scss"
import "./styles.sass"
```

>_Nota: Você também pode usar arquivos Sass / SCSS como módulos, como mencionado na receita anterior sobre módulos CSS, com a diferença de que, em vez de .css, as extensões devem ser .scss ou .sass_

#### Contéudo adicional

- [Diferença entre .sass e .scss](https://responsivedesign.is/articles/difference-between-sass-and-scss/)
- [Guia de Sass no site oficial do Sass](https://sass-lang.com/guide)
- [Um tutorial de instalação mais completo sobre o Sass, com mais explicações e mais recursos](https://www.gatsbyjs.org/docs/sass/)

### Adicionando uma fonte local

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)
- Um arquivo de fonte: `.woff2`, `.ttf`, etc.

#### Instruções

1. Copie um arquivo de fonte no seu projeto Gatsby, como `src/fonts/fontname.woff2`.

```
src/fonts/fontname.woff2
```

2. Importe o recurso de fonte em um arquivo CSS para agrupá-lo no site do Gatsby:

```css:title=src/css/typography.css
@font-face {
  font-family: "Font Name";
  src: url("../fonts/fontname.woff2");
}
```

**Nota:** Verifique se o nome da fonte é referenciado no CSS, por exemplo:

```css:title=src/components/layout.css
body {
  font-family: "Font Name", sans-serif;
}
```

Ao direcionar o elemento HTML `body`, sua fonte será aplicada à maioria dos textos da página. CSS adicionais podem direcionar outros elementos, como `button` ou` textarea`.

Se as fontes não estiverem atualizando as etapas acima, certifique-se de substituir a família de fontes existente no CSS relevante.

#### Contéudo adicional

- Mais sobre [importar assets dentro de arquivos](/docs/importing-assets-into-files/)

### Usando Emotion

[Emotion](https://emotion.sh) is a powerful CSS-in-JS library that supports both inline CSS styles and styled components. You can use each styling feature individually or together in the same file.

é uma poderosa biblioteca CSS-in-JS que suporta estilos CSS inline e styled components. Você pode usar cada recurso de estilo individualmente ou juntos no mesmo arquivo.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)

#### Instruções

1. Instale o [plugin Gatsby Emotion](/packages/gatsby-plugin-emotion/) e os pacotes Emotion.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

2. Adicione o plugin `gatsby-plugin-emotion` ao seu arquivo` gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

3. Se você ainda não possui uma, crie uma página no seu site do Gatsby em `src/pages/emotion-sample.js`.

Import Emotion's `css` core package. You can then use the `css` prop to add [Emotion object styles](https://emotion.sh/docs/object-styles) to any element inside a component:

Importar o pacote principal de `css` do Emotion. Você pode usar o prop `css` para adicionar [estilos de objetos do Emotion](https://emotion.sh/docs/object-styles) a qualquer elemento dentro de um componente:

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import { css } from "@emotion/core"

export default () => (
  <div>
    <p
      css={{
        background: "pink",
        color: "blue",
      }}
    >
      This page is using Emotion.
    </p>
  </div>
)
```

4. Para usar os [styled components do Emotion](https://emotion.sh/docs/styled), importe o pacote e defina-os usando a função `styled`.

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import styled from "@emotion/styled"

const Content = styled.div`
  text-align: center;
  margin-top: 10px;
  p {
    font-weight: bold;
  }
`

export default () => (
  <Content>
    <p>This page is using Emotion.</p>
  </Content>
)
```

#### Conteúdo adicional

- [Usando Emotion no Gatsby](/docs/emotion/)
- [Emotion website](https://emotion.sh)
- [Introdução ao Emotion e Gatsby](https://egghead.io/lessons/gatsby-getting-started-with-emotion-and-gatsby)

### Usando Google Fonts

Hospedar seu próprio [Google Fonts](https://fonts.google.com/) localmente em um projeto significa que eles não terão que ser buscados pela rede quando o site carregar, aumentando o índice de velocidade do site em até ~300 milissegundos no desktop e mais de 1 segundo no 3G. Também é recomendável limitar o uso de fontes personalizadas apenas ao essencial para o desempenho.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)
- O [Gatsby CLI](/docs/gatsby-cli/) instalado
- Escolher um pacote de fonte de [the typefaces project](https://github.com/KyleAMathews/typefaces)

#### Instruções

1. Execute `npm install --save typeface-sua-fonte-escolhida`, substituindo `sua-fonte-escolhida` pelo nome da fonte que você deseja instalar a partir do [the typefaces project](https://github.com/KyleAMathews/typefaces).

Um bom exemplo para carregar uma fonte seria 'Source Sans Pro': `npm install --save typeface-source-sans-pro`.

2. Adicione `import" typeface-sua-fonte-escolhida"` a um modelo de layout, componente de página ou `gatsby-browser.js`.

```jsx:title=src/components/layout.js
import "typeface-your-chosen-font"
```

3. Depois de importado, você pode fazer referência ao nome da fonte em uma folha de estilo CSS, CSS module ou CSS-in-JS.

```css:title=src/components/layout.css
body {
  font-family: "Your Chosen Font";
}
```

_NOTA: Portanto, para o exemplo acima, a declaração CSS relevante seria `font-family: 'Source Sans Pro';`_

#### Conteúdo adicional

- [Typography.js](/docs/typography-js/) - Outra opção para usar fontes do Google em um site do Gatsby
- [Documentação do The Typefaces Project](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Exemplo ao vivo em Kyle Mathews' blog](https://www.bricolage.io/typefaces-easiest-way-to-self-host-fonts/)

## 3. Trabalhando com Starters

[Starters](/docs/starters/) são sites padronizados do Gatsby mantidos oficialmente ou pela comunidade.

### Usando um starter

#### Pré-requisitos

- O [Gatsby CLI](/docs/gatsby-cli) instalado

#### Instruções

1. Encontre o starter que você gostaria de usar. (_O [Starter Library](/starters/?V=2) é um bom lugar para procurar!_)

2.Gere um novo site com base no starter. No terminal, execute:

```shell
gatsby new {nome-do-seu-projeto} {link-do-starter}
```

> _Não execute o comando acima como está - lembre-se de substituir {nome-do-seu-projeto} {link-do-starter}!_

3. Execute seu novo site:

```shell
cd {your-project-name}
gatsby develop
```

#### Conteúdo adicional

- Siga um [guia mais detalhado](/docs/starters/) sobre o uso de starters Gatsby.
- Aprenda a usar a ferramenta [Gatsby CLI](/docs/gatsby-cli) para usar os starters no [tutorial parte um](/tutorial/part-one/#using-gatsby-starters)
- Navegue pela [biblioteca de Starter's](/starters/?v=2)
- Confira o [starter padrão oficial do Gatsby](https://github.com/gatsbyjs/gatsby-starter-default)

## 4. Trabalhando com Temas

Um tema do Gatsby abstrai a configuração do Gatsby (funcionalidade compartilhada, fonte de dados, design) em um pacote instalável. Isso significa que a configuração e a funcionalidade não são gravadas diretamente no seu projeto, mas sim versionadas, gerenciadas centralmente e instaladas como uma dependência. Você pode atualizar perfeitamente um tema, compor temas juntos e até trocar um tema compatível por outro.

- Leia mais sobre [o que é um tema Gatsby?](/docs/themes/what-are-gatsby-themes)

### Criando um novo site usando um starter de temas

A criação de um site baseado em um starter que configura um tema segue o mesmo processo que a criação de um site baseado em um starter que **não** configura um tema. Neste exemplo, você pode usar o [starter para criar um novo site que use o tema oficial do blog Gatsby](https://github.com/gatsbyjs/gatsby-starter-blog-theme).

#### Pré-requisitos

- O [Gatsby CLI](/docs/gatsby-cli) instalado

#### Instruções

1. Gere um novo site com base no starter de temas do blog:

```shell
gatsby new {nome-do-seu-projeto} https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

2. Execute seu novo site:

```shell
cd {nome-do-seu-projeto}
gatsby develop
```

#### Conteúdo adicional

- Aprenda a usar um tema Gatsby existente no [guia conceitual mais curto](/docs/themes/using-a-gatsby-theme) ou no mais detalhado [tutorial passo a passo](/tutorial/using-a-theme)

### Building a new theme

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-the-gatsby-theme-workspace-starter-to-begin-building-a-new-theme"
  lessonTitle="Use the Gatsby Theme Workspace Starter to Begin Building a New Theme"
/>

#### Prerequisites

- The [Gatsby CLI](/docs/gatsby-cli) installed

* [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) installed

#### Directions

1. Generate a new theme workspace using the [Gatsby theme workspace starter](https://github.com/gatsbyjs/gatsby-starter-theme-workspace):

```shell
gatsby new {your-project-name} https://github.com/gatsbyjs/gatsby-starter-theme-workspace
```

2. Run the example site in the workspace:

```shell
yarn workspace example develop
```

#### Additional resources

- Follow a [more detailed guide](/docs/themes/building-themes/) on using the Gatsby theme workspace starter.
- Learn how to build your own theme in the [Gatsby Theme Authoring video course on Egghead](https://egghead.io/courses/gatsby-theme-authoring), or in the [video course's complementary written tutorial companion](/tutorial/building-a-theme).

## 5. Sourcing data

Data sourcing in Gatsby is plugin-driven; Source plugins fetch data from their source (e.g. the `gatsby-source-filesystem` plugin fetches data from the file system, the `gatsby-source-wordpress` plugin fetches data from the WordPress API, etc). You can also source the data yourself.

### Adding data to GraphQL

Gatsby's [GraphQL data layer](/docs/querying-with-graphql/) uses nodes to model chunks of data. Gatsby source plugins add source nodes that you can query for, but you can also create source nodes yourself. To add custom data to the GraphQL data layer yourself, Gatsby provides methods you can leverage.

This recipe shows you how to add custom data using `createNode()`.

#### Directions

1. In `gatsby-node.js` use `sourceNodes()` and `actions.createNode()` to create and export nodes to be able to query the data.

```javascript:title=gatsby-node.js
exports.sourceNodes = ({ actions, createNodeId, createContentDigest }) => {
  const pokemons = [
    { name: "Pikachu", type: "electric" },
    { name: "Squirtle", type: "water" },
  ]

  pokemons.forEach(pokemon => {
    const node = {
      name: pokemon.name,
      type: pokemon.type,
      id: createNodeId(`Pokemon-${pokemon.name}`),
      internal: {
        type: "Pokemon",
        contentDigest: createContentDigest(pokemon),
      },
    }
    actions.createNode(node)
  })
}
```

2. Run `gatsby develop`.

   > _Note: After making changes in `gatsby-node.js` you need to re-run `gatsby develop` for the changes to take effect._

3. Query the data (in GraphiQL or in your components).

```graphql
query MyPokemonQuery {
  allPokemon {
    nodes {
      name
      type
      id
    }
  }
}
```

#### Additional resources

- Walk through an example using the `gatsby-source-filesystem` plugin in [tutorial part five](/tutorial/part-five/#source-plugins)
- Search available source plugins in the [Gatsby library](/plugins/?=source)
- Understand source plugins by building one in the [Pixabay source plugin tutorial](/docs/pixabay-source-plugin-tutorial/)
- The createNode function [documentation](/docs/actions/#createNode)

### Sourcing Markdown data for blog posts and pages with GraphQL

You can source Markdown data and use Gatsby's [`createPages` API](/docs/actions/#createPage) to create pages dynamically.

This recipe shows how to create pages from Markdown files on your local filesystem using Gatsby's GraphQL data layer.

#### Prerequisites

- A [Gatsby site](/docs/quick-start) with a `gatsby-config.js` file
- The [Gatsby CLI](/docs/gatsby-cli) installed
- The [gatsby-source-filesystem plugin](/packages/gatsby-source-filesystem) installed
- The [gatsby-transformer-remark plugin](/packages/gatsby-transformer-remark) installed
- A `gatsby-node.js` file

#### Directions

1. In `gatsby-config.js`, configure `gatsby-transformer-remark` along with `gatsby-source-filesystem` to pull in Markdown files from a source folder. This would be in addition to any previous `gatsby-source-filesystem` entries, such as for images:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/src/content`,
      },
    },
  ]
```

2. Add a Markdown post to `src/content`, including frontmatter for the title, date, and path, with some initial content for the body of the post:

```markdown:title=src/content/my-first-post.md
---
title: My First Post
date: 2019-07-10
path: /my-first-post
---

This is my first Gatsby post written in Markdown!
```

3. Start up the development server with `gatsby develop`, navigate to the GraphiQL explorer at `http://localhost:8000/___graphql`, and write a query to get all markdown data:

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          path
        }
      }
    }
  }
}
```

<iframe
  title="Query for all markdown"
  src="https://q4xpb.sse.codesandbox.io/___graphql?explorerIsOpen=false&query=%7B%0A%20%20allMarkdownRemark%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D"
  width="600"
  height="300"
/>

4. Add the JavaScript code to generate pages from Markdown posts at build time by copying the GraphQL query into `gatsby-node.js` and looping through the results:

```js:title=gatsby-node.js
const path = require(`path`)

exports.createPages = async ({ actions, graphql }) => {
  const { createPage } = actions

  const result = await graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            frontmatter {
              path
            }
          }
        }
      }
    }
  `)
  if (result.errors) {
    console.error(result.errors)
  }

  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.frontmatter.path,
      component: path.resolve(`src/templates/post.js`),
    })
  })
}
```

5. Add a post template in `src/templates`, including a GraphQL query for generating pages dynamically from Markdown content at build time:

```jsx:title=src/templates/post.js
import React from "react"
import { graphql } from "gatsby"

export default function Template({ data }) {
  const { markdownRemark } = data // data.markdownRemark holds your post data
  const { frontmatter, html } = markdownRemark
  return (
    <div className="blog-post">
      <h1>{frontmatter.title}</h1>
      <h2>{frontmatter.date}</h2>
      <div
        className="blog-post-content"
        dangerouslySetInnerHTML={{ __html: html }}
      />
    </div>
  )
}

export const pageQuery = graphql`
  query($path: String!) {
    markdownRemark(frontmatter: { path: { eq: $path } }) {
      html
      frontmatter {
        date(formatString: "MMMM DD, YYYY")
        path
        title
      }
    }
  }
`
```

6. Run `gatsby develop` to restart the development server. View your post in the browser: `http://localhost:8000/my-first-post`

#### Additional resources

- [Tutorial: Programmatically create pages from data](/tutorial/part-seven/)
- [Creating and modifying pages](/docs/creating-and-modifying-pages/)
- [Adding Markdown pages](/docs/adding-markdown-pages/)
- [Guide to creating pages from data programmatically](/docs/programmatically-create-pages-from-data/)
- [Example repo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-sourcing-markdown) for this recipe

### Pulling data from an external source and creating pages without GraphQL

You don't have to use the GraphQL data layer to include data in pages, [though there are reasons why you should consider GraphQL](/docs/why-gatsby-uses-graphql/). You can use the node `createPages` API to pull unstructured data directly into Gatsby sites rather than through GraphQL and source plugins.

In this recipe, you'll create dynamic pages from data fetched from the [PokéAPI’s REST endpoints](https://www.pokeapi.co/). The [full example](https://github.com/jlengstorf/gatsby-with-unstructured-data/) can be found on GitHub.

#### Prerequisites

- A Gatsby Site with a `gatsby-node.js` file
- The [Gatsby CLI](/docs/gatsby-cli) installed
- The [axios](https://www.npmjs.com/package/axios) package installed through npm

#### Directions

1. In `gatsby-node.js`, add the JavaScript code to fetch data from the PokéAPI and programmatically create an index page:

```js:title=gatsby-node.js
const axios = require("axios")

const get = endpoint => axios.get(`https://pokeapi.co/api/v2${endpoint}`)

const getPokemonData = names =>
  Promise.all(
    names.map(async name => {
      const { data: pokemon } = await get(`/pokemon/${name}`)
      return { ...pokemon }
    })
  )
exports.createPages = async ({ actions: { createPage } }) => {
  const allPokemon = await getPokemonData(["pikachu", "charizard", "squirtle"])

  // Create a page that lists Pokémon.
  createPage({
    path: `/`,
    component: require.resolve("./src/templates/all-pokemon.js"),
    context: { allPokemon },
  })
}
```

2. Create a template to display Pokémon on the homepage:

```js:title=src/templates/all-pokemon.js
import React from "react"

export default ({ pageContext: { allPokemon } }) => (
  <div>
    <h1>Behold, the Pokémon!</h1>
    <ul>
      {allPokemon.map(pokemon => (
        <li key={pokemon.id}>
          <img src={pokemon.sprites.front_default} alt={pokemon.name} />
          <p>{pokemon.name}</p>
        </li>
      ))}
    </ul>
  </div>
)
```

3. Run `gatsby develop` to fetch the data, build pages, and start the development server.
4. View your homepage in a browser: `http://localhost:8000`

#### Additional resources

- [Full Pokemon data repo](https://github.com/jlengstorf/gatsby-with-unstructured-data/)
- More on using unstructured data in [Using Gatsby without GraphQL](/docs/using-gatsby-without-graphql/)
- When and how to [query data with GraphQL](/docs/querying-with-graphql/) for more complex Gatsby sites

### Sourcing content from Drupal

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- A [Drupal](http://drupal.org) site
- The [JSON:API module](https://www.drupal.org/project/jsonapi) installed and enabled on the Drupal site

#### Directions

1. Install the `gatsby-source-drupal` plugin.

```
npm install --save gatsby-source-drupal
```

2. Edit your `gatsby-config.js` file to enable the plugin and configure it.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-drupal`,
      options: {
        baseUrl: `https://your-website/`,
        apiBase: `api`, // optional, defaults to `jsonapi`
      },
    },
  ],
}
```

3. Start the development server with `gatsby develop`, and open the GraphiQL explorer at `http://localhost:8000/___graphql`. Under the Explorer tab, you should see new node types, such as `allBlockBlock` for Drupal blocks, and one for every content type in your Drupal site. For example, if you have a "Page" content type, it will be available as `allNodePage`. To query all "Page" nodes for their title and body, use a query like:

```graphql
{
  allNodePage {
    edges {
      node {
        title
        body {
          value
        }
      }
    }
  }
}
```

4. To use your Drupal data, create a new page in your Gatsby site at `src/pages/drupal.js`. This page will list all Drupal "Page" nodes.

_**Note:** the exact GraphQL schema will depend on your how Drupal instance is structured._

```jsx:title=src/pages/drupal.js
import React from "react"
import { graphql } from "gatsby"

const DrupalPage = ({ data }) => (
  <div>
    <h1>Drupal pages</h1>
    <ul>
    {data.allNodePage.edges.map(({ node, index }) => (
      <li key={index}>
        <h2>{node.title}</h2>
        <div>
          {node.body.value}
        </div>
      </li>
    ))}
   </ul>
  </div>
)

export default DrupalPage

export const query = graphql`
  {
  allNodePage {
    edges {
      node {
        title
        body {
          value
        }
      }
    }
  }
}
```

5. With the development server running, you can view the new page by visiting `http://localhost:8000/drupal`.

#### Additional Resources

- [Using Decoupled Drupal with Gatsby](/blog/2018-08-13-using-decoupled-drupal-with-gatsby/)
- [More on sourcing from Drupal](/docs/sourcing-from-drupal)
- [Tutorial: Programmatically create pages from data](/tutorial/part-seven/)

## 6. Querying data

### Querying data with a Page Query

You can use the `graphql` tag to query data in the pages of your Gatsby site. This gives you access to anything included in Gatsby's data layer, such as site metadata, source plugins, images, and more.

#### Directions

1. Import `graphql` from `gatsby`.

2. Export a constant named `query` and set its value to be a `graphql` template with the query between two backticks.

3. Pass in `data` as a prop to the component.

4. The `data` variable holds the queried data and can be referenced in JSX to output HTML.

```jsx:title=src/pages/index.js
import React from "react"
// highlight-next-line
import { graphql } from "gatsby"

import Layout from "../components/layout"

// highlight-start
export const query = graphql`
  query HomePageQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end

// highlight-next-line
const IndexPage = ({ data }) => (
  <Layout>
    // highlight-next-line
    <h1>{data.site.siteMetadata.title}</h1>
  </Layout>
)

export default IndexPage
```

#### Additional resources

- [GraphQL and Gatsby](/docs/graphql/): understanding the expected shape of your data
- [More on querying data in pages with GraphQL](/docs/page-query/)
- [MDN on Tagged Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) like the ones used in GraphQL

### Querying data with the StaticQuery Component

`StaticQuery` is a component for retrieving data from Gatsby's data layer in [non-page components](/docs/static-query/), such as a header, navigation, or any other child component.

#### Directions

1. The `StaticQuery` Component requires two render props: `query` and `render`.

```jsx:title=src/components/NonPageComponent.js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const NonPageComponent = () => (
  <StaticQuery
    query={graphql` // highlight-line
      query NonPageQuery {
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
        Querying title from NonPageComponent with StaticQuery:
        {data.site.siteMetadata.title}
      </h1>
    )}
  />
)

export default NonPageComponent
```

2. You can now use this component as you would [any other component](/docs/building-with-components#non-page-components) by importing it into a larger page of JSX components and HTML markup.

### Querying data with the useStaticQuery hook

Since Gatsby v2.1.0, you can use the `useStaticQuery` hook to query data with a JavaScript function instead of a component. The syntax removes the need for a `<StaticQuery>` component to wrap everything, which some people find simpler to write.

The `useStaticQuery` hook takes a GraphQL query and returns the requested data. It can be stored in a variable and used later in your JSX templates.

#### Prerequisites

- You'll need React and ReactDOM 16.8.0 or later (keeping Gatsby updated handles this)
- Recommended reading: the [Rules of React Hooks](https://reactjs.org/docs/hooks-rules.html)

#### Directions

1. Import `useStaticQuery` and `graphql` from `gatsby` in order to use the hook query the data.

2. In the start of a stateless functional component, assign a variable to the value of `useStaticQuery` with your `graphql` query passed as an argument.

3. In the JSX code returned from your component, you can reference that variable to handle the returned data.

```jsx:title=src/components/NonPageComponent.js
import React from "react"
import { useStaticQuery, graphql } from "gatsby" //highlight-line

const NonPageComponent = () => {
  // highlight-start
  const data = useStaticQuery(graphql`
    query NonPageQuery {
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
      Querying title from NonPageComponent: {data.site.siteMetadata.title}{" "}
      //highlight-line
    </h1>
  )
}

export default NonPageComponent
```

#### Additional resources

- [More on Static Query for querying data in components](/docs/static-query/)
- [The difference between a static query and a page query](/docs/static-query/#how-staticquery-differs-from-page-query)
- [More on the useStaticQuery hook](/docs/use-static-query/)
- [Visualize your data with GraphiQL](/docs/introducing-graphiql/)

### Limiting with GraphQL

When querying for data with GraphQL, you can limit the number of results returned with a specific number. This is helpful if you only need a few pieces of data or need to [paginate data](/docs/adding-pagination/).

To limit data, you'll need a Gatsby site with some nodes in the GraphQL data layer. All sites have some nodes like `allSitePage` and `sitePage` created automatically: more can be added by installing source plugins like `gatsby-source-filesystem` in `gatsby-config.js`.

#### Prerequisites

- A [Gatsby site](/docs/quick-start/)

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open a tab in your browser at: `http://localhost:8000/___graphql`.
3. Add a query in the editor with the following fields on `allSitePage` to start off:

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

4. Add a `limit` argument to the `allSitePage` field and give it an integer value `3`.

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

5. Click the play button in the GraphiQL page and the data in the `edges` field will be limited to the number specified.

#### Additional resources

- Learn about [nodes in Gatsby's GraphQL data API](/docs/node-interface/)
- [Gatsby GraphQL reference for limiting](/docs/graphql-reference/#limit)
- Live example:

<iframe
  title="Limiting returned data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(limit%3A%203)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Sorting with GraphQL

The ordering of your results can be specified with the GraphQL `sort` argument. You can specify which fields to sort by and the order to sort in.

For this recipe, you'll need a Gatsby site with a collection of nodes to sort in the GraphQL data layer. All sites have some nodes like `allSitePage` created automatically: more can be added by installing source plugins.

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- Queryable fields prefixed with `all`, e.g. `allSitePage`

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open the GraphiQL explorer in a browser tab at: `http://localhost:8000/___graphql`
3. Add a query in the editor with the following fields on `allSitePage` to start off:

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

4. Add a `sort` argument to the `allSitePage` field and give it an object with the `fields` and `order` attributes. The value for `fields` can be a field or an array of fields to sort by (this example uses the `path` field), the `order` can be either `ASC` or `DESC` for ascending and descending respectively.

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

5. Click the play button in the GraphiQL page and the data returned will be sorted ascending by the `path` field.

#### Additional resources

- [Gatsby GraphQL reference for sorting](/docs/graphql-reference/#sort)
- Learn about [nodes in Gatsby's GraphQL data API](/docs/node-interface/)
- Live example:

<iframe
  title="Sorting data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(sort%3A%20%7Bfields%3A%20path%2C%20order%3A%20ASC%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Filtering with GraphQL

Queried results can be filtered down with operators like `eq` (equals), `ne` (not equals), `in`, and `regex` on specified fields.

For this recipe, you'll need a Gatsby site with a collection of nodes to filter in the GraphQL data layer. All sites have some nodes like `allSitePage` created automatically: more can be added by installing source and transformer plugins like `gatsby-source-filesystem` and `gatsby-transformer-remark` in `gatsby-config.js` to produce `allMarkdownRemark`.

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- Queryable fields prefixed with `all`, e.g. `allSitePage` or `allMarkdownRemark`

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open the GraphiQL explorer in a browser tab at: `http://localhost:8000/___graphql`
3. Add a query in the editor using a field prefixed by 'all', like `allMarkdownRemark` (meaning that it will return a list of nodes)

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

4. Add a `filter` argument to the `allMarkdownRemark` field and give it an object with the fields you'd like to filter by. In this example, Markdown content is filtered by the `categories` attribute in frontmatter metadata. The next value is the operator: in this case `eq`, or equals, with a value of 'magical creatures'.

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

5. Click the play button in the GraphiQL page. The data that matches the filter parameters should be returned, in this case only sourced Markdown files tagged with a category of 'magical creatures'.

#### Additional resources

- [Gatsby GraphQL reference for filtering](/docs/graphql-reference/#filter)
- [Complete list of possible operators](/docs/graphql-reference/#complete-list-of-possible-operators)
- Learn about [nodes in Gatsby's GraphQL data API](/docs/node-interface/)
- Live example:

<iframe
  title="Filtering data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allMarkdownRemark(filter%3A%20%7Bfrontmatter%3A%20%7Bcategories%3A%20%7Beq%3A%20%22magical%20creatures%22%7D%7D%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20categories%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### GraphQL Query Aliases

You can rename any field in a GraphQL query with an alias.

If you would like to run two queries on the same datasource, you can use an alias to avoid a naming collision with two queries of the same name.

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open the GraphiQL explorer in a browser tab at: `http://localhost:8000/___graphql`
3. Add a query in the editor using two fields of the same name like `allFile`

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

4. Add the name you would like to use for any field before the name of the field in your GraphQL schema, separated by a colon. (E.g. `[alias-name]: [original-name]`)

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

5. Click the play button in the GraphiQL page and 2 objects with alias names you provided should be output.

#### Additional resources

- [Gatsby GraphQL reference for aliasing](/docs/graphql-reference/#aliasing)
- Live example:

<iframe
  title="Using aliases"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20fileCount%3A%20allFile%20%7B%20%0A%20%20%20%20totalCount%0A%20%20%7D%0A%20%20filePageInfo%3A%20allFile%20%7B%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20currentPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### GraphQL Query Fragments

GraphQL fragments are shareable chunks of a query that can be reused.

You might want to use them to share multiple fields between queries or to colocate a component with the data it uses.

#### Directions

1. Declare a `graphql` template string with a Fragment in it. The fragment should be made up of the keyword `fragment`, a name, the GraphQL type it is associated with (in this case of type `Site`, as demonstrated by `on Site`), and the fields that make up the fragment:

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

2. Now, include the fragment in a query for a field of the type specified by the fragment. This includes those fields without having to declare them all independently:

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

**Note**: Fragments don't need to be imported in Gatsby. Exporting a query with a Fragment makes that Fragment available in _all_ queries in your project.

Fragments can be nested inside other fragments, and multiple fragments can be used in the same query.

#### Additional resources

- [Simple example repo using fragments](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-fragments)
- [Gatsby GraphQL reference for fragments](/docs/graphql-reference/#fragments)
- [Gatsby image fragments](/docs/gatsby-image/#image-query-fragments)
- [Example repo with co-located data](https://github.com/gatsbyjs/gatsby/tree/master/examples/gatsbygram)

## 7. Working with images

### Import an image into a component with webpack

Images can be imported right into a JavaScript module with webpack. This process automatically minifies and copies the image to your site's `public` folder, providing a dynamic image URL for you to pass to an HTML `<img>` element like a regular file path.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-import-a-local-image-into-a-gatsby-component-with-webpack"
  lessonTitle="Import a Local Image into a Gatsby Component with webpack"
/>

#### Prerequisites

- A [Gatsby Site](/docs/quick-start) with a `.js` file exporting a React component
- an image (`.jpg`, `.png`, `.gif`, `.svg`, etc.) in the `src` folder

#### Directions

1. Import your file from its path in the `src` folder:

```jsx:title=src/pages/index.js
import React from "react"
// Tell webpack this JS file uses this image
import FiestaImg from "../assets/fiesta.jpg" // highlight-line
```

2. In `index.js`, add an `<img>` tag with the `src` as the name of the import you used from webpack (in this case `FiestaImg`), and add an `alt` attribute [describing the image](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"
import FiestaImg from "../assets/fiesta.jpg"

export default () => (
  // The import result is the URL of your image
  <img src={FiestaImg} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Run `gatsby develop` to start the development server.
4. View your image in the browser: `http://localhost:8000/`

#### Additional resources

- [Example repo importing an image with webpack](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-webpack-image)
- [More on all image techniques in Gatsby](/docs/images-and-files/)

### Reference an image from the `static` folder

As an alternative to importing assets with webpack, the `static` folder allows access to content that gets automatically copied into the `public` folder when built.

This is an **escape route** for [specific use cases](/docs/static-folder/#when-to-use-the-static-folder), and other methods like [importing with webpack](#import-an-image-into-a-component-with-webpack) are recommended to leverage optimizations made by Gatsby.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-a-local-image-from-the-static-folder-in-a-gatsby-component"
  lessonTitle="Use a local image from the static folder in a Gatsby component"
/>

#### Prerequisites

- A [Gatsby Site](/docs/quick-start) with a `.js` file exporting a React component
- An image (`.jpg`, `.png`, `.gif`, `.svg`, etc.) in the `static` folder

#### Directions

1. Ensure that the image is in your `static` folder at the root of the project. Your project structure might look something like this:

```
├── gatsby-config.js
├── src
│   └── pages
│       └── index.js
├── static
│       └── fiesta.jpg
```

2. In `index.js`, add an `<img>` tag with the `src` as the relative path of the file from the `static` folder, and add an `alt` attribute [describing the image](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <img src={`fiesta.jpg`} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Run `gatsby develop` to start the development server.
4. View your image in the browser: `http://localhost:8000/`

#### Additional resources

- [Example repo referencing an image from the static folder](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-static-image)
- [Using the Static Folder](/docs/static-folder/)
- [More on all image techniques in Gatsby](/docs/images-and-files/)

### Optimizing and querying local images with gatsby-image

The `gatsby-image` plugin can relieve much of the pain associated with optimizing images in your site.

Gatsby will generate optimized resources which can be queried with GraphQL and passed into Gatsby's image component. This takes care of the heavy lifting including creating several image sizes and loading them at the right time.

#### Prerequisites

- The `gatsby-image`, `gatsby-transformer-sharp`, and `gatsby-plugin-sharp` packages installed and added to the plugins array in `gatsby-config`
- [Images sourced](/packages/gatsby-image/#install) in your `gatsby-config` using a plugin like `gatsby-source-filesystem`

#### Directions

1. First, import `Img` from `gatsby-image`, as well as `graphql` and `useStaticQuery` from `gatsby`

```jsx
import { useStaticQuery, graphql } from "gatsby" // to query for image data
import Img from "gatsby-image" // to take image data and render it
```

2. Write a query to get image data, and pass the data into the `<Img />` component:

Choose any of the following options or a combination of them.

a. a single image queried by its file [path](/docs/content-and-data/) (Example: `images/corgi.jpg`)

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) { // highlight-line
      childImageSharp {
        fluid {
          base64
          aspectRatio
          src
          srcSet
          sizes
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="A corgi smiling happily" />
)
```

b. using a [GraphQL fragment](/docs/using-fragments/), to query for the necessary fields more tersely

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fluid {
          ...GatsbyImageSharpFluid // highlight-line
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="A corgi smiling happily" />
)
```

c. several images from a directory (Example: `images/dogs`) [filtered](/docs/graphql-reference/#filter) by the `extension` and `relativeDirectory` fields, and then mapped into `Img` components

```jsx
const data = useStaticQuery(graphql`
  query {
    allFile(
      // highlight-start
      filter: {
        extension: { regex: "/(jpg)|(png)|(jpeg)/" }
        relativeDirectory: { eq: "dogs" }
      }
      // highlight-end
    ) {
      edges {
        node {
          base
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`)

return (
  <div>
    // highlight-start
    {data.allFile.edges.map(image => (
      <Img
        fluid={image.node.childImageSharp.fluid}
        alt={image.node.base.split(".")[0]} // only use section of the file extension with the filename
      />
    ))}
    // highlight-end
  </div>
)
```

**Note**: This method can make it difficult to match images with `alt` text for accessibility. This example uses images with `alt` text included in the filename, like `dog in a party hat.jpg`.

d. an image of a fixed size using the `fixed` field instead of `fluid`

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fixed(width: 250, height: 250) { // highlight-line
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`)
return (
  <Img fixed={data.file.childImageSharp.fixed} alt="A corgi smiling happily" />
)
```

e. an image of a fixed size with a `maxWidth`

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fixed(maxWidth: 250) { // highlight-line
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`)
return (
  <Img fixed={data.file.childImageSharp.fixed} alt="A corgi smiling happily" /> // highlight-line
)
```

f. an image filling a fluid container with a max width (in pixels) and a higher quality (the default value is 50 i.e. 50%)

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fluid(maxWidth: 800, quality: 75) { // highlight-line
          ...GatsbyImageSharpFluid
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="A corgi smiling happily" />
)
```

3. (Optional) Add inline styles to the `<Img />` like you would to other components

```jsx
<Img
  fluid={data.file.childImageSharp.fluid}
  alt="A corgi smiling happily"
  style={{ border: "2px solid rebeccapurple", borderRadius: 5, height: 250 }} // highlight-line
/>
```

4. (Optional) Force an image into a desired aspect ratio by overriding the `aspectRatio` field returned by the GraphQL query before it is passed into the `<Img />` component

```jsx
<Img
  fluid={{
    ...data.file.childImageSharp.fluid,
    aspectRatio: 1.6, // 1280 / 800 = 1.6
  }}
  alt="A corgi smiling happily"
/>
```

5. Run `gatsby develop`, to generate images from files in the filesystem (if not done already) and cache them

#### Additional resources

- [Example repository illustrating these examples](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [Gatsby Image API](/docs/gatsby-image/)
- [Using Gatsby Image](/docs/using-gatsby-image)
- [More on working with images in Gatsby](/docs/working-with-images/)
- [Free egghead.io videos explaining these steps](https://egghead.io/playlists/using-gatsby-image-with-gatsby-ea85129e)

### Optimizing and querying images in post frontmatter with gatsby-image

For use cases like a featured image in a blog post, you can _still_ use `gatsby-image`. The `Img` component needs processed image data, which can come from a local (or remote) file, including from a URL in the frontmatter of a `.md` or `.mdx` file.

To inline images in markdown (using the `![]()` syntax), consider using a plugin like [`gatsby-remark-images`](/packages/gatsby-remark-images/)

#### Prerequisites

- The `gatsby-image`, `gatsby-transformer-sharp`, and `gatsby-plugin-sharp` packages installed and added to the plugins array in `gatsby-config`
- [Images sourced](/packages/gatsby-image/#install) in your `gatsby-config` using a plugin like `gatsby-source-filesystem`
- Markdown files sourced in your `gatsby-config` with image URLs in frontmatter
- [Pages created](/docs/creating-and-modifying-pages/) from Markdown using [`createPages`](https://www.gatsbyjs.org/docs/node-apis/#createPages)

#### Directions

1. Verify that the Markdown file has an image URL with a valid path to an image file in your project

```mdx:title=post.mdx
---
title: My First Post
featuredImage: ./corgi.png // highlight-line
---

Post content...
```

2. Verify that a unique identifier (a slug in this example) is passed in context when `createPages` is called in `gatsby-node.js`, which will later be passed into a GraphQL query in the Layout component

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  // query for all markdown

  result.data.allMdx.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/components/markdown-layout.js`),
      // highlight-start
      context: {
        slug: node.fields.slug,
      },
      // highlight-end
    })
  })
}
```

3. Now, import `Img` from `gatsby-image`, and `graphql` from `gatsby` into the template component, write a [pageQuery](/docs/page-query/) to get image data based on the passed in `slug` and pass that data to the `<Img />` component:

```jsx:title=markdown-layout.jsx
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Img from "gatsby-image" // highlight-line

export default ({ children, data }) => (
  <main>
    // highlight-start
    <Img
      fluid={data.markdown.frontmatter.image.childImageSharp.fluid}
      alt="A corgi smiling happily"
    />
    // highlight-end
    {children}
  </main>
)

// highlight-start
export const pageQuery = graphql`
  query PostQuery($slug: String) {
    markdown: mdx(fields: { slug: { eq: $slug } }) {
      id
      frontmatter {
        image {
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`
// highlight-end
```

4. Run `gatsby develop`, which will generate images for files sourced in the filesystem

#### Additional resources

- [Example repository using this recipe](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [Featured images with frontmatter](/docs/working-with-images-in-markdown/#featured-images-with-frontmatter-metadata)
- [Gatsby Image API](/docs/gatsby-image/)
- [Using Gatsby Image](/docs/using-gatsby-image)
- [More on working with images in Gatsby](/docs/working-with-images/)

## 8. Transforming data

Transforming data in Gatsby is plugin-driven. Transformer plugins take data fetched using source plugins, and process it into something more usable (e.g. JSON into JavaScript objects, and more).

### Transforming Markdown into HTML

The `gatsby-transformer-remark` plugin can transform Markdown files to HTML.

#### Prerequisites

- A Gatsby site with `gatsby-config.js` and an `index.js` page
- A Markdown file saved in your Gatsby site `src` directory
- A source plugin installed, such as `gatsby-source-filesystem`
- The `gatsby-transformer-remark` plugin installed

#### Directions

1. Add the transformer plugin in your `gatsby-config.js`:

```js:title=gatsby-config.js
plugins: [
  // not shown: gatsby-source-filesystem for creating nodes to transform
  `gatsby-transformer-remark`
],
```

2. Add a GraphQL query to the `index.js` file of your Gatsby site to fetch `MarkdownRemark` nodes:

```jsx:title=src/pages/index.js
export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

3. Restart the development server and open GraphiQL at `http://localhost:8000/___graphql`. Explore the fields available on the `MarkdownRemark` node.

#### Additional resources

- [Tutorial on transforming Markdown to HTML](/tutorial/part-six/#transformer-plugins) using `gatsby-transformer-remark`
- Browse available transformer plugins in the [Gatsby plugin library](/plugins/?=transformer)

## 9. Deploying your site

Showtime. Once you are happy with your site, you are ready to go live with it!

### Preparing for deployment

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- The [Gatsby CLI](/docs/gatsby-cli) installed

#### Directions

1. Stop your development server if it is running (`Ctrl + C` on your command line in most cases)

2. For the standard site path at the root directory (`/`), run `gatsby build` using the Gatsby CLI on the command line. The built files will now be in the `public` folder.

```shell
gatsby build
```

3. To include a site path other than `/` (such as `/site-name/`), set a path prefix by adding the following to your `gatsby-config.js` and replacing `yourpathprefix` with your desired path prefix:

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/yourpathprefix`,
}
```

There are a few reasons to do this -- for instance, hosting a blog built with Gatsby on a domain with another site not built on Gatsby. The main site would direct to `example.com`, and the Gatsby site with a path prefix could live at `example.com/blog`.

4. With a path prefix set in `gatsby-config.js`, run `gatsby build` with the `--prefix-paths` flag to automatically add the prefix to the beginning of all Gatsby site URLs and `<Link>` tags.

```shell
gatsby build --prefix-paths
```

5. Make sure that your site looks the same when running `gatsby build` as with `gatsby develop`. By running `gatsby serve` when you build your site, you can test out (and debug if necessary) the finished product before deploying it live.

```shell
gatsby build && gatsby serve
```

#### Additional resources

- Walk through building and deploying an example site in [tutorial part one](/tutorial/part-one/#deploying-a-gatsby-site)
- Learn about [performance optimization](/docs/performance/)
- Read about [other deployment related topics](/docs/preparing-for-deployment/)
- Check out the [deployment docs](/docs/deploying-and-hosting/) for specific hosting platforms and how to deploy to them

### Deploying to Netlify

Use [`netlify-cli`](https://www.netlify.com/docs/cli/) to deploy your Gatsby application without leaving the command-line interface.

#### Prerequisites

- A [Gatsby site](/docs/quick-start) with a single component `index.js`
- The [netlify-cli](https://www.npmjs.com/package/netlify-cli) package installed
- The [Gatsby CLI](/docs/gatsby-cli) installed

#### Directions

1. Build your gatsby application using `gatsby build`

2. Login into Netlify using `netlify login`

3. Run the command `netlify init`. Select the "Create & configure a new site" option.

4. Choose a custom website name if you want or press enter to receive a random one.

5. Choose your [Team](https://www.netlify.com/docs/teams/).

6. Change the deploy path to `public/`

7. Make sure that everything looks fine before deploying to production using `netlify deploy --prod`

#### Additional resources

- [Hosting on Netlify](/docs/hosting-on-netlify)
- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify)

### Deploying to ZEIT Now

Use [Now CLI](https://zeit.co/download) to deploy your Gatsby application without leaving the command-line interface.

#### Prerequisites

- A [ZEIT Now](https://zeit.co/signup) account
- A [Gatsby site](/docs/quick-start) with a single component `index.js`
- [Now CLI](https://zeit.co/download) package installed
- [Gatsby CLI](/docs/gatsby-cli) installed

#### Directions

1. Login into Now CLI using `now login`

2. Change to the directory of your Gatsby.js application in the Terminal if you aren't already there

3. Run `now` to deploy it

#### Additional resources

- [Deploying to ZEIT Now](/docs/deploying-to-zeit-now/)
