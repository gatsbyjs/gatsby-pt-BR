---
title: Babel
---

<<<<<<< HEAD
Gatsby usa o projeto fenomenal [Babel](https://babeljs.io/) para habilitar o suporte para escrever JavaScript moderno — enquanto ainda suporta navegadores mais antigos.
=======
Gatsby uses the phenomenal project [Babel](https://babeljs.io/) to enable support for writing modern JavaScript — while still supporting older browsers.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

## Como especificar quais navegadores dar suporte

<<<<<<< HEAD
O Gatsby suporta, por padrão, as duas últimas versões dos principais navegadores, IE 9+, bem como qualquer navegador que ainda tenha 1%+ de participação do navegador.

Isso significa que compilamos automaticamente seu JavaScript para garantir que ele funcione em navegadores mais antigos. Também adicionamos automaticamente polyfills conforme necessário — chega de enviar código que misteriosamente quebra em navegadores mais antigos!

Se o seu foco é apenas navegadores mais novos, consulte a página de documentação de [Suporte ao Navegador](/docs/browser-support/) para saber como instruir o Gatsby em quais navegadores você suporta e, em seguida, Babel começará a compilar apenas esses navegadores.
=======
Gatsby supports by default the last two versions of major browsers, IE 9+, as well as any browser that still has 1%+ browser share.

This means that your JavaScript is automatically compiled to ensure it works on older browsers. Polyfills are also automatically added — no more shipping code which mysteriously breaks on older browsers!

If you only target newer browsers, see the [Browser Support](/docs/browser-support/) docs page for how to instruct Gatsby on which browsers you support and then Babel will start compiling for only these browsers.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

## Como usar um arquivo .babelrc personalizado

<<<<<<< HEAD
O Gatsby já vem com uma configuração .babelrc padrão que deve funcionar na maioria dos sites. Se você deseja adicionar predefinições ou plugins personalizados do Babel, pode criar seu próprio `.babelrc` na raiz do seu site, importar o [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) e adicionar plugins adicionais, _presets_ e passar opções para o `babel-preset-gatsby`, por exemplo, `targets`.
=======
Gatsby ships with a default .babelrc setup that should work for most sites. If you'd like to add custom Babel presets or plugins, you can create your own `.babelrc` at the root of your site, import [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby), and add additional plugins, presets, and pass options to `babel-preset-gatsby`, e.g. `targets`.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
npm install --save-dev babel-preset-gatsby
```

<!-- prettier-ignore-start -->
```json:title=.babelrc
{
  "plugins": ["@babel/plugin-proposal-optional-chaining"],
  "presets": [
    [
      "babel-preset-gatsby",
      {
        "targets": {
          "browsers": [">0.25%", "not dead"]
        }
      }
    ]
  ]
}
```
<!-- prettier-ignore-end -->

Para configurações mais avançadas, você também pode copiar os padrões de [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) e personalizá-los para atender às suas necessidades.
