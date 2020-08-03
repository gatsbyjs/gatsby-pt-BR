---
title: Criando páginas 404 prefixadas para idiomas diferentes
---

Usando a API [`onCreatePage`](/docs/node-apis/#onCreatePage) no arquivo `gatsby-node.js` do seu projeto, é possível criar páginas 404 diferentes para URLs com prefixos específicos, por exemplo `/en/`.

Veja um exemplo que mostra como criar uma página 404: em Inglês na URL `src/pages/en/404.js`, e em Alemão na URL `/src/pages/de/404.js`:

```jsx:title=src/pages/en/404.js
import React from "react"
import Layout from "../../components/layout"

export default () => (
  <Layout>
    <h1>Page Not Found</h1>
    <p>Oops, we couldn't find this page!</p>
  </Layout>
)
```

```jsx:title=src/pages/de/404.js
import React from "react"
import Layout from "../../components/layout"

export default () => (
  <Layout>
    <h1>Seite nicht gefunden</h1>
    <p>Ups, wir konnten diese Seite nicht finden!</p>
  </Layout>
)
```

Agora abra o arquivo `gatsby-node.js` do seu projecto e adicione o código abaixo:

```javascript:title=gatsby-node.js
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage, deletePage } = actions

  // Verificar se a página é uma 404 localizada
  if (page.path.match(/^\/[a-z]{2}\/404\/$/)) {
    const oldPage = { ...page }

    // Pegar o código de idioma deste caminho,
    // e encontrar todos os outros caminhos
    // que também iniciam com este código
    // (excluindo outros caminhos válidos)
    const langCode = page.path.split(`/`)[1]
    page.matchPath = `/${langCode}/*`

    // Recriar a página modificada
    deletePage(oldPage)
    createPage(page)
  }
}
```

Agora, sempre que o Gatsby criar uma página, irá verificar se a página é uma 404 localizada com o caminho no formato `/XX/404/`. Se este for o caso, então irá pegar o código de idioma, e encontrar todos os outros caminhos que também iniciem com este código, excluindo outros caminhos válidos. Isto significa que sempre que você visitar uma página que não existe no seu site, mas o caminho da página inicia com `/en/` ou `/de/` (ex. `/en/isto-nao-existe`), a sua página 404 localizada será exibida.

Para melhores resultados, configure o seu servidor para servir estas páginas 404 da mesma forma - por exemplo, para `/en/<caminho não existente>`, o seu servidor deverá servir a página `/en/404/`. Caso contrário, você verá a página 404 padrão por algum tempo antes do Gatsby carregar. Se você estiver utilizando o Netlify, pode utilizar o [`gatsby-plugin-netlify`](/packages/gatsby-plugin-netlify/) para fazer isto de forma automática. Note que você precisa criar uma página 404 padrão (geralmente em `src/pages/404.js`) para responder à caminhos sem prefixo, por exemplo `https://exemplo.com/isto-nao-existe`.
