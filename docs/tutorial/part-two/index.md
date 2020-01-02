---
title: Introdução aos estilos com Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

<!-- Idea: Create a glossary to refer to. A lot of these terms get jumbled -->

<!--
  - Global styles
  - Component css
  - CSS-in-JS
  - CSS Modules

-->

Bem-vindo a parte dois do tutorial Gatsby!

## O que é esse tutorial?

Nessa parte, você vai explorar opções para estilizar websites feitos com Gatsby e mergulhar mais profundo no uso de componentes React para construção de sites.

## Usando estilos globais

Todo site tem algum estilo global. Isto inclue coisas como fontes e cores de fundo do site. Esses estilos definem a aparência geral do site - muito parecido com como a cor e a textura de uma parede definem a aparência geral de uma sala.

### Criando estilos globais com arquivos padrão de CSS

Uma das maneiras mais diretas de adicionar estilos globais a um site é usar uma folha de estilo global `.css`.

#### ✋ Crie um novo site Gatsby

Comece criando um novo site Gatsby. Pode ser melhor (principalmente se você é novo na linha de comando) fechar as janelas do terminal usadas para [parte um](/tutorial/part-one/) e iniciar uma nova sessão do terminal para a parte dois.

Abra uma nova janela do terminal, crie um novo "hello world" gatsby site, e inicie o servidor de desenvolvimento.

```shell
gatsby new tutorial-part-two https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-two
```

Agora você tem um novo Gatsby site(baseado no Gatsby starter "hello world") com a seguinte estrutura:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
```

#### ✋ Adiciona estilos em um arquivo css

1. Crie um arquivo `.css` no seu novo projeto:

```shell
cd src
mkdir styles
cd styles
touch global.css
```

> Nota: Sinta-se livre para criar esses diretórios e arquivos usando seu editor de texto, se você preferir.

Agora você deve ter uma estrutura como essa:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
```

2. Defina alguns estilos no arquivo `global.css`:

```css:title=src/styles/global.css
html {
  background-color: lavenderblush;
}
```

> Nota: A localização do arquivo css de exemplo em uma pasta `/src/styles/` é absoluto.

#### ✋ Inclua a folha de estilos em seu `gatsby-browser.js`

1. Crie o `gatsby-browser.js`

```shell
cd ../..
touch gatsby-browser.js
```

A estrutura de arquivos do seu projeto agora deve parecer com isso:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

> 💡 O que é o `gatsby-browser.js`? Não se preocupe muito com isso e, por enquanto, saiba que o `gatsby-browser.js` é um dos poucos arquivos especiais que o Gatsby procura e usa (se eles existirem). Aqui, a nomeação do arquivo **é** importante. Se você quiser explorar mais agora, confira [a documentação](/docs/browser-apis/).

2. Importe sua folha de estilos recentemente criada no arquivo `gatsby-browser.js`:

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"

// ou:
// require('./src/styles/global.css')
```

> Nota: As sintaxes CommonJS (`require`) e ES Module (`import`) funcionam aqui. Se você não tiver certeza sobre qual escolher, usamos `import` na maioria das vezes.

3. Inicie o servidor de desenvolvimento:

```shell
gatsby develop
```

Se você abrir seu projeto no seu projeto no navegador, deverá ver um plano de fundo lavanda aplicado no "hello world" starter:

![Lavender Hello World!](global-css.png)

> Dica: Esta parte do tutorial se concentrou na maneira mais rápida e direta de começar a estilizar um site do Gatsby - importando arquivos CSS padrão diretamente, usando o `gatsby-browser.js`. Na maioria dos casos, a melhor maneira de adicionar estilos globais é com um componente de layout compartilhado. [Confira a documentação](/docs/global-css/) para saber mais sobre essa abordagem.

## Usando css com escopo de componente

Até agora, falamos sobre a abordagem mais tradicional do uso padrão de CSS. Agora, falaremos sobre vários métodos de modularização do CSS para lidar com o estilo de maneira orientada a componentes

### CSS Modules

Vamos explorar o **CSS Modules**. Citando de
[the CSS Module homepage](https://github.com/css-modules/css-modules):

> A **CSS Module** é um arquivo CSS no qual todos os nomes de classe e de animação
> têm escopo localmente por padrão.

CSS Modules são muito populares porque eles deixam você escrecer CSS normalmente, mas com muito mais segurança. A ferramenta gera classes únicas e nomes de animações de forma automática, então você não precisa se preocupar com conflitos entre os seletores.

Gatsby trabalha fora da caixa com CSS Modules, Esta abordagem é altamente recomendada para novos projetos com Gatbsy (e React no geral).

#### ✋ Criando uma nova página usando CSS Modules

Nesta seção, você vai criar uma nova página e estiliza-lá usando CSS Module.

Primeiro, crie um novo componente chamado `Container`.

1. Cria uma nova pasta em `src/components` e então, dentro deste diretório, crie um arquivo chamado `container.js` e cole o seguinte código:

```javascript:title=src/components/container.js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
)
```

Você notará que importou um arquivo de módulo css chamado `container.module.css`. Vamos criar esse arquivo agora.

2. No mesmo diretório (`src/components`), crie um arquivo `container.module.css` e copie/cole o seguinte código:

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

Você notara que o arquivo tem `.module.css` no final do seu nome em vez do usual `.css`. Esta é a forma como avisamos ao Gatsby que este arquivo deve ser processado como um CSS Module em vez de CSS comum.

3. Crie uma nova página criando um arquivo em:
   `src/pages/about-css-modules.js`:

```javascript:title=src/pages/about-css-modules.js
import React from "react"

