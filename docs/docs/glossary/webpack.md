---
title: webpack
disableTableOfContents: true
---

Aprenda o que é webpack, como funciona, e como Gatsby o usa para acelerar o desenvolvimento de web sites.

## O que é webpack?

[webpack](/docs/glossary#webpack) é um <q>gerador de módulos estático,</q> ou um software que coleta _pedaços_ ou módulos do JavaScript e os compila em um pacote mais otimizado. webpack é um dos principais softwares de modularização que sustenta o Gatsby.

O webpack funciona criando um _gráfico de dependências_. Em outras palavras, o webapck determina qual módulo depende de outro para fazer seu site funcionar. Um _módulo_ é um conjunto de códigos que encapsula algumas funcionalidades. Pode ser tão pequeno quanto uma única função JavaScript ou pode ser uma biblioteca inteira como o [React](/docs/glossary#react).

O webpack determina dependências do conteúdo do `webpack.config.js`. `webpack.config.js` pode conter um ou mais _pontos de entrada_, no qual o webpack determina qual arquivo ou arquivos deve ser usado como ponto (ou pontos) de entrada para o gráfico de dependências. Veja o exemplo a seguir.

```javascript
module.exports = {
  entry: "/scripts/index.js",
}
```

O webpack processa arquivos JavaScript e JSON por padrão, mas você pode adicionar suporte para CSS e arquivos de mídia com softwares e configurações adicionais. O Gatsby por exemplo, tem seu próprio [`webpack.config.js`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/webpack.config.js) que suporta [arquivos globais de CSS](/docs/global-css/), [módulos CSS _component-scoped_](/docs/css-modules/), e [CSS-in-JS](/docs/css-in-js/).

Você também pode usar o webpack para otimizar como o CSS e o JavaScript são entregues ao navegador. O webpack suporta uma funcionalidade conhecida como [_code splitting_](https://webpack.js.org/guides/code-splitting/). _Code splitting_ permite que você divida seu código entre alguns pacotes que são carregados conforme são necessários ou requisitados. O Gatsby já está configurado para usar essa funcionalidade. Você não tem que fazer nenhuma configuração adicional para ter esses benefícios.

Se você quiser adicionar suporte para funcionalidades como [Sass/SCSS](/docs/sass/), que o Gatsby não da suporte por padrão, você também pode [adicionar uma configuração customizada](/docs/add-custom-webpack-config/), ou usar um dos [plugins do Gatsby](/docs/plugins/) que são contribuições da comunidade.

### Aprenda mais sobre webpack

- Site oficial do [webpack](https://webpack.js.org/)
- [Configuração customizada](/docs/customization/) da Documentação do Gatsby
