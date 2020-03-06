---
title: Carregando Plugins Da Sua Pasta Local De Plugins
---

O Gatsby também pode carregar plugins da pasta local de plugins do seu site, que é uma pasta chamada `plugins` no diretório raiz do site.

Considere este exemplo da estrutura do projeto que inclui um plugin local chamado `gatsby-local-plugin`:

```
/my-gatsby-site
└── /src
    └── /pages
    └── /components
<!-- highlight-start -->
└── /plugins
    └── /gatsby-local-plugin
        └── /package.json
        └── /gatsby-node.js
<!-- highlight-end -->
└── gatsby-config.js
└── gatsby-node.js
└── package.json
```

Como o nome da pasta de plugins implica, você pode incluir vários plugins na pasta de plugins local.

A inclusão de um plugin local na pasta de plugins também requer uma etapa de configuração (semelhante a um plugin de terceiros que você instalou na pasta `node_modules` executando o `npm install`); Assim como os plugins instalados a partir do npm precisam ser incluídos no seu `gatsby-config`, você também precisa adicionar o nome do seu plugin local ao array de plugins:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-third-party-plugin`,
    `gatsby-local-plugin`, // highlight-line
  ],
}
```

## Verificando se seu plugin está carregando


Para verificar se seu plugin está disponível para uso em seu site Gatsby, você pode adicionar um pequeno trecho de código a um arquivo `gatsby-node.js` (pode ser necessário adicionar o arquivo `gatsby-node.js`, se ainda não houver) na raiz do seu plugin:

```javascript:title=plugins/gatsby-local-plugin/gatsby-node.js
exports.onPreInit = () => {
  console.log("Testing...")
}
```

_O [`onPreInit` API](/docs/node-apis/#onPreInit) é a primeira API do Node chamada pelo Gatsby logo após o carregamento dos plugins._

Então, ao executar seu site no modo de desenvolvimento ou construção, você deverá ver "Testing..." registrado no seu terminal:

```sh
success open and validate gatsby-configs - 0.051s
success load plugins - 1.047s
Testing... // highlight-line
success onPreInit - 0.023s
...
```

## Carregando plugins locais de _fora_ da pasta plugins

Se você deseja fazer referência a um plugin que não está na pasta de plugins, há várias opções descritas em mais detalhes no [Guia Criando um plugin local](/docs/creating-a-local-plugin/).
