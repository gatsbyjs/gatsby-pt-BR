---
title: Receitas
tableOfContentsDepth: 2
---

<!-- Modelo básico para uma receita de Gatsby:

## Tarefa a realizar.
1-2 frases sobre isso. Quanto mais conciso e focado, melhor!

### Pré-requisitos
- Requisitos de sistema/versão
- Tudo o necessário para configurar a tarefa
- Incluindo a configuração de contas em outros sites, como o Netlify
- Consulte [modelos de documentos](/docs/docs-templates/) para dicas de formatação

### Instruções
Instruções passo a passo. Cada passo deve ser repetível e direto ao ponto. Qualquer coisa que não seja crítica para a tarefa deve ser omitida.

#### Exemplo ao vivo (opcional)
Um exemplo ao vivo pode não ser possível, dependendo da natureza da receita; nesse caso, é aceitável omitir.

### Recursos adicionais
- Tutoriais
- Páginas de Documentos
- READMEs de plugin
- etc.

Veja [modelos de documentos](/docs/docs-templates/) nos documentos de contribuição para obter mais ajuda.
-->

Desejando um meio termo entre [tutoriais completos](/tutorial/) e rastejar pelos [docs](/docs/)? Aqui está um livro de receitas orientadoras sobre como construir coisas, no estilo Gatsby.

## 1. Páginas e layouts

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

Alguns arquivos notáveis ​​e suas definições:

- `gatsby-config.js` — configurar opções para um site Gatsby, com metadados para o título do projeto, descrição, plugins, etc.
- `gatsby-node.js` — implementar APIs Node.js do Gatsby para personalizar e estender as configurações padrão que afetam o processo de criação
- `gatsby-browser.js` — personalizar e estender as configurações padrão que afetam o navegador, usando as APIs do navegador do Gatsby
- `gatsby-ssr.js` — use as APIs de renderização do lado do servidor do Gatsby para personalizar as configurações padrão que afetam a renderização do lado do servidor

#### Recursos adicionais

- Para um tour por todas as pastas e arquivos comuns, leia os documentos em [Estrutura de projeto do Gatsby](/docs/gatsby-project-structure/)
- Para comandos comuns, consulte os [documentos da CLI do Gatsby](/docs/gatsby-cli)
- Confira o [Gatsby Cheat Sheet](/docs/cheat-sheet/) para obter informações para download rapidamente

### Criando páginas automaticamente

O núcleo do Gatsby transforma automaticamente os componentes do React em `src/pages` em páginas com URLs.
Por exemplo, componentes em `src/pages/index.js` e `src/pages/about.js` criariam automaticamente páginas desses nomes de arquivo para a página de índice do site (`/`) e `/about`.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- A [ILC Gatsby](/docs/gatsby-cli) instalada

#### Instruções

1. Crie um diretório para `src/pages` se o seu site ainda não tiver um.
2. Adicione um arquivo de componente ao diretório de páginas:

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

#### Recursos adicionais

- [Criando e modificando páginas](/docs/creating-and-modifying-pages/)

### Link entre páginas

O roteamento no Gatsby depende do componente `<Link />`.

#### Pré-requisitos

- Um site do Gatsby com dois componentes de página: `index.js` e `contact.js`
- O componente `<Link />` do Gatsby
- A [ILC Gatsby](/docs/gatsby-cli/) para executar `gatsby develop`

#### Instruções

1. Abra o componente da página index (`src/pages/index.js`), importe o componente `<Link />` do Gatsby, adicione um componente `<Link />` acima do cabeçalho, e dê a ele uma propriedade `to` com o valor de` "/contact/"` para o nome do caminho:

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

2. Execute `gatsby develop` e navegue até a página index. Você deve ter um link que o leve à página de contato quando clicado!

