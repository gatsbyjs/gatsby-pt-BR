---
title: Testando CSS-in-JS
---

Bibliotecas populares de CSS-in-JS como [styled-components](https://github.com/styled-components/styled-components) ou [emotion](https://github.com/emotion-js/emotion) também podem ser testadas com a ajuda de [jest-styled-components](https://github.com/styled-components/jest-styled-components) ou [jest-emotion](https://github.com/emotion-js/emotion/tree/master/packages/jest-emotion) respectivamente. Esses pacotes melhoram a experiência de testes de _snapshot_ com Jest e são uma ótima maneira de ajudar a evitar alterações indesejadas na UI do seu _site_. Consulte a documentação do seu pacote para ver se ele também oferece recursos de teste.

Serializadores de _snapshot_ como `jest-styled-components` ou `jest-emotion` modificam a saída padrão para um _snapshot_ mais significativo e legível, por exemplo removendo informações desnecessárias ou exibindo dados em outro formato. O que leva a testes de _snapshot_ mais comparáveis ​​e eficazes.

Por padrão, os _snapshots_ de seus styled components mostram os nomes de classe gerados (que você não definiu) e nenhuma informação de estilização. Ao alterar os estilos, você verá apenas a diferença de alguns nomes de classe criptografados (_hashes_). É por isso que você deve usar os serializadores de _snapshot_ mencionados acima. Eles removem os _hashes_ e formatam o CSS em elementos de estilo.

Para esse exemplo você vai usar o emotion. Os utilitários de teste do emotion e glamor são amplamente baseados em [jest-styled-components](https://github.com/styled-components/jest-styled-components) então eles tem usos parecidos. Por favor dê uma olhada na seção de testes da sua biblioteca para seguir em frente.

## Instalação

```shell
npm install --save-dev jest-emotion babel-plugin-emotion
```

Como o [plugin emotion do Gatsby](/packages/gatsby-plugin-emotion/) está usando `babel-plugin-emotion` por baixo dos panos, você também precisará instalá-lo para que o Jest possa usá-lo.

Se você seguiu o [guia de Testes Unitários](/docs/unit-testing) terá o arquivo `jest-preprocess.js` na raiz do seu projeto. Abra esse arquivo e adicione o plugin:

```diff:title=jest-preprocess.js
const babelOptions = {
  presets: ["babel-preset-gatsby"],
+  plugins: [
+    "emotion",
+  ],
}

module.exports = require("babel-jest").createTransformer(babelOptions)
```
Para que o Jest use o serializador, você precisará criar o arquivo `setup-test-env.js`, que será executado automaticamente antes de cada teste. Crie o arquivo `setup-test-env.js` na raiz do seu projeto. Insira este código nele:

```js:title=setup-test-env.js
import { createSerializer } from "jest-emotion"
import * as emotion from "@emotion/core"

expect.addSnapshotSerializer(createSerializer(emotion))
```

Por fim, você precisa informar ao Jest onde encontrar esse arquivo. Abra seu `package.json` e adicione esta entrada à sua seção `"jest"`:

```json:title=package.json
"jest": {
  "setupTestFrameworkScriptFile": "<rootDir>/setup-test-env.js"
}
```

## Utilização

Neste exemplo, você usará o `react-test-renderer`, mas também poderá usar [@testing-library/react](/docs/testing-react-components) ou qualquer outra biblioteca apropriada. Como você criou o arquivo `setup-test-env.js`, você pode escrever seus testes unitários como costumava fazer. Mas agora você também receberá as informações de estilização!

```js:title=src/components/Button.test.js
import React from "react"
import styled from "react-emotion"
import renderer from "react-test-renderer"

const Button = styled.div`
  color: hotpink;
`

test("Button renders correctly", () => {
  expect(
    renderer.create(<Button>This is hotpink.</Button>).toJSON()
  ).toMatchSnapshot()
})
```

O _snapshot_ resultante vai ser parecido com isso:

```js
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`Button renders correctly 1`] = `
.emotion-0 {
  color: hotpink;
}

<div
  className="emotion-0 emotion-1"
>
  This is hotpink.
</div>
`
```

Se o seu styled component depende do `theme` via `ThemeProvider`, você terá duas opções:

- Encapsular todos os seus componentes com o `ThemeProvider`
- Usar auxiliares de API (consulte a documentação da biblioteca, por exemplo, [styled-components](https://github.com/styled-components/jest-styled-components#theming) ou [emotion](https://github.com/emotion-js/emotion/tree/master/packages/emotion-theming#createbroadcast-function))

E é aqui que os testes de _snapshots_ realmente brilham. Se você mudar, por exemplo a cor principal no seu arquivo de tema, você verá quais componentes são afetados por essa alteração. Dessa forma, você pode capturar alterações indesejadas na estilização de seus componentes.

Este exemplo usa a primeira opção:

```js:title=src/components/Wrapper.test.js
import React from "react"
import { ThemeProvider } from "emotion-theming"
import renderer from "react-test-renderer"

const theme = {
  maxWidth: "1450px",
}

const Wrapper = styled.section`
  max-width: ${props => props.theme.maxWidth};
`

test("Wrapper renders correctly", () => {
  expect(
    renderer
      .create(
        <ThemeProvider theme={theme}>
          <Wrapper>Content.</Wrapper>
        </ThemeProvider>
      )
      .toJSON()
  ).toMatchSnapshot()
})
```

O _snapshot_ resultante vai ser parecido com isso:

```js
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`Wrapper renders correctly 1`] = `
.emotion-0 {
  max-width: 1450px;
}

<section
  className="emotion-0 emotion-1"
>
  Content
</div>
`
```
