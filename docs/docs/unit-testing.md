---
title: Testes Unitários
---
Testes unitários são uma ótima forma de se proteger contra erros no seu código antes de você implantá-lo. Embora o Gatsby não tenha suporte nativo aos testes unitários, basta apenas alguns passos
para utilizá-los. Entretanto alguns recursos do processo de construção do Gatsby, como a configuração padrão do Jest, podem não funcionar corretamente. Esse guia mostra como configurar isso.
 
## Configurando seu ambiente
 
O framework de testes mais popular para React é o [Jest](https://jestjs.io/),
o qual foi criado pelo Facebook. Mesmo o Jest sendo um framework de testes unitários
de uso geral no JavaScript, ele tem muitos recursos que funcionam particularmente bem
com React.
 
_OBS: Para esse guia, você começará com o `gatsby-starter-default`, mas os conceitos devem ser os mesmos ou muito similares para o seu site ._
 
### 1. Instalando dependências
 
Primeiro você precisa instalar o Jest e alguns pacotes necessários. Nós instalamos
babel-jest and babel-preset-gatsby para garantir que os presets do babel usados correspondam aos que foram utilizados internamente no site do Gatsby.
 
 
```shell
npm install --save-dev jest babel-jest react-test-renderer babel-preset-gatsby identity-obj-proxy
```
 
### 2. Criando um arquivo de configuração para o Jest
 
Como o Gatsby tem a sua própria configuração do Babel, você precisará informar
manualmente para o Jest usar o `babel-jest`. A forma mais fácil de fazer isso é
criando um arquivo `jest.config.js`. Você pode aproveitar para configurar alguns padrões também:
 
```js:title=jest.config.js
module.exports = {
  transform: {
    "^.+\\.jsx?$": `<rootDir>/jest-preprocess.js`,
  },
  moduleNameMapper: {
    ".+\\.(css|styl|less|sass|scss)$": `identity-obj-proxy`,
    ".+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": `<rootDir>/__mocks__/file-mock.js`,
  },
  testPathIgnorePatterns: [`node_modules`, `\\.cache`, `<rootDir>.*/public`],
  transformIgnorePatterns: [`node_modules/(?!(gatsby)/)`],
  globals: {
    __PATH_PREFIX__: ``,
  },
  testURL: `http://localhost`,
  setupFiles: [`<rootDir>/loadershim.js`],
}
```

<!-- Go over the content of this configuration file:

- The `transform` section tells Jest that all `js` or `jsx` files need to be
  transformed using a `jest-preprocess.js` file in the project root. Go ahead and
  create this file now. This is where you set up your Babel config. You can start
  with the following minimal config: -->

```js:title=jest-preprocess.js
const babelOptions = {
 presets: ["babel-preset-gatsby"],
}
 
