---
title: Theme UI
---

[Theme UI][] é uma biblioteca para estilizar aplicações React com restrições de design configuradas pelo usuário.
Ela permite estilizar qualquer componente na aplicação, com tipografia, cor e valores de layout definidos no objeto compartilhado do tema.
A Theme UI está implementada atualmente nos temas oficiais do Gatsby,
mas pode ser usada em qualquer site Gatsby ou aplicação React.
Ela inclui a biblioteca de CSS-in-JS, [Emotion][], junto de utilidades adicionais para estilizar [MDX][], e usar configurações e temas da biblioteca [Typography.js][].

## Usando Theme UI no Gatsby

A Theme UI inclui o pacote `gatsby-plugin-theme-ui` para uma melhor integração com seu projeto Gatsby.

Comece instalando os seguintes pacotes:

```shell
npm install theme-ui gatsby-plugin-theme-ui
```

Após instalar essas dependências, adicione o seguinte trecho ao seu arquivo `gatsby-config.js`

```js:title=gatsby-config.js
module.exports = {
  plugins: ["gatsby-plugin-theme-ui"],
}
```

A Theme UI usa um objeto `theme` para prover cores, tipografia, layout e outros valores utilizados na estilização da sua aplicação, através da [context API do React][].
Dessa forma, seus componentes podem ser estilizados com base em valores predefinidos.

Existem duas formas de adicionar um tema no seu site: configurando através do plugin `gatsby-plugin-theme-ui`, ou usando _local shadowing_.

### Configurando o plugin `gatsby-plugin-theme-ui`

O `gatsby-plugin-theme-ui` possui algumas configurações opcionais. Uma delas é o `preset`, que é o objeto base para o tema que você quer usar no seu site.

O `preset` pode ser um objeto JSON ou o nome de um pacote que o plugin vai importar para você.

Se optar por usar um pacote, certifique-se de que ele está instalado no projeto.

```shell
npm install @theme-ui/preset-funk
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-theme-ui`,
      options: {
        preset: "@theme-ui/preset-funk",
      },
    },
  ],
}
```

Você também pode importar o pacote manualmente. Isso é necessário caso você utilize um pacote local que não está disponível publicamente.

```shell
npm install @theme-ui/preset-funk
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-theme-ui`,
      options: {
        preset: require("meu-preset-local"),
      },
    },
  ],
}
```

O `preset` funciona como o seu tema base, e qualquer estilo local será automaticamente mesclado nele. Estilos locais são considerados mais específicos, e irão sobrescrever os estilos do `preset` quando necessário.

### Local shadowing

A Theme UI usa a [API de component shadowing][] para adicionar o contexto do objeto do tema no seu site. _Shadowing_, é a possibilidade de criar um arquivo no mesmo diretório do tema que você está usando, sobrescrevendo os valores desse tema.

Nesse caso, o diretório citado acima é o `src/gatsby-plugin-theme-ui`. Crie-o seu projeto e adicione um arquivo `index.js` para exportar o objeto do tema.

```shell
mkdir src/gatsby-plugin-theme-ui
```

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {}
```

## Criando o objeto do tema

Crie o diretório `src/gatsby-plugin-theme-ui` no seu projeto e, adicione o arquivo `index.js` para exportar o objeto do tema. Adicione o objeto `colors` para armazenar a paleta de cores do seu site.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#333",
    background: "#fff",
    primary: "#639",
    secondary: "#ff6347",
  },
}
```

Em seguida adicione a base para a tipografia.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#333",
    background: "#fff",
    primary: "#639",
    secondary: "#ff6347",
  },
  // highlight-start
  fonts: {
    body: "system-ui, sans-serif",
    heading: "system-ui, sans-serif",
    monospace: "Menlo, monospace",
  },
  fontWeights: {
    body: 400,
    heading: 700,
    bold: 700,
  },
  lineHeights: {
    body: 1.5,
    heading: 1.125,
  },
  fontSizes: [12, 14, 16, 20, 24, 32, 48, 64, 72],
  // highlight-end
}
```

Por fim, adicione valores para serem usados em espaçamentos.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#333",
    background: "#fff",
    primary: "#639",
    secondary: "#ff6347",
  },
  fonts: {
    body: "system-ui, sans-serif",
    heading: "system-ui, sans-serif",
    monospace: "Menlo, monospace",
  },
  fontWeights: {
    body: 400,
    heading: 700,
    bold: 700,
  },
  lineHeights: {
    body: 1.5,
    heading: 1.125,
  },
  fontSizes: [12, 14, 16, 20, 24, 32, 48, 64, 72],
  // highlight-start
  space: [0, 4, 8, 16, 32, 64, 128, 256, 512],
  // highlight-end
}
```

