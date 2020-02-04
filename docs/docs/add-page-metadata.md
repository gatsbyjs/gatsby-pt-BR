---
title: Adicionando metadados da página
---

Se você já fez uma [auditoria no Lighthouse](/docs/audit-with-lighthouse/), você pode ter notado
uma pontuação baixa na categoria "SEO". Vamos abordar como você pode melhorar essa pontuação.

Adicionar metadados às páginas (como um título ou descrição) é a chave para ajudar mecanismos
de busca como o Google a entender seu conteúdo, e decidir quando mostrá-lo nos resultados de pesquisa.

[React Helmet](https://github.com/nfl/react-helmet) é um pacote que fornece uma interface de componente React para você gerenciar seu [cabeçalho do documento](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

O [plugin react helmet](/packages/gatsby-plugin-react-helmet/) do Gatsby fornece suporte drop-in 
para dados de renderização de servidor adicionados ao React Helmet. Usando o plugin, os atributos que você adicionar ao React Helmet serão adicionados às páginas HTML estáticas que o Gatsby cria.

<<<<<<< HEAD
### Usando `React Helmet` e `gatsby-plugin-react-helmet`
=======
## Using `React Helmet` and `gatsby-plugin-react-helmet`
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

1. Instale os dois pacotes:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2. Adicione o plugin ao array `plugins` no seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [`gatsby-plugin-react-helmet`]
}
```

3. Use o `React Helmet` nas suas páginas:

```jsx
import React from "react"
import { Helmet } from "react-helmet"

class Application extends React.Component {
  render() {
    return (
      <div className="application">
        {/* highlight-start */}
        <Helmet>
          <meta charSet="utf-8" />
          <title>My Title</title>
          <link rel="canonical" href="http://mysite.com/example" />
        </Helmet>
        {/* highlight-end */}
      </div>
    )
  }
}
```

> 💡 O exemplo acima é dos [documentos do React Helmet](https://github.com/nfl/react-helmet#example). Confira-os para mais informação!

Você também pode estar interessado em consultar o documento sobre 
[como adicionar um componente de SEO](/docs/add-seo-component/).
