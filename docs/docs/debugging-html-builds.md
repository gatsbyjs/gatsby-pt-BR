---
title: Depurando Compilações HTML
---

Os erros mais comuns ao compilar arquivos HTML estáticos são:

1.  Parte do seu código referencia "variáveis globais do navegador", como `window` ou `document`.
    Se este for o caso, você deve ver uma mensagem de erro como "window is not defined". Para
    corrigir, encontre o código problemático e a) confira se a jalena está definida antes de chamar o
    código, para que o código não   seja executado enquanto o Gatsby está compilando (veja exemplos
    de código abaixo) ou b) se o código está na função render de um componente React.js, mova o
    código para dentro da [vida útil de um `componentDidMount`](https://pt-br.reactjs.org/docs/react-component.html#componentdidmount) ou de um [gancho `useEffect`](https://pt-br.reactjs.org/docs/hooks-reference.html#useeffect),    o que garante que o código não seja executado, a menos que esteja
    no navegador.

1.  Confira se todo arquivo JS listado no diretório `pages` (e qualquer sub-diretório)
    está exportando um componente React ou uma string. O Gatsby trata qualquer arquivo
    dentro do diretório `pages`como um componente de página, então deve uma exportação
    padrão que é um componente ou string.

1.  Você misturou chamadas `import` e `require` no mesmo arquivo. Isso pode levar a
    "WebpackError: Invariant Violation: Minified React error #130" [já que o Webpack 4
    é mais restrito que a v3](/docs/migrating-from-v1-to-v2/#convert-to-either-pure-commonjs-or-pure-es6).
    A solução é utilizar somente `import`.

1.  Sua aplicação não está corretamente [hidratada](https://pt-br.reactjs.org/docs/react-dom.html),
    o que resulta em inconsistência entre gatsby develop e gatsby build. É possível que uma mudança em
    um arquivo como `gatsby-ssr` ou `gatsby-browser` possua uma estrutura que não foi replicada no outro
    arquivo, o que significa existir uma divergência entre o cliente e a saída do servidor.

1.  Alguma outra razão :-) #1 é o motivo mais comum de falhas ao compilar arquivos estáticos.
    Se for alguma outra razão, você terá que ser um pouco mais criativo para encontrar o problema.

## Como verificar se `window` está definido

```javascript
// Funções requerentes causam erros durante a compilação
// pois o código tenta referenciar a janela do navegador
const module = require("module") // Error

// Envolva a requisição em uma conferência pela janela
if (typeof window !== `undefined`) {
  const module = require("module")
}
```

Caso o módulo precise ser definido para que o código funcione, é possível utilizar um operador ternário

```javascript
const module = typeof window !== `undefined` ? require("module") : null
```

## Consertando módulos de terceiros

Então, o pior aconteceu e você está utilizando um módulo NPM que espera que `window`
seja definido. Você pode reportar o problema para que o módulo seja corrigido, mas
o que fazer nesse meio tempo?

Uma solução é [customizar](/docs/add-custom-webpack-config) a sua configuração do
webpack para substituir o módulo problemático com um módulo postiço durante a
renderização do servidor.

`gatsby-node.js` na raíz do projeto:

```js:title=gatsby-node.js
exports.onCreateWebpackConfig = ({ stage, loaders, actions }) => {
  if (stage === "build-html") {
    actions.setWebpackConfig({
      module: {
        rules: [
          {
            test: /bad-module/,
            use: loaders.null(),
          },
        ],
      },
    })
  }
}
```

Outra solução é utilizar um pacote como [react-loadable](https://github.com/jamiebuilds/react-loadable). O módulo que tenta utilizar `window` será carregado dinamicamente apenas no lado do cliente (e não durante a renderização do lado do servidor).
