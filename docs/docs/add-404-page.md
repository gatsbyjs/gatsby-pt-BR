---
title: Adicionando uma página 404
---

<<<<<<< HEAD
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
=======
To create a 404 page create a page whose path matches the regex `^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`). Most often you'll want to create a React component page at `src/pages/404.js`.

Gatsby ensures that your 404 page is built as `404.html` as many static hosting platforms default to using this as your 404 error page. If you're hosting your site another way you'll need to set up a custom rule to serve this file for 404 errors.

Because Gatsby creates this page for you by default, there is no need to configure it in your `gatsby-node.js` file.

When developing using `gatsby develop`, Gatsby uses a default 404 page that overrides your custom 404 page. However, you can still preview your 404 page by clicking "Preview custom 404 page" to verify that it's working as expected. This is useful when you're developing so that you can see all the available pages.

The screenshot below shows the default 404 page that Gatsby creates. It also lists out all the pages on your website. Clicking the "Preview custom 404 page" button will allow you to view the 404 page you created.
![Gatsby Default 404 Page](./images/gatsby-default-404.png)

The screenshot below shows the custom 404 page.
![Gatsby Custom 404 Page](./images/gatsby-custom-404.png)
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f
