---
title: Usando ESLint
---

ESLint é um utilitário de JavaScript de código aberto para _linting_ de código. _Code linting_ é um tipo de análise estática que é freqüentemente usada para encontrar padrões problemáticos. Existem ferramentas de _linting_ de código para a maioria das linguagens de programação e, às vezes, os compiladores incorporam o _linting_ no processo de compilação.

O JavaScript, por ser uma linguagem dinâmica e fracamente tipada, é especialmente propenso a erros de desenvolvedor. Sem o benefício de um processo de compilação, o código JavaScript geralmente é executado para encontrar erros de sintaxe ou outros erros. Ferramentas de _linting_ como o ESLint permitem que os desenvolvedores descubram problemas com seu código JavaScript sem executá-lo.

## Como usar o ESLint

Gatsby traz o [ESLint](https://eslint.org) já incluso no seu _setup_. Para a maioria dos usuários, a nossa configuração do ESlint é tudo que você precisa. No entanto caso você deseja personalizar sua configuração do ESlint, por exemplo se sua empresa possui sua própria configuração do ESlint personalizada, abaixo é mostrado como isso pode ser feito.

Você vai replicar na maioria das vezes a [configuração do Gatsby para ESLint ](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js), então você poderá adicionar predefinições, plugins e regras adicionais.

```shell

# Primeiro instale as dependências necessárias do ESLint
npm install --save-dev eslint-config-react-app
```

Agora que seus pacotes foram instalados, crie um novo arquivo na raiz do site chamado `.eslintrc.js` usando o comando abaixo.

```shell
# Crie um arquivo de configuração para o ESLint
touch .eslintrc.js
```

### Configurando o ESLint

Copie o trecho abaixo para o arquivo `.eslintrc.js` recém criado. Em seguida adicione as predefinições, plugins e regras adicionais conforme desejado.

```js:title=.eslintrc.js
module.exports = {
  globals: {
    __PATH_PREFIX__: true,
  },
  extends: `react-app`,
}
```

Note: When there is no ESLint file Gatsby implicitly adds a barebones ESLint loader. This loader pipes ESLint feedback into the terminal window where you are running or building Gatsby and also to the console in your browser developer tools. This gives you consolidated, immediate feedback on newly-saved files. When you include a custom `.eslintrc` file, Gatsby gives you full control over the ESLint configuration. This means that it will override the built-in `eslint-loader` and you need to enable any and all rules yourself. One way to do this is to use the Community plugin [`gatsby-eslint-plugin`](/packages/gatsby-plugin-eslint/). This also means that the default [ESLint config Gatsby ships with](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js) will be entirely overwritten. If you would still like to take advantage of those rules, you'll need to copy them to your local file.

### Disabling ESLint

Creating an empty `.eslintrc` file at the root of your project will disable ESLint for your site. The empty file will disable the built-in `eslint-loader` because Gatsby assumes once you have an ESLint file you are in charge of linting.
