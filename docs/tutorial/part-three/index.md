---
title: Creating Nested Layout Components
typora-copy-images-to: ./
disableTableOfContents: true
---

Boas-vindas a parte três!

## O que veremos nesse tutorial?

Nessa parte, você irá aprender sobre plugins do Gatsby e como criar componentes de layout.

Plugins do Gatsby são pacotes JavaScript que ajudam a adicionar funcionalidades a um site Gatsby. O Gatsby foi projetado para ser extensível, o que significa que os plugins podem estender e modificar praticamente qualquer coisa que o Gatsby faz.

Componentes de layout são para seções do seu site que você quer compartilhar entre diversas páginas. Por exemplo, normalmente sites tem componentes de layout para um cabeçalho e rodapé que são compartilhados. Outras coisas comuns de se adicionar em um layout são _sidebars_ e/ou menu de navegação. Nesta página, por exemplo, o cabeçalho no topo é parte de um componente de layout do gatsbyjs.org.

Vamos nos aprofundar na parte três.

## Usando plugins

Você provavelmente tem familiaridade com o conceito de plugins. Diversos sistemas de software suportam adição de plugins customizados para acrescentar novas funcionalidades ou, até mesmo, modificar o funcionamento interno do software. Os plugins do Gatsby funcionam da mesma maneira.

Membros da comunidade (como você!) podem contribuir com plugins (pequenas quantidades de código JavaScript) que outros podem utilizar quando estiverem construindo sites com Gatsby.

> Existem centenas de plugins! Explore a [Biblioteca de Plugins](/plugins) do Gatsby.

Nosso objetivo com plugins é que eles sejam simples de instalar e utilizar. Provavelmente você irá utilizar plugins em quase todos os sites Gatsby que você for construir. Enquanto você estiver percorrendo o restante do tutorial você terá muitas oportunidades para praticar a instalação e utilização de plugins.

Para uma introdução inicial em como utilizar plugins, vamos instalar e implementar o plugin Gatsby para Typography.js

[Typography.js](https://kyleamathews.github.io/typography.js/) é uma biblioteca JavaScript que gera estilos base de tipografia para o seu site. A biblioteca tem um [plugin Gatsby correspondente](/packages/gatsby-plugin-typography/) para simplificar o seu uso em um site Gatsby.

### ✋ Criar um novo site Gatsby

Como mencionamos na [parte dois](/tutorial/part-two/), a partir desse ponto é, provavelmente, uma boa ideia fechar as janelas do terminal e os arquivos das partes anteriores do tutorial, de modo que as coisas mantenham-se organizadas na sua área de trabalho. Em seguida, abra uma nova janela do terminal e execute os seguintes comandos para criar um novo site Gatsby em um novo diretório chamado `tutorial-part-three` e entrar nesse diretório.

```shell
gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-three
```

### ✋ Instalar e configurar o `gatsby-plugin-typography`

Há dois passos principais para utilização de um plugin: Instalação e configuração.

1. Instale o pacote do NPM `gatsby-plugin-typography`.

```shell
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> Nota: Typography.js precisa de alguns pacotes adicionais, então esses pacotes foram incluídos nas instruções. Requisitos adicionais como esse serão listados nas instruções de "instalação" de cada plugin.

2. Modifique o arquivo `gatsby-config.js` na raíz do seu projeto para o seguinte:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

O `gatsby-config.js` é outro arquivo especial que o Gatsby irá reconhecer automaticamente. É nesse arquivo que você adiciona plugins e outras configurações do site.

> Se deseja saber mais, confira a [documentação sobre gatsby-config.js](/docs/gatsby-config/).

3. Typography.js precisa de um arquivo de configuração. Crie uma nova pasta chamada `utils` dentro da pasta `src`. Em seguida, adicione um novo arquivo chamado `typography.js` na pasta `utils` e copie o seguinte conteúdo para dentro do arquivo:

```javascript:title=src/utils/typography.js
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

4. Inicie o servidor de desenvolvimento.

```shell
gatsby develop
```

Assim que você carregar o site, se você inspecionar o HTML gerado utilizando as ferramentas de desenvolvedor do Chrome, você verá que o plugin de tipografia adicionou um elemento `<style>` no elemento`<head>` com o CSS que foi gerado:

![typography-styles](typography-styles.png)

### ✋ Faça mudanças de conteúdo e estilo

Copie o código a seguir para o seu `src/pages/index.js` de forma que você visualize melhor os efeitos do CSS gerado pelo Typography.js

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

Agora seu site deve se parecer com isso:

![no-layout](no-layout.png)

Vamos fazer uma pequena melhoria. Muitos sites tem uma coluna única de texto centralizadas no centro da página. Para criar isso adicione os seguintes estilos na
`<div>` em `src/pages/index.js`.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  // highlight-next-line
  <div style={{ margin: `3rem auto`, maxWidth: 600 }}>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

![with-layout2](with-layout2.png)

Maravilha. Você instalou e configurou seu primeiríssimo plugin do Gatsby!

## Criando componentes de layout

Agora vamos aprender sobre componentes de layout. Para se preparar para essa parte, adicione algumas novas páginas no seu projeto: uma página _sobre_ e uma página de _contato_

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div>
    <h1>About me</h1>
    <p>I’m good enough, I’m smart enough, and gosh darn it, people like me!</p>
  </div>
)
```

```jsx:title=src/pages/contact.js
import React from "react"

