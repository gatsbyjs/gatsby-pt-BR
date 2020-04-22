---
title: Para o que você não precisa de plugins
---

A maioria das funcionalidades de terceiros que você quer adicionar ao seu website seguirá os padrões de JavaScript e React.js para a importação de pacotes e composição de UIs. Estes não precisam de um plugin Gatsby!

Alguns exemplos:

- Importar pacotes JavaScript que provém funcionalidades gerais, como a `lodash` ou `axios`.
- Integrar bibliotecas de visualização, como a `Highcharts` ou `d3`.

Como regra geral, você pode usar _qualquer_ pacote npm independente do Gatsby com o Gatsby. O que os plugins oferecem é uma integração pré-embalada no núcleo das APIs do Gatsby para poupar tempo e energia, com configurações básicas.

A good use case would be using `Styled Components`, you could manually render the `Provider` component near the root of your application, or you could use [gatsby-plugin-styled-components](https://www.gatsbyjs.org/packages/gatsby-plugin-styled-components/) which takes care of this step for you in addition to any other difficulties when configuring Styled Components to work with server-side rendering.
