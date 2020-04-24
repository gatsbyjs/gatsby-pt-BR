---
title: Adicionando um prefixo na rota
---

Muitas aplicações são hospedadas em alguma rota que não necessariamente é a rota raiz (`/`) de seu domínio.

Por exemplo, um blog feito com Gatsby poderia viver em `example.com/blog/`, ou um website poderia ser hospedado no GitHub Pages em `example.github.io/my-gatsby-site/`.

Cada um destes websites precisam de um prefixo adicionado para todas as rotas no website. Fazendo com que um link para `/my-sweet-blog-post` devesse ser reescrito como `/blog/my-sweet-blog-post`.

Além disso, links para vários recursos (JavaScript, CSS, imagens, e outros conteúdos estáticos) precisam do mesmo prefixo para que o website continue a funcionar corretamente quando servido com o prefixo adicionado.

Adicionar o prefixo na rota é um processo de dois passos, são eles:

### Adicionar em `gatsby-config.js`

Primeiramente, adicione o valor do `pathPrefix` no seu `gatsby-config.js`.

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/blog`,
}
```

### Fazer o Build

O passo final é fazer o _build_ da sua aplicação com a opção `--prefix-paths`, assim:

```shell
gatsby build --prefix-paths
```

Se essa opção não for passada, Gatsby ignorará seu `pathPrefix` e fará o build do website como se estivesse hospedado na raiz do domínio.

## Serve

Serve your application with the `--prefix-paths` flag, like so:

```shell
gatsby serve --prefix-paths
```

If this flag is not passed, Gatsby will ignore your `pathPrefix`.

## Links dentro da aplicação

O Gatsby provê APIs e bibliotecas para fazer uso dessa funcionalidade sem problemas. Especificamente, o componente [`Link`](/docs/gatsby-link/) tem uma funcionalidade embutida para lidar com prefixo na rota.

Por exemplo, se você quiser um link para a rota `/page-2`, mas na realidade o link final será prefixado (e.g. `/blog/page-2`); você não precisa colocar o prefixo em todos os seus links. Usando o componente `Link` do Gatsby, as rotas serão prefixadas automaticamente com o valor do `pathPrefix` especificado no seu arquivo `gatsby-config.js`. Se depois você migrar e não usar mais o prefixo na rota, seus links _ainda_ continuarão funcionando sem problemas.

Por exemplo, quando navegando para a rota `page-2` no componente de `Link` abaixo; a localização será automaticamente prefixada com o valor especificado no `pathPrefix`.

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby"
import Layout from "../components/layout"

function Index() {
  return (
    <Layout>
      {/* highlight-next-line */}
      <Link to="page-2">Page 2</Link>
    </Layout>
  )
}
```

Se você quiser fazer navegação programática/dinâmica isso também é possível! Utilize a função auxiliar `navigate` do Gatsby e ela também cuidará automaticamente da prefixação da rota.

```jsx:title=src/pages/index.js
import React from "react"
import { navigate } from "gatsby"
import Layout from "../components/layout"

export default function Index() {
  return (
    <Layout>
      {/* Nota: esse é um exemplo propositalmente simples, mas você pegou a ideia! */}
      {/* highlight-next-line */}
      <button onClick={() => navigate("/page-2")}>
        Go to page 2, dynamically
      </button>
    </Layout>
  )
}
```

## Adicione o prefixo nas rotas usando `withPrefix`

Para rotas construídas manualmente, existe essa função auxiliar, [`withPrefix`](/docs/gatsby-link/#add-the-path-prefix-to-paths-using-withprefix) que prefixa a sua rota em produção (mas não durante o desenvolvimento onde as rotas não precisam ser prefixadas).

### Considerações adicionais

A funcionalidade de [`assetPrefix`](/docs/asset-prefix/) pode ser imaginada como relacionada em parte a esta funcionalidade. Esta funcionalidade permite que seus _assets_ (arquivos não-HTML, e.g. imagens, JavaScript, etc.) sejam hospedados em um domínio separado, por exemplo, em uma _CDN_.

Esse recurso funciona perfeitamente com `assetPrefix`. Faça o _build_ da sua aplicação com a opção `--prefix-paths` e você estará na direção certa para hospedar uma aplicação com seus _assets_ hospedados em uma CDN, e seu recurso mais importante disponível na rota prefixada.