export default () => (
  <div>
    <h1>I'd love to talk! Email me at the address below</h1>
    <p>
      <a href="mailto:me@example.com">me@example.com</a>
    </p>
  </div>
)
```

Vamos ver como a nova página _sobre_ ficou:

![about-uncentered](about-uncentered.png)

Hmm. Seria legal se o conteúdo das duas páginas fossem centralizados como na página inicial. E também serial legal se tivéssemos alguma navegação global, facilitando que os novos visitantes encontrem e visitem as outras páginas.

Você irá realizar essas mudanças criando seu primeiro componente de layout

### ✋ Crie seu primeiro componente de layout

1. Crie um novo diretório em `src/components`.

2. Crie um componente, bem básico, de layout em `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

3. Importe esse componente de layout novo no seu componente de página `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </Layout> {/* highlight-line */}
)
```

![with-layout2](with-layout2.png)

Que ótimo, o layout está funcionando! O conteúdo da sua página inicial ainda está centralizado.

Mas tente navegar para `/about/`, ou `/contact`. O conteúdo nessas páginas não estão centralizados ainda.

4. Importe o componente de layout no `about.js` e `contact.js` (como você fez no `index.js` no passo anterior).

O conteúdo de todas as suas três páginas está centralizado graças a esse único componente de layout compartilhado!

### ✋ Adicione um título ao site

1. Adicione a seguinte linha a um dos seus novos componentes de layout:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MySweetSite</h3> {/* highlight-line */}
    {children}
  </div>
)
```

Se você for a qualquer uma das suas três páginas, você verá o mesmo título adicionado, como, por exemplo, na página `/about/`:

![with-title](with-title.png)

### ✋ Adicione links de navegação entre páginas

1. Copie o seguinte no arquivo do seu componente de layout:

```jsx:title=src/components/layout.js
import React from "react"
// highlight-start
import { Link } from "gatsby"

const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)
// highlight-end

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {/* highlight-start */}
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MySweetSite</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Home</ListLink>
        <ListLink to="/about/">About</ListLink>
        <ListLink to="/contact/">Contact</ListLink>
      </ul>
    </header>
    {/* highlight-end */}
    {children}
  </div>
)
```

![with-navigation2](with-navigation2.png)

E aí está! Um site com três páginas e navegação global básica.

_Desafio:_ Com os poderes do seu novo "componente de layout", tente adicionar cabeçalho, rodapé, navegação global, sidebar, etc. nos seus sites Gatsby.

## O que vem a seguir?

Siga para a [parte quatro do tutorial](/tutorial/part-four/) onde você irá começar a aprender sobre a camada de dados do Gatsby e como criar páginas programaticamente.
