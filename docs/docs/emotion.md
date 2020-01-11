---
title: Emotion
---

Neste tutorial, você irá aprender como configurar um site com a biblioteca CSS-in-JS [Emotion](https://emotion.sh).

Emotion é uma performática e flexível biblioteca CSS-in-JS. Com base em muitas outras bibliotecas CSS-in-JS, ele permite que você crie estilize suas aplicações rapidamente utilizando objetos ou strings de estilo. Tem uma composição previsível para evitar problemas de especificidade com o CSS. Com source maps e rótulos, Emotion tem uma grande experiência de desenvolvimento e grande desempenho com caching pesado na produção.

[Renderização do lado do servidor](https://emotion.sh/docs/ssr) funciona por padrão no Emotion. Você pode usar o método `renderToString` ou `renderToNodeStream` do React sem qualquer configuração adicional. A função `extractCritical` remove regras não usadas que foram criadas com emotion e ajuda a carregar as páginas rapidamente.

Primeiro, abra uma nova janela de terminal e execute o seguinte comando para criar um novo site:

```shell
gatsby new emotion-tutorial https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Em seguida, instale as dependências necessária para o Emotion e Gatsby.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

Depois, adicione o plugin `gatsby-config.js` ao seu site:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

Por fim, em seu terminal execute `npm start` para iniciar o servidor de desenvolvimento do Gatsby.

Agora vamos criar uma simples página Emotion em `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import styled from "@emotion/styled"
import { css } from "@emotion/core"

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const UserWrapper = styled.div`
  display: flex;
  align-items: center;
  margin-top: 0;
  margin-right: auto;
  margin-bottom: 12px;
  margin-left: auto;
  &:last-child {
    margin-bottom: 0;
  }
`

const Avatar = styled.img`
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Description = styled.div`
  flex: 1;
  margin-left: 18px;
  padding: 12px;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const Excerpt = styled.p`
  margin: 0;
`
// Usar o css prop fornece uma API concisa e flexível para estilizar os componentes. //
const underline = css`
  text-decoration: underline;
`

const User = props => (
  <UserWrapper>
    <Avatar src={props.avatar} alt="" />
    <Description>
      <Username>{props.username}</Username>
      <Excerpt>{props.excerpt}</Excerpt>
    </Description>
  </UserWrapper>
)

export default () => (
  <Container>
    <h1 css={underline}>About Emotion</h1>
    <p>Emotion is uber cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
  </Container>
)
```

## Adicionando estilos globais no Gatsby com Emotion

Para iniciar, crie um novo site Gatsby com o [starter _hello world_](https://github.com/gatsbyjs/gatsby-starter-hello-world) e instale o [`gatsby-plugin-emotion`](/packages/gatsby-plugin-emotion/) e suas dependências:

```shell
gatsby new global-styles https://github.com/gatsbyjs/gatsby-starter-hello-world
cd global-styles
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

Crie o `gatsby-config.js` e adicione o plugin Emotion:

```js:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

Em seguida, adicione o componente _layout_ ao `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"
import { Global, css } from "@emotion/core"
import styled from "@emotion/styled"

const Wrapper = styled("div")`
  border: 2px solid green;
  padding: 10px;
`

export default ({ children }) => (
  <Wrapper>
    <Global
      styles={css`
        div {
          background: red;
          color: white;
        }
      `}
    />
    {children}
  </Wrapper>
)
```
Depois, atualize o `src/pages/index.js` para usar o _layout_:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

Execute `npm run build` e você poderá ver no arquivo `public/index.html` que os estilos foram alinhados globalmente.
