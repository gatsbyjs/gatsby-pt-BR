---
title: Composição de Tema
---

Quando estamos construindo temas, muitas vezes vale a pena considerar como seu tema pode compor com outros. Em alguns casos você pode dividir seu tema em partes modulares, como `gatsby-theme-blog` e `gatsby-theme-ecommerce`.

Como os temas ainda são preliminares, recomendamos que comece construindo temas que são mais monolíticos. É menos trabalhoso de se começar, e um tema sempre pode ser fragmentado em temas menores depois.

## Layouts

Nos temas do Gatsby você pode aplicar layouts globais usando [`wrapRootElement`](/docs/browser-apis/#wrapRootElement)
ou [`wrapPageElement`](/docs/browser-apis/#wrapPageElement). É recomendado usar esse recurso com moderação para melhor composição do tema. É uma ótima opção para configurar qualquer provedor de [Contexto React](https://pt-br.reactjs.org/docs/context.html). Normalmente, você não deveria adicionar qualquer componente de layout — como cabeçalhos ou rodapés — porque será aplicado globalmente, o que poderia causar problemas com outros temas.

[Saiba mais sobre layouts e temas do Gatsby](https://www.christopherbiscardi.com/post/layouts-in-gatsby-themes)
