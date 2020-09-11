---
title: Adicionando um Service Worker
---

## O que é um service worker

Um service worker é um script executado pelo seu navegador em plano de fundo, separado de uma página web, possibilitando a inclusão de funcionalidades que não necessariamente precisam de uma página ou interação com o usuário. Estes service workers aumentam a disponibilidade de seu site mesmo em conexões instáveis, e são essenciais para criar uma boa experiência de usuário.

Suporta também funcionalidades como notificações push e sincronia em plano de fundo

## Usando service workers no Gatsby com `gatsby-plugin-offline`

Gatsby provê um plugin de interface incrível para criar e carregar um service worker em seu site [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Você pode usar esse plugin junto com o [manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (Não esqueça de listar o plugin-offline depois do manifest-plugin para que o arquivo de manifesto possa ser incluso no service worker).

## Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Adicione esse plugin ao seu `gatsby-config.js`

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## Referências

- [Service Workers: uma Introdução](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)