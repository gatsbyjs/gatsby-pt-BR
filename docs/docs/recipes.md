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

Desejando um meio termo entre ler os [tutoriais completos](/tutorial/) e rastrear os [docs](/docs/)? Aqui está um livro de receitas orientadoras sobre como construir coisas, no estilo Gatsby.

## 1. Páginas e Layouts

### Estrutura do projeto

Dentro de um projeto Gatsby, você pode ver algumas ou todas as seguintes pastas e arquivos:

## [2. Styling with CSS](/docs/recipes/styling-css)

Alguns arquivos notáveis e suas definições:

- `gatsby-config.js` — configurar opções para um site do Gatsby, com metadados para o título do projeto, descrição, plugins, etc
- `gatsby-node.js` — implementar APIs Node.js do Gatsby para personalizar e estender as configurações padrão que afetam o processo de criação
- `gatsby-browser.js` — personalizar e estender as configurações padrão que afetam o navegador, usando as APIs do navegador do Gatsby
- `gatsby-ssr.js` — use as APIs de renderização do lado servidor do Gatsby para personalizar as configurações padrão que afetam a renderização do lado servidor

#### Conteúdos adicionais

- Para realizar um tour em todas as pastas e arquivos comuns, leia os documentos referentes a [Estrutura de um Projeto Gatsby](/docs/gatsby-project-structure/)
- Para comandos comuns, consulte a [documentação do Gatsby CLI](/docs/gatsby-cli)
- Confira a [folha de colas do Gatsby](/docs/cheat-sheet/) para obter informações de download

### Criando páginas automaticamente

O Gatsby _core_ transforma automaticamente os componentes React dentro de `src/pages` em páginas com URLs. Por exemplo, componentes em `src/pages/index.js` e` src/pages/about.js` criam páginas automaticamente seguindo os nomes dos arquivos para a página de índice do site (`/`) e `/about`.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- O [Gatsby CLI](/docs/gatsby-cli) instalado

#### Instruções

1. Crie um diretório para `src/pages` se o seu site ainda não tiver um
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

3. Execute `gatsby develop` para iniciar o servidor de desenvolvimento
4. Visite sua nova página no navegador: `http://localhost:8000/about`

#### Conteúdos adicionais

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

É comum agrupar páginas com um componente de layout React, o que possibilita o compartilhamento de marcação, estilos e funcionalidade em várias páginas

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)

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

#### Conteúdos adicionais

