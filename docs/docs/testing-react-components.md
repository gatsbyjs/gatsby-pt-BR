---
title: Testando Componentes React
---

_O framework de teste recomendado é o [Jest](https://jestjs.io/). Este guia pressupõe que você seguiu o guia [Teste de Unidade](/docs/unit-testing) para configurar o Jest._

O [@testing-library/react](https://github.com/testing-library/react-testing-library) de Kent C. Dodds ganhou popularidade desde o seu lançamento e é um ótimo substituto para o [enzyme](https://github.com/airbnb/enzyme). Você pode escrever testes de unidade e integração e incentiva você a consultar o DOM da mesma maneira que o usuário faria. Daí o princípio orientador:

> Quanto mais seus testes se assemelharem à maneira como seu software é usado, mais confiança eles podem oferecer.

Ele fornece funções leves de utilidade em cima do `react-dom` e `react-dom/test-utils` e lhe dá a confiança de que as refatorações do seu componente em relação à implementação (mas não à funcionalidade) não quebrem seus testes.

## Instalação

Instale a biblioteca como uma das `devDependencies` do seu projeto. Opcionalmente, você pode instalar o `jest-dom` para usar seus [matchers personalizados do jest](https://github.com/testing-library/jest-dom#custom-matchers).

```shell
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

Crie o arquivo `setup-test-env.js` na raiz do seu projeto. Insira este código nele:

```js:title=setup-test-env.js
import "@testing-library/jest-dom/extend-expect"
```

Esse arquivo é executado automaticamente pelo Jest antes de cada teste e, portanto, você não precisa adicionar as importações a cada arquivo de teste.

Por fim, você precisa informar ao Jest onde encontrar esse arquivo. Abra seu `jest.config.js` e adicione esta entrada na parte inferior após 'setupFiles':

```js:title=jest.config.js
module.exports = {
  setupFilesAfterEnv: ["<rootDir>/setup-test-env.js"],
}
```

## Uso

Vamos criar um pequeno exemplo de teste usando a biblioteca recém-adicionada. Se você ainda não leu o [guia de teste de unidade][unit testing guide](/docs/unit-testing) — essencialmente você usará `@testing-library/react` em vez de `react-test-renderer` agora. Existem muitas opções quando se trata de seletores, este exemplo escolhe `getByTestId` aqui. Ele também utiliza `toHaveTextContent` do `jest-dom`:

```js
import React from "react"
import { render } from "@testing-library/react"

// You have to write data-testid
const Title = () => <h1 data-testid="hero-title">Gatsby é incrível!</h1>

test("Displays the correct title", () => {
  const { getByTestId } = render(<Title />)
  // Assertion
  expect(getByTestId("hero-title")).toHaveTextContent("Gatsby é incrível!")
  // --> Test will pass
})
```
