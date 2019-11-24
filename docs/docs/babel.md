---
title: Babel
---

Gatsby usa o projeto fenomenal [Babel](https://babeljs.io/) para habilitar o suporte para escrever JavaScript moderno — enquanto ainda suporta navegadores mais antigos.

## Como especificar quais navegadores dar suporte

O Gatsby suporta, por padrão, as duas últimas versões dos principais navegadores, IE 9+, bem como qualquer navegador que ainda tenha 1%+ de participação do navegador.

Isso significa que compilamos automaticamente seu JavaScript para garantir que ele funcione em navegadores mais antigos. Também adicionamos automaticamente polyfills conforme necessário — chega de enviar código que misteriosamente quebra em navegadores mais antigos!

Se você segmentar apenas navegadores mais novos, consulte a página de documentação de [Suporte ao Navegador](/docs/browser-support/) para saber como instruir o Gatsby em quais navegadores você suporta e, em seguida, Babel começará a compilar apenas esses navegadores.

## Como usar um arquivo .babelrc personalizado

O Gatsby já vem com uma configuração .babelrc padrão que deve funcionar na maioria dos sites. Se você deseja adicionar predefinições ou plugins personalizados do Babel, pode criar seu próprio `.babelrc` na raiz do seu site, importar o [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) e adicionar plugins adicionais, _presets_ e passar opções para o `babel-preset-gatsby`, por exemplo, `targets`.

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

Para configurações mais avançadas, você também pode copiar os padrões de [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) e personalizá-los para atender às duas necessidades.
