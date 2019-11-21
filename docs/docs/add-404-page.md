---
title: Adicionando uma página 404
---

Para criar uma página 404, crie uma página cuja rota corresponde ao regex 
`^\/?404\/?$` (`/404/`, `/404`, `404/` ou `404`). Na maioria das vezes, 
você desejará criar uma página de componente React em `src/pages/404.js`.

Gatsby garante que sua página 404 seja construida como `404.html` já que muitas 
plataformas de hospedagem estática usam esta por padrão como sua página de erro 404. 
Se você está hospedando seu site de outra maneira, você vai precisar configurar uma
regra personalizada para vincular esse arquivo para erros 404.

Como o Gatsby cria essa página para você por padrão, não há necessidade de configurá-la em seu arquivo `gatsby-node.js`.

Ao desenvolver usando `gatsby develop`, Gatsby usa uma página 404 padrão que
sobrepõe sua página 404 personalizada. Contudo, você ainda pode visualizar 
sua página 404 clicando em "Preview custom 404 page" para verificar 
se está funcionando conforme o esperado. Isto é útil quando você está desenvolvendo, 
já que desta forma você pode ver todas as páginas disponíveis.

A captura abaixo mostra a página 404 padrão que o Gatsby criou. 
Ele também lista todas as páginas do seu site. Clicando no botão 
"Preview custom 404 page" você poderá visualizar a página 404 que você criou.
![Página 404 padrão do Gatsby](images/gatsby-default-404.png)

A captura abaixo mostra a página 404 personalizada.
![Página 404 personalizada do Gatsby](images/gatsby-custom-404.png)