Sinta-se à vontade para incluir quantos valores achar necessário no seu tema.
Leia mais sobre criação de temas na [documentação da Theme UI](https://theme-ui.com/theming)

## Adicionando estilos aos elementos

A Theme UI usa uma diretiva para adicionar suporte à propriedade `sx` no JSX.
Essa função é habilitada ao incluir o seguinte comentário no topo do arquivo:

```js
/** @jsx jsx */
import { jsx } from "theme-ui"
```

A [propriedade `sx`][] é usada para estilizar elementos referenciando os valores do objeto do tema.

```jsx:title=src/components/header.js
/** @jsx jsx */
import { jsx } from "theme-ui"

export default function Header(props) {
  return (
    <header
      sx={{
        // Esse valor vem do `theme.space[4]`
        padding: 4,
        // Esses valores vem do `theme.colors`
        color: "background",
        backgroundColor: "primary",
      }}
    >
      {props.children}
    </header>
  )
}
```

## Usando Theme UI em um tema Gatsby

Ao usar Theme UI em um tema do Gatsby, é importante entender como o plugin `gatsby-plugin-theme-ui` gerencia os objetos do tema, de múltiplos temas e sites do Gatsby.

Se múltiplos temas estão instalados no mesmo site, o que estiver definido por último no array `plugins` do arquivo `gatsby-config.js` terá prioridade.

Para estender uma configuração existente da Theme UI a partir de um tema, você precisará identificar como o tema base está passando os estilos. Se for através de um `preset`, como o pacote `gatsby-theme-blog` faz, os arquivos criados usando [_local shadowing_](#local-shadowing) serão mesclados automaticamente. Você pode descobrir isso no código fonte do tema na `node_modules` ou no GitHub.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#222",
    primary: "tomato",
  },
}
```

Se o tema por si só, foi feito com [_local shadowing_](#local-shadowing), sem um _preset_, você precisará efetuar o _merge_ desses estilos com os seus. Veja um exemplo usando a API `merge` da Theme UI:

```js:title=src/gatsby-plugin-theme-ui/index.js
import baseTheme from "gatsby-theme-unknown/src/gatsby-plugin-theme-ui"
import { merge } from "theme-ui"

// merge will deeply merge custom values with the
// unknown theme's defaults
export default merge(baseTheme, {
  colors: {
    text: "#222",
    primary: "tomato",
  },
})
```

## Estilizando conteúdo MDX

A Theme UI permite estilizar elementos nos documentos MDX, sem adicionar estilos CSS globais no seu site.
Isso é útil para criar temas do Gatsby, que podem ser instalados em conjunto com outros temas.

Na sua configuração da Theme UI, adicione o objeto `styles` para estilizar elementos renderizados do MDX.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  // base theme values...
  styles: {
    // the keys used here reference elements in MDX
    h1: {
      // the style object for each element
      // can reference other values in the theme
      fontFamily: "heading",
      fontWeight: "heading",
      lineHeight: "heading",
      marginTop: 0,
      marginBottom: 3,
    },
    a: {
      color: "primary",
      ":hover, :focus": {
        color: "secondary",
      },
    },
    // more styles can be added as needed
  },
}
```

Com o exemplo acima, quaisquer elementos `<h1>` ou `<a>` renderizados de um arquivo MDX, irão possuir esses estilos base.

Para aprender mais sobre usar Theme UI no seu projeto, veja o site oficial da [Theme UI][]

[theme ui]: https://theme-ui.com
[emotion]: /docs/docs/emotion.md
[mdx]: /docs/docs/mdx.md
[typography.js]: /docs/docs/typography-js.md
[context api do react]: https://reactjs.org/docs/context.html
[api de component shadowing]: /docs/docs/theme-api.md/#shadowing
[propriedade `sx`]: https://theme-ui.com/sx-prop