- Crie um componente de layout no [tutorial parte três](/tutorial/part-three/#your-first-layout-component)
- Estilizando com [componentes de layout](/docs/layout-components/)

### Criando páginas programaticamente com createPage

Você pode criar páginas programaticamente no arquivo `gatsby-node.js` com os métodos auxiliares que o Gatsby fornece.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Um arquivo `gatsby-node.js`

#### Instruções

1. Em `gatsby-node.js`, adicione uma exportação para `createPages`

```javascript:title=gatsby-node.js
// highlight-start
exports.createPages = ({ actions }) => {
  // ...
}
// highlight-end
```

2. Faça uma desestruturação da ação `createPage`, para que possa ser chamada sozinha e permitir que você adicione ou obtenha dados

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  // highlight-start
  const { createPage } = actions
  // puxe ou use quaisquer dados
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

3. Faça um loop pelos dados em `gatsby-node.js` e forneça o caminho, o modelo e o contexto (dados que serão passados no _pageContext_ dos objetos) para `createPage` em cada chamada

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

5. Execute `gatsby develop` e navegue até o caminho de uma das páginas que você criou (como em `http://localhost:8000/Fido`) para ver os dados que você passou exibidos na página

#### Conteúdos adicionais

- Seção do tutorial sobre [criar páginas programaticamente a partir de dados](/tutorial/part-seven/)
- Guia de referência para [usar o Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/)
- [Repositório exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-createPage) para esta receita

## 2. Estilizando com CSS

Existem muitas maneiras de adicionar estilos ao seu site; O Gatsby suporta quase todas as opções possíveis, através de plugins oficiais e da comunidade.

### Usando arquivos CSS globais sem um componente de Layout

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente de página de índice
- Um arquivo `gatsby-browser.js`

#### Instruções

1. Crie um arquivo CSS global com o nome `src/styles/global.css` e cole o seguinte trecho de código no arquivo:

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

#### Conteúdos adicionais

- Mais sobre [adicionando estilos globais sem um componente de layout](/docs/global-css/#adding-global-styles-without-a-layout-component)

### Usando estilos globais em um componente de layout

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente da página de índice

#### Instruções

Você pode adicionar estilos globais a um [componente de layout compartilhado](/tutorial/part-three/#your-first-layout-component). Esse componente é usado para coisas comuns em todo o site, como um cabeçalho ou rodapé.

1. Se você ainda não possui um, crie um novo diretório em seu site em `/src/components`

2. Dentro do diretório de componentes, crie dois arquivos: `layout.css` e `layout.js`

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

#### Conteúdos adicionais

- [Estilização padrão com arquivos CSS globais](/docs/global-css/)
- [Mais sobre componentes de layout](/tutorial/part-three)

### Usando Styled Components

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente da página de índice
- [gatsby-plugin-styled-components, styled-components, e babel-plugin-styled-components](/packages/gatsby-plugin-styled-components/) instalados no seu `package.json`

#### Instruções

1. Dentro do seu arquivo `gatsby-config.js`, adicione `gatsby-plugin-styled-components`

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

2. Abra o componente da página de índice (`src/pages/index.js`) e importe o pacote `styled-components`

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

#### Conteúdos adicionais

- [Mais sobre o uso de Styled Components](/docs/styled-components/)
- [Lições Egghead](https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components)

### Usando CSS Modules

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente da página de índice

#### Instruções

1. Crie um módulo CSS como `src/pages/index.module.css` e cole o seguinte trecho de código no módulo:

```css:title=src/components/index.module.css
.feature {
  margin: 2rem auto;
  max-width: 500px;
}
```

2. Importe o módulo CSS como um objeto JSX `style` no arquivo `index.js` modificando a página para que ela se pareça com o seguinte:

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

3. Execute `gatsby develop` para ver as alterações

**Nota:**
Observe que a extensão do arquivo é `.module.css` em vez de `.css`, o que informa ao Gatsby que este é um CSS module.

#### Conteúdos adicionais

- Mais sobre como [usar CSS Modules](/tutorial/part-two/#css-modules)
- [Exemplo usando CSS modules](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-css-modules)

### Usando Sass/SCSS

Sass é uma extensão do CSS que oferece recursos mais avançados, como regras aninhadas, variáveis, mixins e muito mais.

O Sass possui 2 sintaxes. A sintaxe mais usada é "SCSS", que é um superconjunto de CSS. Isso significa que toda sintaxe CSS válida é uma sintaxe SCSS válida. Os arquivos SCSS usam a extensão .scss

O Sass compilará arquivos .scss e .sass em arquivos .css para você, para que você possa escrever suas folhas de estilo com recursos mais avançados.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/).

#### Instruções

1. Instale o plugin Gatsby [gatsby-plugin-sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/) e o `node-sass`

`npm install --save node-sass gatsby-plugin-sass`

2. Inclua o plugin no seu arquivo `gatsby-config.js`

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

3.  Escreva suas folhas de estilo como arquivos `.sass` ou `.scss` e importe-as. Se você não sabe importar estilos, dê uma olhada em [Estilizando com CSS](/docs/recipes/#2-styling-with-css)

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

>_Nota: Você também pode usar arquivos Sass/SCSS como módulos, como mencionado na receita anterior sobre módulos CSS, com a diferença de que, em vez de .css, as extensões devem ser .scss ou .sass_

#### Conteúdos adicionais

- [Diferença entre .sass e .scss](https://responsivedesign.is/articles/difference-between-sass-and-scss/)
- [Guia no site oficial do Sass](https://sass-lang.com/guide)
- [Um tutorial de instalação mais completo sobre o Sass, com mais explicações e mais recursos](https://www.gatsbyjs.org/docs/sass/)

### Adicionando uma fonte local

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)
- Um arquivo de fonte: `.woff2`, `.ttf`, etc.

#### Instruções

1. Copie um arquivo de fonte no seu projeto Gatsby, como `src/fonts/fontname.woff2`

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
  font-family: "Nome da Fonte", sans-serif;
}
```

Ao direcionar o elemento HTML `body`, sua fonte será aplicada à maioria dos textos da página. CSS adicionais podem direcionar outros elementos, como `button` ou `textarea`.

Se ao seguir as etapas acima, as fontes não estiverem atualizando, certifique-se de substituir a família de fontes existente no CSS relevante.

#### Conteúdos adicionais

- Mais sobre [importar assets dentro de arquivos](/docs/importing-assets-into-files/)

### Usando Emotion

[Emotion](https://emotion.sh) é uma poderosa biblioteca CSS-in-JS que suporta estilos CSS inline e _styled components_. Você pode usar cada recurso de estilo individualmente ou juntos no mesmo arquivo

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)

#### Instruções

1. Instale o [plugin Gatsby Emotion](/packages/gatsby-plugin-emotion/) e os pacotes Emotion.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

2. Adicione o plugin `gatsby-plugin-emotion` ao seu arquivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

3. Se você ainda não possui uma, crie uma página no seu site do Gatsby em `src/pages/emotion-sample.js`.

Importe o pacote principal de `css` do Emotion. Você pode usar o prop `css` para adicionar [estilos de objetos do Emotion](https://emotion.sh/docs/object-styles) a qualquer elemento dentro de um componente:

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

#### Conteúdos adicionais

- [Usando Emotion no Gatsby](/docs/emotion/)
- [Emotion website](https://emotion.sh)
- [Introdução ao Emotion e Gatsby](https://egghead.io/lessons/gatsby-getting-started-with-emotion-and-gatsby)

### Usando Google Fonts

Hospedar suas próprias fontes (possivelmente provenientes do [Google Fonts](https://fonts.google.com/)) localmente em um projeto significa que eles não terão que ser buscados pela rede quando o site carregar, aumentando o índice de velocidade do site em até ~300 milissegundos no desktop e mais de 1 segundo no 3G. Também é recomendável limitar o uso de fontes personalizadas apenas ao essencial para o desempenho.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- O [Gatsby CLI](/docs/gatsby-cli/) instalado
- Escolher um pacote de fonte de [the typefaces project](https://github.com/KyleAMathews/typefaces)

#### Instruções

1. Execute `npm install --save typeface-sua-fonte-escolhida`, substituindo `sua-fonte-escolhida` pelo nome da fonte que você deseja instalar a partir do [projeto _typefaces_](https://github.com/KyleAMathews/typefaces).

Um bom exemplo para carregar uma fonte seria 'Source Sans Pro': `npm install --save typeface-source-sans-pro`.

2. Adicione `import "typeface-sua-fonte-escolhida"` a um modelo de layout, componente de página ou `gatsby-browser.js`.

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

#### Conteúdos adicionais

- [Typography.js](/docs/typography-js/) - Outra opção para usar fontes do Google em um site do Gatsby
- [Documentação do The Typefaces Project](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Exemplo de Kyle Mathews' blog](https://www.bricolage.io/typefaces-easiest-way-to-self-host-fonts/)

## 3. Trabalhando com Starters

[Starters](/docs/starters/) são sites padronizados do Gatsby mantidos oficialmente ou pela comunidade.

### Usando um starter

#### Pré-requisitos

- O [Gatsby CLI](/docs/gatsby-cli) instalado

#### Instruções

1. Encontre o starter que você gostaria de usar. (_O [Starter Library](/starters/?v=2) é um bom lugar para procurar!_)

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

#### Conteúdos adicionais

- Siga um [guia mais detalhado](/docs/starters/) sobre o uso de starters Gatsby.
- Aprenda a usar a ferramenta [Gatsby CLI](/docs/gatsby-cli) para usar os starters no [tutorial parte um](/tutorial/part-one/#using-gatsby-starters)
- Navegue pela [biblioteca dos Starters](/starters/?v=2)
- Confira o [starter padrão oficial do Gatsby](https://github.com/gatsbyjs/gatsby-starter-default)

## 4. Trabalhando com Temas

Um tema do Gatsby abstrai a configuração do Gatsby (funcionalidade compartilhada, fonte de dados, design) em um pacote instalável. Isso significa que a configuração e a funcionalidade não são gravadas diretamente no seu projeto, mas sim versionadas, gerenciadas centralmente e instaladas como uma dependência. Você pode atualizar perfeitamente um tema, compor temas juntos e até trocar um tema compatível por outro.

- Leia mais sobre [O que é um tema Gatsby?](/docs/themes/what-are-gatsby-themes)

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

#### Conteúdos adicionais

- Aprenda a usar um tema Gatsby existente no [guia conceitual mais curto](/docs/themes/using-a-gatsby-theme) ou no mais detalhado [tutorial passo a passo](/tutorial/using-a-theme)

### Criando um novo tema

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-the-gatsby-theme-workspace-starter-to-begin-building-a-new-theme"
  lessonTitle="Use the Gatsby Theme Workspace Starter to Begin Building a New Theme"
/>

#### Pré-requisitos

- O [Gatsby CLI](/docs/gatsby-cli) instalado

* [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) instalado

#### Instruções

1. Gere um novo _workspace_ com tema usando o [Gatsby theme workspace starter](https://github.com/gatsbyjs/gatsby-starter-theme-workspace):

```shell
gatsby new {nome-do-seu-projeto} https://github.com/gatsbyjs/gatsby-starter-theme-workspace
```

2. Execute o site de exemplo em seu _workspace_:

```shell
yarn workspace example develop
```

#### Conteúdos adicionais

- Siga um [guia mais detalhado](/docs/themes/building-themes/) sobre o uso do starter do _Gatsby theme workspace_.
- Aprenda como criar seu próprio tema no [curso em vídeo aula Gatsby Theme Authoring do Egghead](https://egghead.io/courses/gatsby-theme-authoring), ou nos cursos em [vídeo complementares do tutorial](/tutorial/building-a-theme).

## 5. Fonte de dados

A fonte de dados no Gatsby é orientada por plugins; Os plugins buscam dados de sua origem (por exemplo, o plugin `gatsby-source-filesystem` busca dados do sistema de arquivos, o plugin `gatsby-source-wordpress` busca dados da API do WordPress, etc).Você também pode fornecer os dados por conta própria.

### Adicionando dados ao GraphQL

A [camada de dados GraphQL](/docs/querying-with-graphql/) do Gatsby usa _nodes_ para modelar blocos de dados. Os plugins de origem do Gatsby adicionam _nodes_ de origem que você pode consultar, mas você também pode criar _nodes_ de origem. Para adicionar dados personalizados à camada de dados do GraphQL, o Gatsby fornece métodos que você pode aproveitar.

Esta receita mostra como adicionar dados personalizados usando `createNode()`.

#### Instruções

1. Em `gatsby-node.js`, use `sourceNodes()` e `actions.createNode()` para criar e exportar _nodes_ para poder consultar os dados.

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

2. Execute `gatsby develop`.

   > _Nota: Depois de fazer alterações no `gatsby-node.js`, você precisa executar novamente `gatsby develop` para que as alterações entrem em vigor._

3. Consultar os dados (no GraphiQL ou em seus componentes).

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

#### Conteúdos adicionais

- Veja um exemplo usando o plugin `gatsby-source-filesystem` no [tutorial parte cinco](/tutorial/part-five/#source-plugins)
- Pesquise plugins de origem disponíveis na [biblioteca Gatsby](/plugins/?=source)
- Entenda os plugins de origem criando um no [tutorial do plugin de fonte Pixabay](/docs/pixabay-source-plugin-tutorial/)
- A função createNode [documentação](/docs/actions/#createNode)

### Fornecendo dados de Markdown para postagens e páginas de blog com GraphQL

Você pode obter dados do Markdown e usar a API do Gatsby [`createPages`](/docs/actions/#createPage) para criar páginas dinamicamente.

Esta receita mostra como criar páginas a partir de arquivos Markdown no seu sistema de arquivos local usando a camada de dados GraphQL do Gatsby.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start) com um arquivo `gatsby-config.js`
- O [Gatsby CLI](/docs/gatsby-cli) instalado
- O [gatsby-source-filesystem plugin](/packages/gatsby-source-filesystem) instalado
- O [gatsby-transformer-remark plugin](/packages/gatsby-transformer-remark) instalado
- Um arquivo `gatsby-node.js`

#### Instruções

1. No `gatsby-config.js`, configure `gatsby-transformer-remark` junto com o `gatsby-source-filesystem` para extrair os arquivos Markdown de uma pasta de origem. Isso seria um acréscimo a quaisquer entradas anteriores do `gatsby-source-filesystem`, como para imagens:

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

2. Adicione uma postagem do Markdown ao `src/content`, incluindo _frontmatter_ para o título, data e caminho, com algum conteúdo inicial para o corpo da postagem:

```markdown:title=src/content/my-first-post.md
---
title: My First Post
date: 2019-07-10
path: /my-first-post
---

Este é o meu primeiro post do Gatsby escrito em Markdown!
```

3. Inicie o servidor de desenvolvimento com `gatsby develop`, navegue até o GraphiQL explorer em `http://localhost:8000/___graphql` e escreva uma consulta para obter todos os dados do markdown:

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

4. Adicione o código JavaScript para gerar páginas das postagens do Markdown no momento da construção, copiando a consulta GraphQL para `gatsby-node.js` e fazendo um loop pelos resultados:

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

5. Adicione um modelo de postagem no `src/templates`, incluindo uma consulta GraphQL para gerar páginas dinamicamente a partir do conteúdo do Markdown no momento da criação:

```jsx:title=src/templates/post.js
import React from "react"
import { graphql } from "gatsby"

export default function Template({ data }) {
  const { markdownRemark } = data // data.markdownRemark mantém seus dados da postagem
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

6. Execute `gatsby develop` para reiniciar o servidor de desenvolvimento. Veja sua postagem no navegador: `http://localhost:8000/my-first-post`

#### Conteúdos adicionais

- [Tutorial: Crie programaticamente páginas a partir de dados](/tutorial/part-seven/)
- [Criando e modificando páginas](/docs/creating-and-modifying-pages/)
- [Adicionando páginas Markdown](/docs/adding-markdown-pages/)
- [Guia para criar páginas de dados programaticamente](/docs/programmatically-create-pages-from-data/)
- [Repositório de exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-sourcing-markdown) para esta receita

### Pegando dados de uma fonte externa e criando páginas sem o GraphQL

Você não precisa usar a camada de dados GraphQL para incluir dados nas páginas, [embora haja razões pelas quais você deve considerar o GraphQL](/docs/why-gatsby-uses-graphql/). Você pode usar o _node API_ `createPages` para extrair dados não estruturados diretamente para sites do Gatsby, e não através do GraphQL e plugins de origem.

Nesta receita, você criará páginas dinâmicas a partir de dados buscados no [PokéAPI’s REST endpoints](https://www.pokeapi.co/). O [exemplo completo](https://github.com/jlengstorf/gatsby-with-unstructured-data/) pode ser encontrado no GitHub.

#### Pré-requisitos

- Um site Gatsby com um arquivo `gatsby-node.js`
- O [Gatsby CLI](/docs/gatsby-cli) instalado
- O pacote [axios](https://www.npmjs.com/package/axios) instalado através do _npm_

#### Instruções

1. No arquivo `gatsby-node.js`, adicione o código JavaScript para buscar dados da PokéAPI e crie programaticamente uma página de índice:

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

  // Crie uma página que lista os Pokémon.
  createPage({
    path: `/`,
    component: require.resolve("./src/templates/all-pokemon.js"),
    context: { allPokemon },
  })
}
```

2. Crie um modelo para exibir Pokémon na página inicial:

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

3. Execute `gatsby develop` para buscar os dados, criar páginas e iniciar o servidor de desenvolvimento.
4. Veja sua página inicial em um navegador: `http://localhost:8000`

#### Conteúdos adicionais

- [Repositório Pokemon com dados completos](https://github.com/jlengstorf/gatsby-with-unstructured-data/)
- Mais sobre o uso de dados não estruturados em [Usando o Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/)
- Quando e como [consultar dados com o GraphQL](/docs/querying-with-graphql/) para sites mais complexos usando Gatsby

### Fornecendo conteúdo do Drupal

#### Pré-requisitos

- A [Gatsby site](/docs/quick-start)
- A [Drupal](http://drupal.org) site
- The [JSON:API module](https://www.drupal.org/project/jsonapi) installed and enabled on the Drupal site

#### Instruções

1. Instale o plugin `gatsby-source-drupal`.

```
npm install --save gatsby-source-drupal
```

2. Edite seu arquivo `gatsby-config.js` para ativar o plugin e configurá-lo.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-drupal`,
      options: {
        baseUrl: `https://your-website/`,
        apiBase: `api`, // opcional, o padrão é `jsonapi`
      },
    },
  ],
}
```

3. Inicie o servidor de desenvolvimento com `gatsby develop` e abra o explorador GraphiQL em `http://localhost:8000/___ graphql`. Na guia Explorer, você verá novos tipos de _node_, como `allBlockBlock` para blocos Drupal, e um para cada tipo de conteúdo no site Drupal. Por exemplo, se você tiver um tipo de conteúdo "Página", ele estará disponível como `allNodePage`. Para consultar todos os _nodes_ "Página" por seu título e conteúdo, use uma consulta como:

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

4. Para usar seus dados do Drupal, crie uma nova página no seu site do Gatsby em `src/pages/drupal.js`. Esta página listará todos os _nodes_ da "Página" do Drupal.

_**Nota:** o esquema exato do GraphQL dependerá de como a instância do Drupal está estruturada._

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

5. Com o servidor de desenvolvimento em execução, você pode visualizar a nova página visitando `http://localhost:8000/drupal`.

#### Conteúdos adicionais

- [Usando Drupal desacoplado com Gatsby](/blog/2018-08-13-using-decoupled-drupal-with-gatsby/)
- [Mais informações sobre o Drupal](/docs/sourcing-from-drupal)
- [Tutorial: criar programaticamente páginas a partir de dados](/tutorial/part-seven/)

## 6. Consultando dados

### Consultando dados com uma Consulta de Página

Você pode usar a tag `graphql` para consultar dados nas páginas do seu site do Gatsby. Isso fornece acesso a qualquer coisa incluída na camada de dados do Gatsby, como metadados do site, plugins de origem, imagens e muito mais.

#### Instruções

1. Importe `graphql` de `gatsby`.

2. Exporte uma constante chamada `query` e defina seu valor como um modelo `graphql` com a consulta entre dois _backticks_.

3. Passe `data` como _prop_ para o componente.

4. A variável `data` contém os dados consultados e pode ser referenciada no JSX para gerar um HTML.

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

#### Conteúdos adicionais

- [GraphQL e Gatsby](/docs/graphql/): Entendendo a forma esperada dos seus dados
- [Mais sobre como consultar dados em páginas com o GraphQL](/docs/page-query/)
- [MDN em Tagged Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) como os usados no GraphQL

### Consultando dados com o StaticQuery Component

`StaticQuery` é um componente para recuperar dados da camada de dados do Gatsby em [componentes que não são de página](/docs/static-query/), como um _header_, _navigation_ ou qualquer outro componente filho.

#### Instruções

1. O componente `StaticQuery` requer dois objetos de renderização: `query` e `render`

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

2. Agora você pode usar esse componente como faria com [qualquer outro componente](/docs/building-with-components#non-page-components) importando-o para uma página maior de componentes JSX e marcação HTML.

### Consultando dados com _hook_ de useStaticQuery

Desde o Gatsby v2.1.0, você pode usar o _hook_ `useStaticQuery` para consultar dados com uma função JavaScript em vez de um componente. A sintaxe elimina a necessidade de um componente `<StaticQuery>` para agrupar tudo, o que algumas pessoas acham mais simples de escrever.

O _hook_ `useStaticQuery` pega uma consulta GraphQL e retorna os dados solicitados. Ele pode ser armazenado em uma variável e usada posteriormente em seus modelos JSX.

#### Pré-requisitos

- Você precisará do React e ReactDOM 16.8.0 ou posterior (manter o Gatsby atualizado)
- Leitura recomendada: as [regras de React Hooks](https://pt-br.reactjs.org/docs/hooks-rules.html)

#### Instruções

1. Importe `useStaticQuery` e `graphql` de `gatsby` para usar o _hook_ para consultar os dados.

2. No início de um componente funcional sem estado, atribua uma variável ao valor de `useStaticQuery` com sua consulta `graphql` passada como argumento.

3. No código JSX retornado do seu componente, é possível referenciar essa variável para manipular os dados retornados.

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

#### Conteúdos adicionais

- [Mais sobre consulta estática para consultar dados em componentes](/docs/static-query/)
- [A diferença entre uma consulta estática e uma consulta de página](/docs/static-query/#how-staticquery-differs-from-page-query)
- [Mais sobre o hook de useStaticQuery](/docs/use-static-query/)
- [Visualize seus dados com o GraphiQL](/docs/introducing-graphiql/)

### Limitando com GraphQL

Ao consultar dados com o GraphQL, você pode limitar o número de resultados retornados com um número específico. Isso é útil se você precisar apenas de alguns dados ou [paginar dados](/docs/adding-pagination/).

Para limitar os dados, você precisará de um site Gatsby com alguns nodes na camada de dados GraphQL. Todos os sites têm alguns _nodes_ como `allSitePage` e `sitePage` criados automaticamente: mais _nodes_ podem ser adicionados instalando plugins de origem como `gatsby-source-filesystem` em `gatsby-config.js`.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/)

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra uma guia no seu navegador em: `http://localhost:8000/___graphql`.
3. Adicione uma consulta no editor com os seguintes campos em `allSitePage` para começar:

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

4. Adicione um argumento `limit` ao campo `allSitePage` e atribua um valor inteiro `3`.

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

5. Clique no botão play na página GraphiQL e os dados no campo `edge` serão limitados ao número especificado.

#### Conteúdos adicionais

- Aprenda sobre [_nodes_ na API de dados GraphQL de Gatsby](/docs/node-interface/)
- [Referência do Gatsby GraphQL para limitar](/docs/graphql-reference/#limit)
- Exemplo:

<iframe
  title="Limiting returned data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(limit%3A%203)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Classificando com GraphQL

A ordem dos seus resultados pode ser especificada com o argumento do GraphQL  `sort`. Você pode especificar em quais campos classificar e a ordem em que serão classificados.

Para esta receita, você precisará de um site Gatsby com uma coleção de _nodes_ para classificar na camada de dados GraphQL. Todos os sites têm alguns _nodes_ como o `allSitePage` criado automaticamente: mais _nodes_ podem ser adicionados instalando plugins de origem.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Campos consultáveis prefixados com `all`, por exemplo `allSitePage`

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o GraphiQL Explorer em uma nova guia do navegador em: `http://localhost:8000/___ graphql`
3. Adicione uma consulta no editor com os seguintes campos em `allSitePage` para começar:

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

4. Adicione um argumento `sort` ao campo `allSitePage` e atribua a ele um objeto com os atributos `fields` e `order`. O valor para `fields` pode ser um campo ou uma matriz de campos para classificar (este exemplo usa o campo` path`); o `order` pode ser` ASC` ou `DESC` para crescente  e decrescente, respectivamente.

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

#### Conteúdo adicional

- [Referência do Gatsby GraphQL para classificação](/docs/graphql-reference/#sort)
- Aprenda sobre [_nodes_ na API de dados GraphQL de Gatsby](/docs/node-interface/)
- Exemplo:

<iframe
  title="Sorting data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(sort%3A%20%7Bfields%3A%20path%2C%20order%3A%20ASC%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Filtrando com GraphQL

Os resultados consultados podem ser filtrados com operadores como `eq` (igual), `ne` (não igual), `in` e `regex` em campos especificados.

Para esta receita, você precisará de um site Gatsby com uma coleção de _nodes_ para filtrar na camada de dados GraphQL. Todos os sites têm alguns _nodes_ como o `allSitePage` criado automaticamente: mais _nodes_  podem ser adicionados instalando plugins de fonte e transformadores, como `gatsby-source-filesystem` e `gatsby-transformer-comment` em `gatsby-config.js` para produzir `allMarkdownRemark `.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Campos consultáveis prefixados com `all`, por exemplo `allSitePage` ou `allMarkdownRemark`

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o GraphiQL Explorer em uma nova guia do navegador em: `http://localhost:8000/___ graphql`
3. Adicione uma consulta no editor usando um campo prefixado por 'all', como `allMarkdownRemark`(o que significa que ele retornará uma lista de _nodes_)

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

4. Adicione um argumento `filter` ao campo `allMarkdownRemark` e atribua a ele um objeto com os campos pelos quais você deseja filtrar. Neste exemplo, o conteúdo do Markdown é filtrado pelo atributo `categories` nos metadados do frontmatter. O próximo valor é o operador: neste caso, `eq`, ou igual a um valor de 'criaturas mágicas'.

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

5. Clique no botão play na página GraphiQL. Os dados que correspondem aos parâmetros do filtro devem ser retornados; nesse caso, apenas os arquivos Markdown de origem marcados com uma categoria de 'criaturas mágicas'.

#### Conteúdos adicionais

- [Referência do Gatsby GraphQL para filtragem](/docs/graphql-reference/#filter)
- [Lista completa de possíveis operadores](/docs/graphql-reference/#complete-list-of-possible-operators)
- Aprenda sobre [_nodes_ na API de dados GraphQL do Gatsby](/docs/node-interface/)
- Exemplo:

<iframe
  title="Filtering data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allMarkdownRemark(filter%3A%20%7Bfrontmatter%3A%20%7Bcategories%3A%20%7Beq%3A%20%22magical%20creatures%22%7D%7D%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20categories%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### GraphQL Query Alias 

Você pode renomear qualquer campo em uma consulta GraphQL com um _alias_.

Se você deseja executar duas consultas na mesma fonte de dados, pode usar um _alias_ para evitar uma colisão de nomes com duas consultas com o mesmo nome.

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o GraphiQL Explorer em uma nova guia do navegador em: `http://localhost:8000/___ graphql`
3. Adicione uma consulta no editor usando dois campos com o mesmo nome como `allFile`

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

4. Adicione o nome que você gostaria de usar para qualquer campo antes do nome do campo no esquema do GraphQL, separado por dois pontos. (Por exemplo, `[nome-do-alias]: [nome-original]`)

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

5. Clique no botão play na página GraphiQL e 2 objetos com nomes alternativos que você forneceu devem ser exibidos.

#### Conteúdos adicionais

- [Referência do Gatsby GraphQL para _alias_](/docs/graphql-reference/#aliasing)
- Exemplo:

<iframe
  title="Using aliases"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20fileCount%3A%20allFile%20%7B%20%0A%20%20%20%20totalCount%0A%20%20%7D%0A%20%20filePageInfo%3A%20allFile%20%7B%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20currentPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Fragmentos de Consulta GraphQL

Os fragmentos do GraphQL são pedaços compartilháveis de uma consulta que pode ser reutilizada.

Você pode usá-los para compartilhar vários campos entre as consultas ou para colocar um componente nos dados que ele usa.

#### Instruções

1. Declare uma string de modelo `graphql` com um fragmento nela. O fragmento deve ser composto da palavra-chave `fragment`, um nome, o tipo GraphQL ao qual está associado (neste caso, do tipo `Site`, conforme demonstrado em `on Site`), e os campos que compõem o fragmento:

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

2. Agora, inclua o fragmento em uma consulta para um campo do tipo especificado pelo fragmento. Isso inclui esses campos sem precisar declará-los todos de forma independente:

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

**Nota**: Fragmentos não precisam ser importados no Gatsby. A exportação de uma consulta com um fragmento torna esse fragmento disponível em _todas_ consultas no seu projeto.

Fragmentos podem ser aninhados dentro de outros fragmentos e vários fragmentos podem ser usados na mesma consulta.

#### Conteúdos adicionais

- [Exemplo simples de repositório usando fragmentos](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-fragments)
- [Referência do Gatsby GraphQL para fragmentos](/docs/graphql-reference/#fragments)
- [Fragmentos de imagem do Gatsby](/docs/gatsby-image/#image-query-fragments)
- [Exemplo de repositório com dados co-localizados](https://github.com/gatsbyjs/gatsby/tree/master/examples/gatsbygram)

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
// Informe ao webpack que este arquivo JS usa esta imagem
import FiestaImg from "../assets/fiesta.jpg" // highlight-line
```

2. In `index.js`, add an `<img>` tag with the `src` as the name of the import you used from webpack (in this case `FiestaImg`), and add an `alt` attribute [describing the image](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"
import FiestaImg from "../assets/fiesta.jpg"

export default () => (
  // O resultado da importação é o URL da sua imagem
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
        alt={image.node.base.split(".")[0]} // use somente a seção da extensão do arquivo com o nome do arquivo
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

- [Using global CSS files without a Layout component](/docs/recipes/styling-css#using-global-css-files-without-a-layout-component)
- [Using global styles in a layout component](/docs/recipes/styling-css#using-global-styles-in-a-layout-component)
- [Using Styled Components](/docs/recipes/styling-css#using-styled-components)
- [Using CSS Modules](/docs/recipes/styling-css#using-css-modules)
- [Using Sass/SCSS](/docs/recipes/styling-css#using-sassscss)
- [Adding a Local Font](/docs/recipes/styling-css#adding-a-local-font)
- [Using Emotion](/docs/recipes/styling-css#using-emotion)
- [Using Google Fonts](/docs/recipes/styling-css#using-google-fonts)

## [3. Working with starters](/docs/recipes/working-with-starters)

[Starters](/docs/starters/) are boilerplate Gatsby sites maintained officially, or by the community.

- [Using a starter](/docs/recipes/working-with-starters#using-a-starter)

## [4. Working with themes](/docs/recipes/working-with-themes)

A Gatsby theme lets you centralize the look-and-feel of your site. You can seamlessly update a theme, compose themes together, and even swap out one compatible theme for another.

- [Creating a new site using a theme](/docs/recipes/working-with-themes#creating-a-new-site-using-a-theme)
- [Creating a new site using a theme starter](/docs/recipes/working-with-themes#creating-a-new-site-using-a-theme-starter)
- [Building a new theme](/docs/recipes/working-with-themes#building-a-new-theme)

  // consulta para todas as remarcações

Pull data from multiple locations, like the filesystem or database, into your Gatsby site.

- [Adding data to GraphQL](/docs/recipes/sourcing-data#adding-data-to-graphql)
- [Sourcing Markdown data for blog posts and pages with GraphQL](/docs/recipes/sourcing-data#sourcing-markdown-data-for-blog-posts-and-pages-with-graphql)
- [Sourcing from WordPress](/docs/recipes/sourcing-data#sourcing-from-wordpress)
- [Sourcing data from Contentful](/docs/recipes/sourcing-data#sourcing-data-from-contentful)
- [Pulling data from an external source and creating pages without GraphQL](/docs/recipes/sourcing-data#pulling-data-from-an-external-source-and-creating-pages-without-graphql)
- [Sourcing content from Drupal](/docs/recipes/sourcing-data#sourcing-content-from-drupal)

## [6. Querying data](/docs/recipes/querying-data)

Gatsby lets you access your data across all sources using a single GraphQL interface.

- [Querying data with a Page Query](/docs/recipes/querying-data#querying-data-with-a-page-query)
- [Querying data with the StaticQuery Component](/docs/recipes/querying-data#querying-data-with-the-staticquery-component)
- [Querying data with the useStaticQuery hook](/docs/recipes/querying-data/#querying-data-with-the-usestaticquery-hook)
- [Limiting with GraphQL](/docs/recipes/querying-data#limiting-with-graphql)
- [Sorting with GraphQL](/docs/recipes/querying-data#sorting-with-graphql)
- [Filtering with GraphQL](/docs/recipes/querying-data#filtering-with-graphql)
- [GraphQL Query Aliases](/docs/recipes/querying-data#graphql-query-aliases)
- [GraphQL Query Fragments](/docs/recipes/querying-data#graphql-query-fragments)
- [Querying data client-side with fetch](/docs/recipes/querying-data#querying-data-client-side-with-fetch)

## [7. Working with images](/docs/recipes/working-with-images)

Access images as static resources, or automate the process of optimizing them through powerful plugins.

- [Import an image into a component with webpack](/docs/recipes/working-with-images#import-an-image-into-a-component-with-webpack)
- [Reference an image from the static folder](/docs/recipes/working-with-images#reference-an-image-from-the-static-folder)
- [Optimizing and querying local images with gatsby-image](/docs/recipes/working-with-images#optimizing-and-querying-local-images-with-gatsby-image)
- [Optimizing and querying images in post frontmatter with gatsby-image](/docs/recipes/working-with-images#optimizing-and-querying-images-in-post-frontmatter-with-gatsby-image)

## [8. Transforming data](/docs/recipes/transforming-data)

Transforming data in Gatsby is plugin-driven. Transformer plugins take data fetched using source plugins, and process it into something more usable (e.g. JSON into JavaScript objects, and more).

- [Transforming Markdown into HTML](/docs/recipes/transforming-data#transforming-markdown-into-html)
- [Transforming images into grayscale using GraphQL](/docs/recipes/transforming-data#transforming-images-into-grayscale-using-graphql)

- A Gatsby site with `gatsby-config.js` and an `index.js` page
- A Markdown file saved in your Gatsby site `src` directory
- A source plugin installed, such as `gatsby-source-filesystem`
- The `gatsby-transformer-remark` plugin installed

#### Directions

1. Add the transformer plugin in your `gatsby-config.js`:

```js:title=gatsby-config.js
plugins: [
  // não mostrado: gatsby-source-filesystem para criar _nodes_ para transformar
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

- [Preparing for deployment](/docs/recipes/deploying-your-site#preparing-for-deployment)
- [Deploying to Netlify](/docs/recipes/deploying-your-site#deploying-to-netlify)
- [Deploying to ZEIT Now](/docs/recipes/deploying-your-site#deploying-to-zeit-now)