import Container from "../components/container"

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
)
```

Agore, se você visitar `http://localhost:8000/about-css-modules/`, sua página deve ficar da seguinte forma:

![Page with CSS module styles](css-modules-basic.png)

#### ✋ Estilize um componente usando CSS Modules

Nesta seção, você vai criar uma lista de pessoas com nomes, fotos e pequenas briografias em latim. Você deve criar um componente `<User />` e estilizar esse componente usando CSS Module.

1. Crie o arquivo de CSS em `src/pages/about-css-modules.module.css`.

2. Cole o seguinte código no novo arquivo:

```css:title=src/pages/about-css-modules.module.css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

3. Importe o novo arquivo `src/pages/about-css-modules.module.css` na página `about-css-modules.js` que você criou mais cedo editando as primeiras linhas da seguinte forma:

```javascript:title=src/pages/about-css-modules.js
import React from "react"
// highlight-next-line
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

// highlight-next-line
console.log(styles)
```

O código `console.log(styles)` mostrará a importação resultante para que você possa ver o resultado do seu arquivo `. /about-css-modules.module.css` processado. Se você abrir o console do desenvolvedor (usando por exemplo, Firefox ou Chrome developer tools) em seu navegador, você vai ver:

![Import result of CSS module in console](css-modules-console.png)

Se você comparar isso com seu arquivo CSS, você vai ver que cada classe agora é uma chave no objeto importado apontando para uma longa string, por exemplo, `avatar` aponta para `src-pages----about-css-modules-module---avatar---2lRF7`. Essas são os nomes das classes geradas pelo CSS Modules. Elas são únicas em todo seu site. E como você precisa importá-los para usar as classes, nunca há dúvidas sobre onde algum CSS está sendo usado.

4. Crie um componente `User`.

Crie um novo componente `<User />` inline na página `about-css-modules.js`. Modifique `about-css-modules.js` para ficar parecido com o seguinte código:

```jsx:title=src/pages/about-css-modules.js
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

console.log(styles)

// highlight-start
const User = props => (
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>{props.username}</h2>
      <p className={styles.excerpt}>{props.excerpt}</p>
    </div>
  </div>
)
// highlight-end

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
    {/* highlight-start */}
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    {/* highlight-end */}
  </Container>
)
```

> Dica: Geralmente, se você usa um componente em vários locais de um site, ele deve estar em seu próprio arquivo de módulo no diretório `components`. Mas, se for usado apenas em um arquivo, crie-o inline.

Agora a página final deve ficar assim:

![User list page with CSS modules](css-modules-userlist.png)

### CSS-in-JS

CSS-in-JS é uma abordagem de estilo orientada a componentes. Geralmente, é um padrão em que [CSS é composto inline usando JavaScript](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js).

#### Usando CSS-in-JS com Gatsby

Existem muitas bibliotecas CSS-in-JS diferentes e muitas delas já possuem plugins Gatsby. Não abordaremos um exemplo de CSS-in-JS neste tutorial inicial, mas recomendamos que você [explore](/docs/styling/) o que o ecossistema tem a oferecer. Existem minitutoriais para duas bibliotecas, em particular, [Emotion](/docs/emotion/) e [Styled Components](/docs/styled-components/).

#### Sugestão de leitura em CSS-in-JS

Se você estiver interessado em ler mais, confira[Christopher "vjeux" Chedeau's 2014 presentation that sparked this movement](https://speakerdeck.com/vjeux/react-css-in-js) bem como [Mark Dalgleish's more recent post "A Unified Styling Language"](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

### Outras opções de CSS

O Gatsby suporta quase todas as opções de estilo possíveis (se ainda não houver um plugin para a sua opção CSS favorita, [por favor contribua com um!](/contributing/how-to-contribute/))

- [Typography.js](/packages/gatsby-plugin-typography/)
- [Sass](/packages/gatsby-plugin-sass/)
- [JSS](/packages/gatsby-plugin-jss/)
- [Stylus](/packages/gatsby-plugin-stylus/)
- [PostCSS](/packages/gatsby-plugin-postcss/)

e mais!

## O que vem a seguir?

Agora continue na [parte três do tutorial](/tutorial/part-three/), onde você aprenderá sobre os plugins do Gatsby e os componentes de layout.
