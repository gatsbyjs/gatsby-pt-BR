---
title: Utilizando Macros do Plugin Babel
---

Gatsby inclui uma nova e poderosa forma de aplicar transformações em seu código durante o compilamento, [os macros para o Babel](https://github.com/kentcdodds/babel-plugin-macros)! Macros são como plugins para o Babel, mas ao invés de adicioná-los ao seu `.babelrc`, você os importa dentro do próprio arquivo onde serão utilizados. Isso tem duas grandes vantagens:

- Sem confusão quanto a origem de uma sintaxe fora do padrão. Os macros são explicitamente importados onde quer que sejam usados.
- Sem arquivos de configuração. Os marcos são incluídos diretamente em seu código quando necessários.

Tal como os plugins para o Babel, os macros são executados somente no momento de compilamento. Eles não são incluídos em seu bundle público de JavaScript. Dessa forma, os macros não tem nenhum outro efeito em seu código além das transformações que aplicam.

## Instalando macros

Assim como plugins, muitos macros são publicados como pacotes npm. Por convenção, são nomeados por sua função, seguida de `.macro`.

Por exemplo, [`preval.macro`](https://www.npmjs.com/package/preval.macro) é um macro que pré-avalia o código JavaScript. Você pode instalá-lo usando:

```shell
npm install --save-dev preval.macro
```

Há ainda alguns outros macros que são incluídos em pacotes maiores. Para instalação e uso destes, veja a documentação específica de cada um.

## Utilizando macros

Para usar um macro instalado, você deve importá-lo em seu código:

```javascript
import preval from "preval.macro"
```

Você pode então utilizar a variável importada da forma em que sua documentação a descreve. `preval.macro`, por exemplo, é usado como um identificador template literal:

```javascript
import preval from "preval.macro"
const x = preval`module.exports = 1` // linha em destaque
```

Quando compilado, esse código será transformado em:

```javascript
const x = 1
```

## Descobrindo macros disponíveis

Dê uma olhada na lista [Awesome babel macros](https://github.com/jgierer12/awesome-babel-macros) para encontrar macros disponíveis para uso. Além disso, essa lista conta com recursos úteis de como fazer bom uso dos macros e mesmo para desenvolver um você mesmo.