module.exports = require("babel-jest").createTransformer(babelOptions)
```
 
- A próxima opção é `moduleNameMapper`. Esta seção funciona um pouco como as
 regras do Webpack, e diz ao Jest como tratar as importações. Você deve se
 atentar principalmente ao _mocking_ de importação de arquivos estáticos,
 a qual o Jest não consegue fazer. O _mock_ é um módulo fictício que
 é usado para testes no lugar do módulo real. É uma boa alternativa quando
 você tem algo que não quer ou não pode testar. Você pode simular qualquer
 coisa, e aqui você está simulando _assets_ em vez do código. Para _stylesheets_
 você precisa utilizar o pacote `identity-obj-proxy`. Para todos os outros _assets_
 você precisará usar um mock manual chamado `file-mock.js`. Você precisa
 criar isso você mesmo. Para isso a convenção é criar um diretório chamado `__mocks__`
 no diretório raiz. Não esqueça os pares de dois underlines no nome.
 
```js:title=__mocks__/file-mock.js
module.exports = "test-file-stub"
```
- A próxima configuração é `testPathIgnorePatterns`. Você está falando ao Jest para
 ignorar quaisquer testes nos diretórios `node_modules` ou `.cache`. 
 
- A próxima opção é muito importante, e é diferente do que você encontrará em outros
 guias do Jest. O  motivo pelo qual você precisa do `transformIgnorePatterns` é porque
 o Gatsby inclui código ES6 não transpilado. Por padrão o Jest tenta transformar o código
 dentro do `node_modules`, então você receberá um erro como este:
 

```text
/my-app/node_modules/gatsby/cache-dir/gatsby-browser-entry.js:1
({"Object.<anonymous>":function(module,exports,require,__dirname,__filename,global,jest){import React from "react"
                                                                                           ^^^^^^
SyntaxError: Unexpected token import
```
Isso ocorre porque o `gatsby-browser-entry.js` não está sendo transpilado antes
da execução no Jest. Você pode corrigir isso alterando o padrão `transformIgnorePatterns`
para excluir o módulo `gatsby`.
 
- A seção `globals` define `__PATH_PREFIX__`, que geralmente é definido pelo
 Gatsby, e que alguns componentes precisam.
 
- Você precisa definir `testURL` como uma URL válida, porque algumas APIs do DOM
 como `localStorage` não estão satisfeitos com o padrão (`about:blank`).
 
> OBS: Se você está usando a versão Jest 23.5.0 ou posterior, o `testURL` será padronizado com
 `http://localhost`, então você pode pular esta configuração.
 
- Há mais uma configuração global que você precisa definir, mas é uma função
que você não pode definir aqui no JSON. O array `setupFiles` permite você listar
 arquivos que serão incluídos antes da execução de todos os testes, então é
 perfeito para isso.
 
```js:title=loadershim.js
global.___loader = {
 enqueue: jest.fn(),
}
```
 
### 3. _Mocks_ úteis para completar seu ambiente de testes
 
#### Simulando `gatsby`
 
Finalmente, é uma boa ideia simular o próprio módulo `gatsby`. Isto pode
não ser necessário no início, mas facilitará muitas coisas se você quiser
testar componentes que usam `Link` ou GraphQL.
 
```js:title=__mocks__/gatsby.js
const React = require("react")
const gatsby = jest.requireActual("gatsby")
 
module.exports = {
 ...gatsby,
 graphql: jest.fn(),
 Link: jest.fn().mockImplementation(
   // these props are invalid for an `a` tag
   ({
     activeClassName,
     activeStyle,
     getProps,
     innerRef,
     partiallyActive,
     ref,
     replace,
     to,
     ...rest
   }) =>
     React.createElement("a", {
       ...rest,
       href: to,
     })
 ),
 StaticQuery: jest.fn(),
 useStaticQuery: jest.fn(),
}
```
 
Isso simula a função `graphql()`, o componente `Link`, e o componente `StaticQuery`.
 
## Escrevendo testes
 
Este guia está longe de ser um guia completo de testes unitários, mas você
pode começar com um simples teste de _snapshot_ para checar se está tudo funcionando.
 
Primeiro, crie o arquivo de teste. Você pode colocá-lo no diretório
`__tests__`, ou colocá-lo em outro lugar (geralmente ao lado do próprio componente),
com a extensão `.spec.js` ou `.test.js`, a preferência é sua. Neste guia , usaremos como convenção a pasta `__tests__`. Vamos criar um teste para o nosso componente de cabeçalho, então crie o arquivo
`header.js` em `src/components/__tests__/`:
 
```js:title=src/components/__tests__/header.js
import React from "react"
import renderer from "react-test-renderer"
 
import Header from "../header"
 
describe("Header", () => {
 it("renders correctly", () => {
   const tree = renderer
     .create(<Header siteTitle="Default Starter" />)
     .toJSON()
   expect(tree).toMatchSnapshot()
 })
})
```
 
Este é um teste de _snapshot_ muito simples, que usa `react-test-renderer` para renderizar
o componente e, em seguida, gera um _snapshot_ dele na primeira execução. Isso então
faz a comparação com futuros snapshots, o que significa que você pode checar rapidamente
as regressões. Visite [a documentação do Jest](https://jestjs.io/docs/en/getting-started)
para aprender mais sobre outros testes que você pode escrever.
 
## Executando testes
 
Se você verificar dentro do `package.json` você provavelmente verá que já existe
um script para `test`, que apenas gera uma mensagem de erro. Mude para utilizar
executável do `jest`, que estará disponível assim:
 
```json:title=package.json
 "scripts": {
   "test": "jest"
 }
```
<!-- 
This means you can now run tests by typing `npm test`. If you want you could
also run with a flag that triggers watch mode to watch files and run tests when they are changed: `npm test -- --watch`.

Run the tests again now and it should all work! You may get a message about
the snapshot being written. This is created in a `__snapshots__` directory next
to your tests. If you take a look at it, you will see that it is a JSON
representation of the `<Header />` component. You should check your snapshot files
into a source control system (for example, a GitHub repo) so that any changes are tracked in history.
This is particularly important to remember if you are using a continuous
integration system such as Travis or CircleCI to run tests, as these will fail if the snapshot is not checked into source control.

If you make changes that mean you need to update the snapshot, you can do this
by running `npm test -- -u`.

## Using TypeScript

If you are using TypeScript, you need to make two changes to your
config.

Update the transform in `jest.config.js` to run `jest-preprocess` on files in your project's root directory.

**Note:** `<rootDir>` is replaced by Jest with the root directory of the project. Don't change it.

```js:title=jest.config.js
    "^.+\\.[jt]sx?$": "<rootDir>/jest-preprocess.js",
```

Also update `jest.preprocess.js` with the following Babel preset to look like this:

```js:title=jest-preprocess.js
const babelOptions = {
  presets: ["babel-preset-gatsby", "@babel/preset-typescript"],
}
```

Once this is changed, you can write your tests in TypeScript using the `.ts` or `.tsx` extensions.

## Other resources

If you need to make changes to your Babel config, you can edit the config in
`jest-preprocess.js`. You may need to enable some of the plugins used by Gatsby,
though remember you may need to install the Babel 7 versions. See
[the Gatsby Babel config guide](/docs/babel) for some examples.

For more information on Jest testing, visit
[the Jest site](https://jestjs.io/docs/en/getting-started).

For an example encapsulating all of these techniques--and a full unit test suite with [@testing-library/react][react-testing-library], check out the [using-jest][using-jest] example.

[using-jest]: https://github.com/gatsbyjs/gatsby/tree/master/examples/using-jest
[react-testing-library]: https://github.com/testing-library/react-testing-library -->
