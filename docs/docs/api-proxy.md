---
title: Solicitações de proxy de API em desenvolvimento
---

## Recursos

Se você não é familiar com o ciclo de vida do Gatsby, veja a visão geral [Ciclos de vida de APIs Gatsby](/docs/gatsby-lifecycle-apis/).

## Solicitações de proxy de API em desenvolvimento

As pessoas costumam disponibilizar o _frontend_ da sua aplicação React na mesma hospedagem e porta de sua implementação _backend_.

Para dizer ao servidor de desenvolvimento para fazer o proxy de qualquer requisição desconhecida para o servidor de desenvolvimento da sua API, adicione um campo `proxy` no arquivo `gatsby-config.js`, por exemplo:

```javascript:title=gatsby-config.js
module.exports = {
  proxy: {
    prefix: "/api",
    url: "http://dev-mysite.com",
  },
}
```

ou:

```js:title=gatsby-config.js
module.exports = {
  proxy: [
    {
      prefix: "/api",
      url: "http://dev-mysite.com",
    },
    {
      prefix: "/api2",
      url: "http://dev2-mysite.com",
    },
  ],
}
```

Dessa forma, quando você fizer `fetch('/api/todos')` em desenvolvimento, o servidor de desenvolvimento irá reconhecer que não é um ativo estático, e vai realizar o _proxy_ da sua requisição para `http://dev-mysite.com/api/todos` como um substituto.

Tenha em mente que o `proxy` tem efeito apenas em desenvolvimento (com `gatsby develop`), e cabe a você garantir que URLs como `/api/todos` apontem para o local correto quando em produção

## Proxying avançado

Algumas vezes você precisa de mais acesso granular/flexível ao servidor de desenvolvimento. Gatsby expõe o servidor de desenvolvimento [Express.js](https://expressjs.com/) ao seu site `gatsby-config.js` onde você pode adicionar o _middleware_ do Express sempre que precisar.

```javascript:title=gatsby-config.js
var proxy = require("http-proxy-middleware")

module.exports = {
  developMiddleware: app => {
    app.use(
      "/.netlify/functions/",
      proxy({
        target: "http://localhost:9000",
        pathRewrite: {
          "/.netlify/functions/": "",
        },
      })
    )
  },
}
```

Lembre-se de que o _middleware_ tem efeito apenas em desenvolvimento (com `gatsby develop`).

### Certificados autoassinados

Se você fizer o proxy para APIs locais com certificados autoassinados, marque a opção `secure` para `false`.

```javascript:title=gatsby-config.js
var proxy = require("http-proxy-middleware")
module.exports = {
  developMiddleware: app => {
    app.use(
      "/.netlify/functions/",
      proxy({
        target: "http://localhost:9000",
        secure: false, // Nao  rejeite certificados autoassinados
        pathRewrite: {
          "/.netlify/functions/": "",
        },
      })
    )
  },
}
```
