---
title: Para o que você não precisa de plugins
---

A maioria das funcionalidades de terceiros que você quer adicionar ao seu website seguirá os padrões de JavaScript e React.js para a importação de pacotes e composição de UIs. Estes não precisam de um plugin Gatsby!

Alguns exemplos:

- Importar pacotes JavaScript que provém funcionalidades gerais, como a `lodash` ou `axios`.
- Integrar bibliotecas de visualização, como a `Highcharts` ou `d3`.

Como regra geral, você pode usar _qualquer_ pacote npm independente do Gatsby com o Gatsby. O que os plugins oferecem é uma integração pré-embalada no núcleo das APIs do Gatsby para poupar tempo e energia, com configurações básicas.

Um bom caso de uso seria o uso do `Styled Components`, você pode renderizar manualmente o componente `Provider` perto da raiz da sua aplicação ou você pode usar o [gatsby-plugin-styled-components](https://www.gatsbyjs.org/packages/gatsby-plugin-styled-components/) que cuidará desta etapa por você, além de outras dificuldades ao configurar o `Styled Components` para trabalhar com a renderização no servidor.
