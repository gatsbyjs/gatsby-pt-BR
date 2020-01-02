---
title: Para o que você não precisa de plugins
---

A maioria das funcionalidades de terceiros que você quer adicionar ao seu website seguirá os padrões de JavaScript e React.js para a importação de pacotes e composição de UIs. Estes não precisam de um plugin Gatsby!

Alguns exemplos:

- Importando pacotes JavaScript que provém funcionalidades gerais, como a `lodash` ou `axios`.
- Utilizando componentes React ou componentes de bibliotecas que você quer incluir na sua UI como `Ant Design`, `Material UI`, ou o tipo da sua biblioteca de componentes.
- Bibliotecas de vizualização integrada, como a `Highcharts` ou `d3`.

Como regra geral, você pode usar _qualquer_ pacote npm que você possa usar sem Gatsby, com Gatsby. O que os plugins oferecem é uma integração pré-embalada no núcleo do Gatsby APIs para poupar tempo e energia, com configuração mínima. No caso de `Componentes Estilizados`, você poderia renderizar manualmente o componente `Provider` próximo a raiz da sua aplicação, ou você pode apenas usar o `gatsby-plugin-styled-components` no qual cuida desse passo para você além de quaisquer outras dificuldades que você possa encontrar na configuração de Componentes Estilizados para trabalhar com renderização do lado do servidor.
