---
title: Para o que você não precisa de plugins
---

A maioria das funcionalidades de terceiros que você quer adicionar ao seu website seguirá os padrões de JavaScript e React.js para a importação de pacotes e composição de UIs. Estes não precisam de um plugin Gatsby!

Alguns exemplos:

<<<<<<< HEAD
- Importar pacotes JavaScript que provém funcionalidades gerais, como a `lodash` ou `axios`.
- Utilizar componentes React ou componentes de bibliotecas que você quer incluir na sua UI como `Ant Design`, `Material UI`, ou o tipo da sua biblioteca de componentes.
- Integrar bibliotecas de visualização, como a `Highcharts` ou `d3`.

Como regra geral, você pode usar _qualquer_ pacote npm independente do Gatsby com o Gatsby. O que os plugins oferecem é uma integração pré-embalada no núcleo das APIs do Gatsby para poupar tempo e energia, com configurações básicas. No caso de `Componentes Estilizados`, você poderia renderizar manualmente o componente `Provider` próximo a raiz da sua aplicação, ou você pode apenas usar o `gatsby-plugin-styled-components` que cuida desse passo para você, além de quaisquer outras dificuldades que você possa encontrar na configuração de Componentes Estilizados para trabalhar com renderização do lado do servidor.
=======
- Importing JavaScript packages that provide general functionality, such as `lodash` or `axios`
- Integrating visualization libraries, such as `Highcharts` or `d3`.

As a general rule, any npm package you might use while working on another JavaScript or React application can also be used ,with a Gatsby application. What plugins offer is a prepackaged integration into the core Gatsby APIs to save you time and energy, with minimal configuration.

A good use case would be using `Styled Components`, you could manually render the `Provider` component near the root of your application, or you could use [gatsby-plugin-styled-components](https://www.gatsbyjs.org/packages/gatsby-plugin-styled-components/) which takes care of this step for you in addition to any other difficulties when configuring Styled Components to work with server-side rendering.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1