> **Nota**: O componente `<Link />` do Gatsby é um invólucro em torno do [Componente de link do `@reach/router`](https://reach.tech/router/api/Link). Para obter mais informações sobre o componente `<Link />` do Gatsby, consulte a [referência da API para `<Link />`](/docs/gatsby-link/).

### Criando um componente de layout

É comum agrupar páginas com um componente de layout React, o que possibilita o compartilhamento de marcação, estilos e funcionalidade em várias páginas.

#### Pré-requisitos

- Um site Gatsby

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

#### Recursos adicionais

- Crie um componente de layout em [tutorial, parte três](/tutorial/part-three/#your-first-layout-component)
- Estilo com [Componentes de layout](/docs/layout-components/)

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

2. Reestruture a ação `createPage` a partir das actions disponíveis, para que possa ser chamada sozinha e adicione ou obtenha dados

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

3. Faça um loop pelos dados em `gatsby-node.js` e forneça o caminho, o modelo e o contexto (dados que serão passados pageContext do props) para `createPage` para cada chamada

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

#### Recursos adicionais

- Seção do tutorial sobre [criando programaticamente páginas a partir de dados](/tutorial/part-seven/)
- Guia de referência sobre [usando o Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/)
- [Repositório de exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-createPage) para essa receita

## 2. Estilo com CSS

Existem muitas maneiras de adicionar estilos ao seu site; O Gatsby suporta quase todas as opções possíveis, através de plugins oficiais e da comunidade.

### Usando arquivos CSS globais sem um componente de Layout

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) exisente com um componente de página index
- Um arquivo `gatsby-browser.js`

#### Instruções

1. Crie um arquivo CSS global como `src/styles/global.css` e cole o seguinte no arquivo:

```css:title=src/styles/styles/global.css
html {
  background-color: lavenderblush;
}

p {
  color: maroon;
}
```

2. Importe o arquivo CSS global no arquivo `gatsby-browser.js` como o seguinte:

```javascript:gatsby-browser.js
import "./src/styles/global.css"
```

> **Nota:** Você também pode fazer uso de `require('./src/styles/global.css')` para importar o arquivo CSS global no seu arquivo `gatsby-config.js`.

3. Execute `gatsby-develop` para observar o estilo global sendo aplicado em seu site.

> **Nota:** Essa abordagem não é a mais adequada se você estiver usando CSS-in-JS para estilizar seu site. Nesse caso, uma página de layout com todos os componentes compartilhados deve ser usada. Isso é coberto na próxima receita.

#### Recursos adicionais

- Mais sobre [adicionando estilos globais sem um componente de layout](/docs/global-css/#adding-global-styles-without-a-layout-component)

### Usando estilos globais em um componente de layout

#### Pré-requisitos

- Um [ site Gatsby](/docs/quick-start/) com um componente da página index

#### Instruções

Você pode adicionar estilos globais a um [componente de layout compartilhado](/tutorial/part-three/#your-first-layout-component). Esse componente é usado para coisas comuns em todo o site, como um cabeçalho ou rodapé.

1. Se você ainda não possui um, crie um novo diretório no seu site em `/src/components`.

2. Dentro do diretório de componentes, crie dois arquivos: `layout.css` e `layout.js`.

3. Adicione o seguinte a `layout.css`:

```css:title=/src/components/layout.css
body {
  background: red;
}
```

4. Edite `layout.js` para importar o arquivo CSS e retorne a marcação do layout:

```jsx:title=/src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

5. Agora edite a página inicial do seu site em `/src/pages/index.js` e use o novo componente de layout:

```jsx:title=/src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

#### Recursos adicionais

- [Estilo padrão com arquivos CSS globais](/docs/global-css/)
- [Mais sobre componentes de layout](/tutorial/part-three)

### Usando Styled Components

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) com um componente da página index
- [gatsby-plugin-styled-components, styled-components, e babel-plugin-styled-components](/packages/gatsby-plugin-styled-components/) instalados em `package.json`

#### Instruções

1. Dentro do seu arquivo `gatsby-config.js` adicione `gatsby-plugin-styled-components`

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

2. Abra o componente da página index (`src/pages/index.js`) e importe o pacote `styled-components`

3. Estilize componentes criando blocos de estilo para cada tipo de elemento

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

4. Execute `gatsby develop` para ver as mudanças

#### Recursos adicionais

- [Mais sobre como usar Styled Components](/docs/styled-components/)
- [Aula no Egghead](https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components)

### Usando módulos CSS

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/) existente com um componente da página index

#### Instruções

1. Crie um módulo CSS como `src/pages/index.module.css` e cole o seguinte no módulo:

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

3. Execute `gatsby develop` para ver as mudanças.

**Nota:**
Observe que a extensão do arquivo é `.module.css` em vez de `.css`, o que informa ao Gatsby que este é um módulo CSS.

#### Recursos adicionais

- Mais sobre [Usando módulos CSS](/tutorial/part-two/#css-modules)
- [Exemplo ao vivo de Usando módulos CSS](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-css-modules)

### Usando Sass/SCSS

Sass é uma extensão do CSS que oferece recursos mais avançados, como regras aninhadas, variáveis, mixins e muito mais.

O Sass possui 2 sintaxes. A sintaxe mais usada é "SCSS", e é um superconjunto de CSS. Isso significa que toda sintaxe CSS válida é sintaxe SCSS válida. Os arquivos SCSS usam a extensão .scss

O Sass compilará arquivos .scss e .sass em arquivos .css para você, para que você possa escrever suas folhas de estilo com recursos mais avançados.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start/).

#### Instruções

1. Instale o plugin Gatsby [gatsby-plugin-sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/) e `node-sass`.

`npm install --save node-sass gatsby-plugin-sass`

2. Inclua o plugin no seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

3.  Escreva suas folhas de estilo como arquivos `.sass` ou `.scss` e importe eles. Se você não sabe importar estilos, dê uma olhada em [Estilizando com CSS](/docs/recipes/#2-styling-with-css)

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

_Nota: Você também pode usar arquivos Sass/SCSS como módulos, como mencionado na receita anterior sobre módulos CSS, com a diferença de que, em vez de .css, as extensões devem ser .scss ou .sass_

#### Recursos adicionais

- [Diferença entre .sass e .scss](https://responsivedesign.is/articles/difference-between-sass-and-scss/)
- [Guia Sass no site oficial do Sass](https://sass-lang.com/guide)
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

**Nota:** Verifique se o nome da fonte é referenciado no CSS relevante, por exemplo:

```css:title=src/components/layout.css
body {
  font-family: "Font Name", sans-serif;
}
```

Ao direcionar o elemento HTML `body`, sua fonte será aplicada à maioria dos textos da página. CSS adicionais podem direcionar outros elementos, como `button` ou` textarea`.

Se as fontes não estiverem atualizando seguindo as etapas acima, certifique-se de substituir a família de fontes existente no CSS relevante.

#### Recursos adicionais

- Mais sobre [importar ativos para arquivos](/docs/importing-assets-into-files/)

### Usando Emotion

[Emotion](https://emotion.sh) é uma poderosa biblioteca CSS-in-JS que suporta estilos CSS embutidos e componentes com estilo. Você pode usar cada recurso de estilo individualmente ou juntos no mesmo arquivo.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)

#### Instruções

1. Instale o [plugin Gatsby Emotion](/packages/gatsby-plugin-emotion/) e pacotes Emotion.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

2. Adicione o plugin `gatsby-plugin-emotion` ao seu arquivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

3. Se você ainda não possui uma, crie uma página no site do Gatsby em `src/pages/emotion-sample.js`.

Importar o pacote principal `css` do Emotion. Você pode usar a prop `css` para adicionar [objetos de estilos Emotion](https://emotion.sh/docs/object-styles) para qualquer elemento dentro de um componente:

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

4. Para usar os [Styled Components do Emotion](https://emotion.sh/docs/styled), importe o pacote e defina-o usando a função `styled`.

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

#### Recursos adicionais

- [Usando Emotion em Gatsby](/docs/emotion/)
- [Site do Emotion](https://emotion.sh)
- [Introdução ao Emotion e Gatsby](https://egghead.io/lessons/gatsby-getting-started-with-emotion-and-gatsby)

### Usando fontes do Google

Hospedar suas próprias [Google Fonts](https://fonts.google.com/) localmente em um projeto significa que eles não terão que ser buscados pela rede quando o site carregar, aumentando o índice de velocidade do site em até ~300 milissegundos em desktops e mais de 1 segundo em 3G. Também é recomendável limitar o uso de fontes personalizadas apenas ao essencial, pelo desempenho.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- A [ILC Gatsby](/docs/gatsby-cli/) instalada
- Escolher um pacote de fontes do [projeto typefaces](https://github.com/KyleAMathews/typefaces)

#### Instruções

1. Execute `npm install --save typeface-your-chosen-font`, substituindo `your-chosen-font` com o nome da fonte da qual você deseja instalar do [projeto typefaces](https://github.com/KyleAMathews/typefaces).

Um exemplo para carregar a popular fonte 'Source Sans Pro' seria: `npm install --save typeface-source-sans-pro`.

2. Adicione `import "typeface-your-chosen-font"` para um modelo de layout, componente de página ou `gatsby-browser.js`.

```jsx:title=src/components/layout.js
import "typeface-your-chosen-font"
```

3. Depois de importado, você pode fazer referência ao nome da fonte em uma folha de estilo CSS, módulo CSS ou CSS-in-JS.

```css:title=src/components/layout.css
body {
  font-family: "Your Chosen Font";
}
```

_NOTA: Portanto, para o exemplo acima, a declaração CSS relevante seria `font-family: 'Source Sans Pro';`_

#### Recursos adicionais

- [Typography.js](/docs/typography-js/) - Outra opção para usar fontes do Google em um site Gatsby
- [Os documentos do projeto Typefaces](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Exemplo ao vivo no blog de Kyle Mathews](https://www.bricolage.io/typefaces-easiest-way-to-self-host-fonts/)

## 3. Trabalhando com starters

[Starters](/docs/starters/) são sites Gatsby padronizados mantidos oficialmente ou pela comunidade.

### Usando um starter

#### Pré-requisitos

- A [ILC Gatsby](/docs/gatsby-cli) instalada

#### Instruções

1. Encontre o starter que você gostaria de usar. (_A [Biblioteca Starter](/starters/?v=2) é um bom lugar para procurar!_)

2. Gere um novo site com base no starter. No terminal, execute:

```shell
gatsby new {your-project-name} {link-to-starter}
```

> _Não execute o comando acima como está -- lembre-se de substituir {your-project-name} e {link-to-starter}!_

3. Execute seu novo site:

```shell
cd {your-project-name}
gatsby develop
```

#### Recursos adicionais

- Siga um [guia mais detalhado](/docs/starters/) sobre o uso de starters Gatsby.
- Aprenda a usar a ferramenta [ILC Gatsby](/docs/gatsby-cli) para usar starters em [tutorial parte um](/tutorial/part-one/#using-gatsby-starters)
- Navegue a [Biblioteca Starter](/starters/?v=2)
- Confira [starter oficial padrão](https://github.com/gatsbyjs/gatsby-starter-default) do Gatsby

## 4. Trabalhando com themes

Um theme do Gatsby abstrai a configuração do Gatsby (funcionalidade compartilhada, fonte de dados, design) em um pacote instalável. Isso significa que a configuração e a funcionalidade não são gravadas diretamente no seu projeto, mas sim versionadas, gerenciadas centralmente e instaladas como uma dependência. Você pode atualizar perfeitamente um theme, compor themes juntos e até trocar um tema compatível por outro.

- Leia mais em [O que é um Gatsby theme?](/docs/themes/what-are-gatsby-themes)

### Criando um novo site usando um theme starter

Criando um site com base em um starter que configura um theme segue o mesmo processo que a criação de um site com base em um starter que **não** configura um theme. Neste exemplo, você pode usar o [starter para criar um novo site que usa o theme do blog oficial do Gatsby](https://github.com/gatsbyjs/gatsby-starter-blog-theme).

#### Pré-requisitos

- A [ILC Gatsby](/docs/gatsby-cli) instalada

#### Instruções

1. Gere um novo site com base no theme starter do blog:

```shell
gatsby new {your-project-name} https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

2. Execute seu novo site:

```shell
cd {your-project-name}
gatsby develop
```

#### Recursos adicionais

- Aprenda a usar um theme Gatsby existente no [guia conceitual mais curto](/docs/themes/using-a-gatsby-theme) ou o mais detalhado no [tutorial passo a passo](/tutorial/using-a-theme).

### Construindo um novo theme

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-the-gatsby-theme-workspace-starter-to-begin-building-a-new-theme"
  lessonTitle="Use a área de trabalho Gatsby Theme Starter para começar a construir um novo Theme"
/>

#### Pré-requisitos

- A [ILC Gatsby](/docs/gatsby-cli) instalada

* [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) installed

#### Instruções

1. Gere uma nova área de trabalho de theme usando a [área de trabalho do starter Gatsby theme](https://github.com/gatsbyjs/gatsby-starter-theme-workspace):

```shell
gatsby new {your-project-name} https://github.com/gatsbyjs/gatsby-starter-theme-workspace
```

2. Execute o site de exemplo na área de trabalho:

```shell
yarn workspace example develop
```

#### Recursos adicionais

- Siga um [guia mais detalhado](/docs/themes/building-themes/) sobre o uso da área de trabalho do Gatsby starter theme.
- Aprenda a criar seu próprio theme no [Curso de criação de Gatsby Theme em vídeo no Egghead](https://egghead.io/courses/gatsby-theme-authoring), ou no [companheiro de tutorial complementar escrito do curso em vídeo](/tutorial/building-a-theme).

## 5. Obtendo Dados

A fonte de dados no Gatsby é orientada por plug-ins; Os plugins de origem buscam dados de sua origem (por exemplo, o plugin `gatsby-source-filesystem` busca dados do sistema de arquivos, o plugin `gatsby-source-wordpress` busca dados da API do WordPress, etc). Você também pode obter os dados você mesmo.

### Adicionando dados ao GraphQL

[A camada de dados GraphQL](/docs/querying-with-graphql/) do Gatsby usa nós para modelar pedaços de dados. Os plugins de origem do Gatsby adicionam nós de origem que você pode consultar, mas você também pode criar nós de origem. Para adicionar dados personalizados à camada de dados do GraphQL, o Gatsby fornece métodos que você pode aproveitar.

Esta receita mostra como adicionar dados personalizados usando `createNode()`.

#### Instruções

1. No `gatsby-node.js` use `sourceNodes()` e `actions.createNode()` para criar e exportar nós para poder consultar os dados.

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

3. Consulte os dados (no GraphiQL oo nos seus componentes).

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

#### Recursos adicionais

- Percorra um exemplo usando o plugin `gatsby-source-filesystem` no [tutorial parte cinco](/tutorial/part-five/#source-plugins)
- Pesquise plugins de origem disponíveis na [biblioteca Gatsby](/plugins/?=source)
- Entenda os plugins de origem criando um no [tutorial do plugin de fonte Pixabay](/docs/pixabay-source-plugin-tutorial/)
- A [documentação](/docs/actions/#createNode) da função createNode

### Fornecendo dados de Markdown para postagens e páginas de blog com GraphQL

Você pode obter dados do Markdown e usar a [API `createPages`](/docs/actions/#createPage) do Gatsby para criar páginas dinamicamente.

This recipe shows how to create pages from Markdown files on your local filesystem using Gatsby's GraphQL data layer.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start) com um arquivo `gatsby-config.js`
- A [ILC Gatsby] (/docs/gatsby-cli) instalada
- O [plugin gatsby-source-filesystem](/packages/gatsby-source-filesystem) instalado
- O [plugin gatsby-transformer-remark](/packages/gatsby-transformer-remark) instalado
- Um arquivo `gatsby-node.js`

#### Instruções

1. No `gatsby-config.js`, configure `gatsby-transformer-remark` junto com o `gatsby-source-filesystem` para extrair arquivos Markdown de uma pasta de origem. Isso seria um acréscimo a quaisquer entradas anteriores do `gatsby-source-filesystem`, como para imagens:

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

2. Adicione uma postagem do Markdown ao `src/content`, incluindo frontmatter para o título, data e caminho, com algum conteúdo inicial para o corpo da postagem:

```markdown:title=src/content/my-first-post.md
---
title: My First Post
date: 2019-07-10
path: /my-first-post
---

This is my first Gatsby post written in Markdown!
```

3. Inicie o servidor de desenvolvimento com `gatsby develop`, navegue até o GraphiQL explorer em `http://localhost:8000/___graphql` e escreva uma consulta para obter todos os dados de remarcação:

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
  title="Consulta para todas as Markdowns"
  src="https://q4xpb.sse.codesandbox.io/___graphql?explorerIsOpen=false&query=%7B%0A%20%20allMarkdownRemark%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D"
  width="600"
  height="300"
/>

4. Adicione o código JavaScript para gerar páginas a partir das postagens do Markdown no momento da construção, copiando a consulta GraphQL para `gatsby-node.js` e fazendo um loop pelos resultados:

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

6. Execute `gatsby develop` para reiniciar o servidor de desenvolvimento. Veja sua postagem no navegador: `http://localhost:8000/my-first-post`

#### Recursos adicionais

- [Tutorial: Crie páginas programaticamente a partir de dados](/tutorial/part-seven/)
- [Criando e modificando páginas](/docs/creating-and-modifying-pages/)
- [Adicionando páginas Markdown](/docs/adding-markdown-pages/)
- [Guia para criar páginas de dados programaticamente](/docs/programmatically-create-pages-from-data/)
- [Repositório de exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-sourcing-markdown) para esta receita

### Puxando dados de uma fonte externa e criando páginas sem o GraphQL

Você não precisa usar a camada de dados do GraphQL para incluir dados nas páginas, [embora haja razões para considerar o GraphQL](/docs/why-gatsby-uses-graphql/). Você pode usar o nó da API do `createPages` para extrair dados não estruturados diretamente nos sites do Gatsby, em vez de usar o GraphQL e os plugins de origem.

Nesta receita, você criará páginas dinâmicas a partir de dados buscados nos [pontos de extremidade REST da PokéAPI](https://www.pokeapi.co/). O [exemplo completo](https://github.com/jlengstorf/gatsby-with-unstructured-data/) pode ser encontrado em GitHub.

#### Pré-requisitos

- Um site Gatsby com um arquivo `gatsby-node.js`
- A [ILC Gatsby](/docs/gatsby-cli) instalada
- O pacote [axios](https://www.npmjs.com/package/axios) instalado através do npm

#### Instruções

1. Em `gatsby-node.js`, adicione o código JavaScript para buscar dados da PokéAPI e crie programaticamente uma página de índice:

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

#### Recursos adicionais

- [Repo completo de dados de Pokemon](https://github.com/jlengstorf/gatsby-with-unstructured-data/)
- Mais sobre o uso de dados não estruturados em [Usando o Gatsby sem GraphQL](/docs/using-gatsby-without-graphql/)
- Quando e como [consultar dados com o GraphQL](/docs/querying-with-graphql/) para sites mais complexos de Gatsby

### Obtendo conteúdo do Drupal

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Um site [Drupal](http://drupal.org)
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
        apiBase: `api`, // optional, defaults to `jsonapi`
      },
    },
  ],
}
```

3. Inicie o servidor de desenvolvimento com `gatsby develop` e abra o explorador GraphiQL em `http://localhost:8000/___graphql`. Na guia Explorer, você verá novos tipos de nós, como `allBlockBlock` para blocos Drupal, e um para cada tipo de conteúdo no site Drupal. Por exemplo, se você tiver um tipo de conteúdo "Page", ele estará disponível como `allNodePage`. Para consultar todos os nós "Page" por seu título e corpo, use uma consulta como:

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

4. Para usar seus dados do Drupal, crie uma nova página no seu site do Gatsby em `src/pages/drupal.js`. Esta página listará todos os nós da "Página" do Drupal.

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

#### Recursos adicionais

- [Usando Drupal desacoplado com Gatsby](/blog/2018-08-13-using-decoupled-drupal-with-gatsby/)
- [Mais informações sobre o Drupal](/docs/sourcing-from-drupal)
- [Tutorial: Crie páginas programaticamente a partir de dados](/tutorial/part-seven/)

## 6. Consultando dados

### Consultando dados com uma Consulta de Página

Você pode usar a tag `graphql` para consultar dados nas páginas do seu site do Gatsby. Isso fornece acesso a qualquer coisa incluída na camada de dados do Gatsby, como metadados do site, plugins de origem, imagens e muito mais.

#### Instruções

1. Importe `graphql` de `gatsby`.

2. Exporte uma constante chamada `query` e defina seu valor como um modelo `graphql` com a consulta entre dois acentos graves.

3. Passe `data` como prop ao componente.

4. A variável `data` contém os dados consultados e pode ser referenciada em JSX para gerar HTML.

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

#### Recursos adicionais

- [GraphQL e Gatsby](/docs/graphql/): Entendendo a forma esperada dos seus dados
- [Mais sobre como consultar dados em páginas com o GraphQL](/docs/page-query/)
- [MDN sobre template literals com tags](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/template_strings) como os usados ​​no GraphQL

### Consultando dados com o componente StaticQuery 

`StaticQuery` é um componente para recuperar dados da camada de dados do Gatsby em [componentes que não são de página](/docs/static-query/), como um cabeçalho, navegação ou qualquer outro componente filho.

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

2. You can now use this component as you would [any other component](/docs/building-with-components#non-page-components) by importing it into a larger page of JSX components and HTML markup.

### Consultando dados com o hook useStaticQuery

Desde o Gatsby v2.1.0, você pode usar o hook `useStaticQuery` para consultar dados com uma função JavaScript em vez de um componente. A sintaxe elimina a necessidade de um componente `<StaticQuery>` para agrupar tudo, o que algumas pessoas acham mais simples de escrever.

O hook `useStaticQuery` pega uma consulta GraphQL e retorna os dados solicitados. Ele pode ser armazenado em uma variável e usado posteriormente em seus modelos JSX.

#### Pré-requisitos

- Você precisará do React e ReactDOM 16.8.0 ou posterior (manter o Gatsby atualizado lida com isso)
- Leitura recomendada: as [Regras dos Hooks do React](https://pt-br.reactjs.org/docs/hooks-rules.html)

#### Instruções

1. Importe `useStaticQuery` e `graphql` de `gatsby` para usar o gancho para consultar os dados.

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

#### Recursos adicionais

- [Mais sobre Static Query para consultar dados em componentes](/docs/static-query/)
- [A diferença entre uma static query e uma page query](/docs/static-query/#how-staticquery-differs-from-page-query)
- [Mais sobre o hook useStaticQuery](/docs/use-static-query/)
- [Visualize seus dados com o GraphiQL](/docs/introducing-graphiql/)

### Limitando com GraphQL

Ao consultar dados com o GraphQL, você pode limitar o número de resultados retornados com um número específico. Isso é útil se você precisar de apenas alguns dados ou [paginar dados](/docs/adding-pagination/).

Para limitar os dados, você precisará de um site Gatsby com alguns nós na camada de dados GraphQL. Todos os sites têm alguns nós como `allSitePage` e `sitePage` criados automaticamente: mais pode ser adicionado instalando plugins de origem como `gatsby-source-filesystem` em `gatsby-config.js`.

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

#### Recursos adicionais

- Saiba mais sobre [nós na API de dados GraphQL de Gatsby](/docs/node-interface/)
- [Gatsby GraphQL reference for limiting](/docs/graphql-reference/#limit)
- Live example:

<iframe
  title="Limitando dados retornados"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(limit%3A%203)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Classificando com GraphQL

A ordem dos seus resultados pode ser especificada com o argumento `sort` do GraphQL. Você pode especificar em quais campos classificar e a ordem em que serão classificados.

Para esta receita, você precisará de um site Gatsby com uma coleção de nós para classificar na camada de dados GraphQL. Todos os sites têm alguns nós como o `allSitePage` criados automaticamente: mais podem ser adicionados instalando plugins de origem.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Campos consultáveis ​​prefixados com `all`, por exemplo `allSitePage`

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o explorador GraphiQL em uma guia do navegador em: `http://localhost:8000/___graphql`
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

4. Adicione um argumento `sort` ao campo `allSitePage` e atribua a ele um objeto com os atributos `fields` e `order`. O valor para `fields` pode ser um campo ou uma matriz de campos para classificar (este exemplo usa o campo `path`); a `order` pode ser `ASC` ou `DESC` para ascensão e descida, respectivamente.

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

#### Recursos adicionais

- [Referência do Gatsby GraphQL para classificação](/docs/graphql-reference/#sort)
- Aprenda sobre [nós na API de dados GraphQL de Gatsby](/docs/node-interface/)
- Exemplo ao vivo:

<iframe
  title="Classificação de dados"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(sort%3A%20%7Bfields%3A%20path%2C%20order%3A%20ASC%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Filtrando com GraphQL

Os resultados consultados podem ser filtrados com operadores como `eq` (igual), `ne` (não igual), `in` e  `regex` em campos especificados.

Para esta receita, você precisará de um site Gatsby com uma coleção de nós para filtrar na camada de dados GraphQL. Todos os sites têm alguns nós, como o `allSitePage`, criados automaticamente: mais podem ser adicionados ao instalar plugins de origem e transformador, como `gatsby-source-filesystem` e `gatsby-transformer-remark` em `gatsby-config.js` para produzir `allMarkdownRemark`.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- Campos consultáveis ​​prefixados com `all`, por exemplo `allSitePage` ou `allMarkdownRemark`

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o explorador GraphiQL em uma guia do navegador em: `http://localhost:8000/___graphql`
3. Adicione uma consulta no editor usando um campo prefixado por 'all', como `allMarkdownRemark` (o que significa que ele retornará uma lista de nós)

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

4. Adicione um argumento `filter` ao campo `allMarkdownRemark` e atribua a ele um objeto com os campos pelos quais você deseja filtrar. Neste exemplo, o conteúdo do Markdown é filtrado pelo atributo `categories` nos metadados do frontmatter. O próximo valor é o operador: neste caso, `eq`, ou igual a, com um valor de 'magical creatures'.

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

5. Clique no botão play na página GraphiQL. Os dados que correspondem aos parâmetros do filtro devem ser retornados; nesse caso, apenas os arquivos Markdown de origem marcados com uma categoria de'magical creatures'.

#### Recursos adicionais

- [Referência do Gatsby GraphQL para filtragem](/docs/graphql-reference/#filter)
- [Lista completa de possíveis operadores](/docs/graphql-reference/#complete-list-of-possible-operators)
- Aprenda sobre [nós na API de dados GraphQL de Gatsby](/docs/node-interface/)
- Exemplo ao vivo:

<iframe
  title="Filtrando dados"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allMarkdownRemark(filter%3A%20%7Bfrontmatter%3A%20%7Bcategories%3A%20%7Beq%3A%20%22magical%20creatures%22%7D%7D%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20categories%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Aliases de consulta do GraphQL

Você pode renomear qualquer campo em uma consulta GraphQL com um alias.

Se você deseja executar duas consultas na mesma fonte de dados, pode usar um alias para evitar uma colisão de nomes com duas consultas com o mesmo nome.

#### Instruções

1. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
2. Abra o explorador GraphiQL em uma guia do navegador em: `http://localhost:8000/___graphql`
3. Adicione uma consulta no editor usando dois campos com o mesmo nome, como `allFile`

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

4. Adicione o nome que você gostaria de usar para qualquer campo antes do nome do campo no esquema do GraphQL, separado por dois pontos. (Por exemplo, `[alias-name]: [original-name]`)

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

#### Recursos adicionais

- [Referência do Gatsby GraphQL para fazer alias](/docs/graphql-reference/#aliasing)
- Exemplo ao vivo:

<iframe
  title="Usando aliases"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20fileCount%3A%20allFile%20%7B%20%0A%20%20%20%20totalCount%0A%20%20%7D%0A%20%20filePageInfo%3A%20allFile%20%7B%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20currentPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Fragmentos de Consulta GraphQL

Os fragmentos do GraphQL são pedaços compartilháveis ​​de uma consulta que pode ser reutilizada.

Você pode usá-los para compartilhar vários campos entre as consultas ou para colocar um componente nos dados que ele usa.

#### Instruções

1. Declare uma string de modelo `graphql` com um fragmento nela. O fragmento deve ser composto da palavra-chave `fragment`, um nome, o tipo GraphQL ao qual está associado (neste caso do tipo `Site`, conforme demonstrado por `on Site`), e os campos que compõem o fragmento:

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

2. Agora, inclua o fragmento em uma consulta para um campo do tipo especificado pelo fragmento. Isso inclui esses campos sem precisar declará-los todos independentemente:

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

Fragmentos podem ser aninhados dentro de outros fragmentos e vários fragmentos podem ser usados ​​na mesma consulta.

#### Recursos adicionais

- [Simples exemplo de repositório usando fragmentos](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-fragments)
- [Referência do Gatsby GraphQL para fragmentos](/docs/graphql-reference/#fragments)
- [Fragmentos de imagem de Gatsby](/docs/gatsby-image/#image-query-fragments)
- [Exemplo de repo com dados co-localizados](https://github.com/gatsbyjs/gatsby/tree/master/examples/gatsbygram)

## 7. Trabalhando com imagens

### Importar uma imagem para um componente com o webpack

As imagens podem ser importadas diretamente para um módulo JavaScript com o webpack. Esse processo reduz e copia automaticamente a imagem para a pasta `public` do seu site, fornecendo uma URL de imagem dinâmica para você passar para um elemento HTML `<img>` como um caminho de arquivo comum.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-import-a-local-image-into-a-gatsby-component-with-webpack"
  lessonTitle="Importar uma imagem local para um componente Gatsby com webpack"
/>

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start) com um arquivo `.js` exportando um componente React
- Uma imagem (`.jpg`, `.png`, `.gif`, `.svg`, etc.) na pasta `src`

#### Instruções

1. Importe o caminho do seu arquivo em relação a pasta `src`:

```jsx:title=src/pages/index.js
import React from "react"
// Informa ao webpack que este arquivo JS usa esta imagem
import FiestaImg from "../assets/fiesta.jpg" // highlight-line
```

2. No `index.js`, adicione uma tag `<img>` com o `src` como o nome da importação que você usou do webpack (nesse caso `FiestaImg`), e adicione um atributo `alt` [descrevendo a imagem](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"
import FiestaImg from "../assets/fiesta.jpg"

export default () => (
  // O resultado da importação é o URL da sua imagem
  <img src={FiestaImg} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
4. Veja sua imagem no navegador: `http://localhost:8000/`

#### Recursos adicionais

- [Exemplo de repositório importando uma imagem com o webpack](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-webpack-image)
- [Mais sobre todas as técnicas de imagem em Gatsby](/docs/images-and-files/)

### Referencie uma imagem da pasta `static`

Como alternativa à importação de ativos com o webpack, a pasta `static` permite o acesso ao conteúdo que é automaticamente copiado para a pasta `public` quando o site é criado.

Isto é uma **rota de fuga** para [casos de uso específicos](/docs/static-folder/#when-to-use-the-static-folder), e outros métodos como [importando com o webpack](#import-an-image-into-a-component-with-webpack) são recomendados para aproveitar as otimizações feitas pelo Gatsby.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-a-local-image-from-the-static-folder-in-a-gatsby-component"
  lessonTitle="Use uma imagem local da pasta estática em um componente Gatsby"
/>

#### Pré-requisitos

- Um [Site Gatsby](/docs/quick-start) com um arquivo `.js` exportando um componente  React
- Uma imagem (`.jpg`, `.png`, `.gif`, `.svg`, etc.) na pasta `static`

#### Instruções

1. Certifique-se de que a imagem esteja na sua pasta `static` na raiz do projeto. A estrutura do seu projeto pode ser algo como isto:

```
├── gatsby-config.js
├── src
│   └── pages
│       └── index.js
├── static
│       └── fiesta.jpg
```

2. No `index.js`, adicione uma tag `<img>` com o `src` como o caminho relativo do arquivo da pasta `static`, e adicione um atributo `alt` [descrevendo a imagem](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <img src={`fiesta.jpg`} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Execute `gatsby develop` para iniciar o servidor de desenvolvimento.
4. Veja sua imagem no navegador:`http://localhost:8000/`

#### Recursos adicionais

- [Exemplo de repositório referenciando uma imagem da pasta estática](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-static-image)
- [Usando a Pasta Static](/docs/static-folder/)
- [Mais sobre todas as técnicas de imagem em Gatsby](/docs/images-and-files/)

### Otimizando e consultando imagens locais com gatsby-image

O plugin `gatsby-image` pode aliviar grande parte da dor associada à otimização de imagens no seu site.

O Gatsby irá gerar recursos otimizados que podem ser consultados com o GraphQL e passados ​​para o componente de imagem do Gatsby. Isso cuida do trabalho pesado, incluindo a criação de vários tamanhos de imagem e o carregamento no momento certo.

#### Pré-requisitos

- Os pacotes `gatsby-image`, `gatsby-transformer-sharp` e `gatsby-plugin-sharp` instalados e adicionados ao array de plugins em `gatsby-config`
- [Imagens obtidas](/packages/gatsby-image/#install) no seu `gatsby-config` usando um plugin como `gatsby-source-filesystem`

#### Instruções

1. Primeiro, importe `Img` de `gatsby-image`, bem como `graphql` e `useStaticQuery` de `gatsby`

```jsx
import { useStaticQuery, graphql } from "gatsby" // para consultar dados de imagem
import Img from "gatsby-image" // para pegar dados de imagem e renderizá-los
```

2. Escreva uma consulta para obter dados da imagem e passe os dados para o componente `<Img />`:

Escolha qualquer uma das seguintes opções ou uma combinação delas.

a. uma única imagem consultada por seu [caminho de arquivo](/docs/content-and-data/) (Exemplo: `images/corgi.jpg`)

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

b. usando um [fragmento GraphQL](/docs/using-fragments/), para consultar os campos necessários de forma mais concisa

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

c. várias imagens de um diretório (Exemplo: `images/dogs`) [filtradas](/docs/graphql-reference/#filter) pelos campos `extension` e `relativeDirectory`, e depois mapeado para os componentes `Img`

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

**Nota**: Este método pode dificultar a correspondência de imagens com o texto `alt` para acessibilidade. Este exemplo usa imagens com o texto `alt` incluído no nome do arquivo, como `dog in a party hat.jpg`.

d. uma imagem de tamanho fixo usando o campo `fixed` em vez de `fluid`

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

e. uma imagem de tamanho fixo com um `maxWidth`

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

f. uma imagem preenchendo um recipiente de fluido com uma largura máxima (em pixels) e uma qualidade mais alta (o valor padrão é 50, ou seja, 50%)

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

3. (Opcional) Adicione estilos embutidos ao `<Img />` como faria com outros componentes

```jsx
<Img
  fluid={data.file.childImageSharp.fluid}
  alt="A corgi smiling happily"
  style={{ border: "2px solid rebeccapurple", borderRadius: 5, height: 250 }} // highlight-line
/>
```

4. (Opcional) Forçar uma imagem na proporção desejada, substituindo o campo `aspectRatio` retornado pela consulta GraphQL antes de ser transmitida para o componente `<Img /> `

```jsx
<Img
  fluid={{
    ...data.file.childImageSharp.fluid,
    aspectRatio: 1.6, // 1280 / 800 = 1.6
  }}
  alt="A corgi smiling happily"
/>
```

5. Execute `gatsby develop`, para gerar imagens de arquivos no sistema de arquivos (se ainda não o tiver feito) e armazená-las em cache

#### Recursos adicionais

- [Repositório de exemplo ilustrando estes exemplos](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [API de imagem do Gatsby](/docs/gatsby-image/)
- [Usado Gatsby Image](/docs/using-gatsby-image)
- [Mais sobre como trabalhar com imagens em Gatsby](/docs/working-with-images/)
- [Vídeos gratuitos do egghead.io explicando essas etapas](https://egghead.io/playlists/using-gatsby-image-with-gatsby-ea85129e)

### Otimizando e consultando imagens no pós frontmatter com gatsby-image

Para casos de uso como uma imagem em destaque em uma postagem de blog, você _ainda_ pode usar `gatsby-image`. O componente `Img` precisa de dados de imagem processados, que podem vir de um arquivo local (ou remoto), incluindo de uma URL no frontmatter de um arquivo `.md` ou `.mdx`.

Para embutir imagens no markdown (usando a sintaxe `![]()`), considere usar um plugin como [`gatsby-remark-images`](/packages/gatsby-remark-images/)

#### Pré-requisitos

- Os pacotes `gatsby-image`, `gatsby-transformer-sharp` e `gatsby-plugin-sharp` instalados e adicionados ao array de plugins em `gatsby-config`
- [Imagens obtidas](/packages/gatsby-image/#install) no seu `gatsby-config` usando um plugin como `gatsby-source-filesystem`
- Arquivos markdown originados em seu `gatsby-config` com URLs de imagem no frontmatter
- [Páginas criadas](/docs/creating-and-modifying-pages/) de Markdown usando [`createPages`](https://www.gatsbyjs.org/docs/node-apis/#createPages)

#### Instruções

1. Verifique se o arquivo Markdown tem um URL de imagem com um caminho válido para um arquivo de imagem no seu projeto

```mdx:title=post.mdx
---
title: My First Post
featuredImage: ./corgi.png // highlight-line
---

Post content...
```

2. Verifique se um identificador exclusivo (um slug neste exemplo) é passado no contexto quando `createPages` é chamado em `gatsby-node.js`, que posteriormente será passado para uma consulta GraphQL no componente Layout

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  // consulta para todas as markdowns

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

3. Agora, importe `Img` de `gatsby-image` e `graphql` de `gatsby` para o componente do modelo, escreva uma [pageQuery](/docs/page-query/) para obter dados de imagem com base nos dados passados ​​no `slug` e passar esses dados para o componente `<Img /> `:

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

4. Execute `gatsby develop`, que irá gerar imagens para os arquivos originados no sistema de arquivos

#### Recursos adicionais

- [Exemplo de repositório usando esta receita](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [Imagens em destaque com frontmatter](/docs/working-with-images-in-markdown/#featured-images-with-frontmatter-metadata)
- [API Gatsby Image](/docs/gatsby-image/)
- [UsandoGatsby Image](/docs/using-gatsby-image)
- [Mais sobre como trabalhar com imagens em Gatsby](/docs/working-with-images/)

## 8. Transformando dados

A transformação de dados no Gatsby é orientada por plugins. Os plugins transformadores obtêm os dados buscados usando os plugins de origem e os transformam em algo mais utilizável (por exemplo. JSON em objetos JavaScript e muito mais).

### Transformandp Markdown em HTML

O plugin `gatsby-transformer-remark` pode transformar arquivos Markdown em HTML.

#### Pré-requisitos

- Um site de Gatsby com `gatsby-config.js` e uma página `index.js`
- Um arquivo Markdown salvo no diretório `src` do seu site Gatsby
- Um plugin de origem instalado, como `gatsby-source-filesystem`
- O plugin `gatsby-transformer-remark` instalado

#### Instruções

1. Adicione o plugin transformador no seu `gatsby-config.js`:

```js:title=gatsby-config.js
plugins: [
  // não mostrado: gatsby-source-filesystem para criar nós para transformar
  `gatsby-transformer-remark`
],
```

2. Adicione uma consulta GraphQL ao arquivo `index.js` do seu site Gatsby para buscar os nós `MarkdownRemark`:

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

3. Reinicie o servidor de desenvolvimento e abra o GraphiQL em `http://localhost:8000/___graphql`. Explore os campos disponíveis no nó `MarkdownRemark`.

#### Recursos adicionais

- [Tutorial sobre como transformar Markdown em HTML](/tutorial/part-six/#transformer-plugins) usando `gatsby-transformer-remark`
- Procure plugins transformadores disponíveis na [biblioteca de plugins do Gatsby](/plugins/?=transformer)

## 9. Implantando seu site

Hora de mostrar. Quando estiver satisfeito com o seu site, você estará pronto para publicá-lo!

### Preparando para implantação

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start)
- A [ILC Gatsby](/docs/gatsby-cli) instalada

#### Instruções

1. Pare o servidor de desenvolvimento se estiver em execução (`Ctrl + C` na sua linha de comando na maioria dos casos)

2. Para o caminho padrão do site no diretório raiz (`/`), execute `gatsby build` usando a ILC do Gatsby na linha de comandos. Os arquivos construídos estarão agora na pasta `public`.

```shell
gatsby build
```

3. Para incluir um caminho de site diferente de `/` (tal como `/site-name/`), defina um prefixo de caminho adicionando o seguinte ao seu `gatsby-config.js` e substituindo `yourpathprefix` pelo prefixo do caminho desejado:

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/yourpathprefix`,
}
```

Existem algumas razões para fazer isso -- por exemplo, hospedar um blog criado com o Gatsby em um domínio com outro site não criado no Gatsby. O site principal direcionaria para `example.com`, e o site Gatsby com um prefixo de caminho poderia morar em `example.com/blog`.

4. Com um prefixo de caminho definido em `gatsby-config.js`, execute `gatsby build` com a flag `--prefix-paths` para adicionar automaticamente o prefixo ao início de todos os URLs do site Gatsby e tags `<Link>`.

```shell
gatsby build --prefix-paths
```

5. Certifique-se de que o seu site tenha a mesma aparência ao executar o `gatsby build` como no `gatsby develop`. Executando `gatsby serve` ao criar seu site, você pode testar (e depurar, se necessário) o produto final antes de implantá-lo ao vivo.

```shell
gatsby build && gatsby serve
```

#### Recursos adicionais

- Caminho para criação e implantação de um site de exemplo no [tutorial parte um](/tutorial/part-one/#deploying-a-gatsby-site)
- Aprenda sobre [otimização de desempenho](/docs/performance/)
- Leia sobre [outros tópicos relacionados à implantação](/docs/preparing-for-deployment/)
- Confira os [documentos de implantação](/docs/deploying-and-hosting/) para plataformas de hospedagem específicas e como implantar nelas

### Implantando em Netlify

Use [`netlify-cli`](https://www.netlify.com/docs/cli/) para implantar seu aplicativo Gatsby sem sair da interface da linha de comandos.

#### Pré-requisitos

- Um [site Gatsby](/docs/quick-start) com um único componente `index.js`
- O pacote [netlify-cli](https://www.npmjs.com/package/netlify-cli) instalado
- A [ILC Gatsby](/docs/gatsby-cli) instalada

#### Instruções

1. Crie seu aplicativo gatsby usando `gatsby build`

2. Entre no Netlify usando `netlify login`

3. Execute o comando `netlify init`. Selecione a opção "Create & configure a new site".

4. Escolha um nome de site personalizado, se desejar, ou pressione enter para receber um nome aleatório.

5. Escolha seu [Team](https://www.netlify.com/docs/teams/).

6. Mude o caminho de implantação para `public/`

7. Verifique se tudo está bem antes de implantar na produção usando `netlify deploy --prod`

#### Recursos adicionais

- [Hospedagem em Netlify](/docs/hosting-on-netlify)
- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify)

### Implantando em ZEIT Now

Use [Now CLI](https://zeit.co/download) para implantar seu aplicativo Gatsby sem sair da interface da linha de comandos.

#### Pré-requisitos

- Uma conta [ZEIT Now](https://zeit.co/signup)
- Um [site Gatsby](/docs/quick-start) com um único componente `index.js`
- Pacote [Now CLI](https://zeit.co/download) instalado
- [ILC Gatsby](/docs/gatsby-cli) instalado

#### Instruções

1. Faça login na Now CLI usando `now login`

2. Mude para o diretório do seu aplicativo Gatsby.js no Terminal se você ainda não estiver lá

3. Execute `now` para implementá-lo

#### Recursos adicionais

- [Implantando em ZEIT Now](/docs/deploying-to-zeit-now/)
