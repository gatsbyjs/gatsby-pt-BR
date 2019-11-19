---
title: Styled Components
---

Neste guia, você aprenderá como configurar um site com a biblioteca CSS-in-JS [Styled Components](https://www.styled-components.com/).

Styled Components permite você usar a sintaxe CSS real dentro de seus components. Styled Components é uma variante do "CSS-in-JS" — que resolve muitos dos problemas do CSS tradicional.

Um dos problemas mais importantes que ele resolve é a colisão de nomes de seletores. Com o CSS tradicional, você deve tomar cuidado para não sobrescrever os seletores de CSS usados em outras partes de um site, porque todos os seletores de CSS vivem no mesmo espaço de nome global. Essa infeliz restrição pode levar a elaborar (e muitas vezes confuso) esquemas de nomeação de seletores.

Com CSS-in-JS, você evita tudo isso, pois os seletores de CSS têm escopo definido automaticamente para seus componentes. Os estilos são fortemente acoplados aos seus componentes. Isso torna muito mais fácil saber como editar o CSS de um componente, pois nunca há confusão sobre como e onde o CSS está sendo usado.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components"
  lessonTitle="Style Gatsby sites with styled-components"
/>

Primeiro, abra uma nova janela do terminal e execute o seguinte para criar um novo site:

```shell
gatsby new styled-components-tutorial https://github.com/gatsbyjs/gatsby-starter-hello-world
cd styled-components-tutorial
```

Segundo, instale as dependências necessárias para o `styled-components`, incluindo o plugin Gatsby.

```shell
npm install --save gatsby-plugin-styled-components styled-components babel-plugin-styled-components
```

E, em seguida, adicione-o ao `gatsby-config.js` do seu site:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

Em seguida, no seu terminal, execute `gatsby develop` para iniciar o servidor de desenvolvimento Gatsby.

Agora crie uma página de amostra de Styled Components em `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import styled from "styled-components"

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
  margin: 0 auto 12px auto;
  &:last-child {
    margin-bottom: 0;
  }
`

const Avatar = styled.img`
  flex: 0 0 96px;
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
    <h1>About Styled Components</h1>
    <p>Styled Components is cool</p>
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

### Ativando folhas de estilo do usuário com um nome de classe estável

Adicionar um nome de classe CSS persistente aos seus componentes de estilo pode facilitar para os usuários finais do seu site para tirar proveito das [folhas de estilos do usuário](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para acessibilidade.

Aqui está um exemplo onde o nome da classe `container` é adicionado ao DOM junto com os nomes de classe criados dinamicamente por Styled Components:

```jsx:title=src/components/container.js
import React from "react"
import styled from "styled-components"

const Section = styled.section`
  margin: 3rem auto;
  max-width: 600px;
`

export default ({ children }) => (
  <Section className={`container`}>{children}</Section>
)
```

Um usuário final do seu site poderia então [escrever seus próprios estilos CSS](https://mediatemple.net/blog/tips/bend-websites-css-will-stylish-stylebot/) correspondentes os elementos HTML usando um nome de classe ` .container`. Se o seu estilo CSS-in-JS mudar, ele não afetará a folha de estilo do usuário final.

```css:title=user-stylesheet.css
.container {
  margin: 5rem auto;
  font-size: 1.3rem;
}
```
