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
 testPathIgnorePatterns: [`node_modules`, `.cache`, `public`],
 transformIgnorePatterns: [`node_modules/(?!(gatsby)/)`],
 globals: {
   __PATH_PREFIX__: ``,
 },
 testURL: `http://localhost`,
 setupFiles: [`<rootDir>/loadershim.js`],
}
```
 
Vamos dar uma olhada nesse arquivo de configuração:
 
- A seção `transform` fala ao Jest que todos os arquivos `js` or `jsx` precisam ser
 transformados usando o arquivo `jest-preprocess.js` na raiz do projeto. Vá em frente e crie esse arquivo agora. É aqui que você define a sua configuração do Babel. Você pode começar seguindo a configuração mínima:
 
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
Isso significa que você pode executar testes digitando `npm test`. Você também pode
executar com um flag que aciona o `watch mode` para observar e executar testes quando eles são alterados: `npm test -- --watch`.

Execute novamente os testes e agora tudo irá funcionar! Você pode receber uma mensagem sobre
o snapshot sendo gravado. Isto é, criado no próximo diretório `__snapshots__` para seus testes.
Se você observar, verá que é um JSON do componente `<Header />`. você deve armazenar seus arquivos
snapshot em um sistema de controle de versão (por exemplo, o repositório GitHub) para que quaisquer
alterações sejam gravadas no histórico. Isso é particularmente importante para lembrar se está usando um sistema de integração como o Travis ou CircleCI para executar testes, pois eles irão falhar se o snapshot não estiver armazenado em um repositório.
 
Se você fizer alterações isso significa que você precisa atualizar o snapshot,
você pode fazer isso executando `npm test -- -u`.
 
 
## Usando TypeScript
 
Se você estiver usando TypeScript, você precisará fazer algumas pequenas alterações
na sua configuração. Primeiro instale o `ts-jest`:
 
```shell
npm install --save-dev ts-jest
```
 
Então atualize a configuração no `jest.config.js`, da seguinte forma:
 
```js:title=jest.config.js
module.exports = {
 transform: {
   "^.+\\.tsx?$": "ts-jest",
   "^.+\\.jsx?$": "<rootDir>/jest-preprocess.js",
 },
 testRegex: "(/__tests__/.*|(\\.|/)(test|spec))\\.([tj]sx?)$",
 moduleNameMapper: {
   ".+\\.(css|styl|less|sass|scss)$": "identity-obj-proxy",
   ".+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$":
     "<rootDir>/__mocks__/file-mock.js",
 },
 moduleFileExtensions: ["ts", "tsx", "js", "jsx", "json", "node"],
 testPathIgnorePatterns: ["node_modules", ".cache", "public"],
 transformIgnorePatterns: ["node_modules/(?!(gatsby)/)"],
 globals: {
   __PATH_PREFIX__: "",
 },
 testURL: "http://localhost",
 setupFiles: ["<rootDir>/loadershim.js"],
}
```
 
Você pode perceber que outras duas opções, `testRegex` and `moduleFileExtensions`,
foram adicionadas. A opção `testRegex` é o padrão que informa ao Jest quais os arquivos
contém testes. O padrão acima corresponde a qualquer arquivo `.js`, `.jsx`, `.ts` ou `.tsx`
dentro do diretório `__tests__`, ou qualquer outro arquivo com extensão `.test.js`,
`.test.jsx`, `.test.ts`, `.test.tsx`, or `.spec.js`, `.spec.jsx`,`.spec.ts`, `.spec.tsx`.
 
A opção `moduleFileExtensions` é necessária quando se está usando o TypeScript.
A única coisa que está sendo feita é dizer ao Jest quais extensões
você pode importar nos seus arquivos sem precisar informar a extensão do arquivo.
Por padrão, isso funciona com extensões de arquivo `js`, `json`, `jsx`, `node`,
portanto precisamos apenas adicionar `ts` e `tsx`. Você pode ler mais a respeito na
[Documentação do Jest](https://jestjs.io/docs/en/configuration.html#modulefileextensions-array-string).
 
## Outros recursos
 
Se você precisar fazer mudanças na sua configuração do Babel, você pode editá-la no
`jest-preprocess.js`. Pode ser necessário que você ative alguns plugins usados pelo Gatsby,
mas lembre-se de que você pode precisar instalar as versões do Babel 7. Acesse [Guia para
configuração do Babel](/docs/babel) para alguns exemplos.
 
Para mais informações sobre teste no Jest, visite [o site do Jest](https://jestjs.io/docs/en/getting-started).
 
Para exemplos englobando todas essas técnicas e um conjunto de testes unitários com
[@testing-library/react][react-testing-library], dê uma olhada no exemplo [using-jest][using-jest].
 
[using-jest]: https://github.com/gatsbyjs/gatsby/tree/master/examples/using-jest
[react-testing-library]: https://github.com/testing-library/react-testing-library
 
