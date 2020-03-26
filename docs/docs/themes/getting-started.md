---
title: Iniciando com os Temas do Gatsby
---

A maneira mais rápida de começar a usar um tema do Gatsby é usar um iniciador configurado para usar o tema.

Por exemplo, `gatsby-starter-blog-theme` é um iniciador de temas para o pacote `gatsby-theme-blog`.

Um **iniciador regular do Gatsby** cria um novo site do Gatsby pré-configurado para um caso de uso específico. O site resultante efetivamente se separa do iniciador - depois de criado, o site não mantém nenhuma conexão com o iniciador.

Um **iniciador de temas do Gatsby** cria um novo site do Gatsby que instala e configura um ou mais temas do Gatsby. Quando um iniciador instala um tema, ele mantém a conexão com esse tema como um pacote npm independente.

A instalação do iniciador de temas do blog Gatsby é o mesmo processo que um iniciador regular do Gatsby:

```shell
gatsby new my-blog https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

## O que um iniciador de temas faz?

O iniciador do tema oficial do blog Gatsby faz o seguinte:

### 1. O iniciador instala o tema e o configura

Quando você usa um iniciador construído com um tema, frequentemente verá que é apresentado inicialmente com um menor `gatsby-config.js`. Os temas começam a funcionar quando instalados através de um array `plugins`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-theme-blog",
      options: {},
    },
  ],
  // Customize your site metadata:
  siteMetadata: {
    title: "My Blog Title",
    author: "My Name",
    description: "My site description...",
    siteUrl: "https://www.gatsbyjs.org/",
    social: [
      {
        name: "twitter",
        url: "https://twitter.com/gatsbyjs",
      },
      {
        name: "github",
        url: "https://github.com/gatsbyjs",
      },
    ],
  },
}
```

### 2. O iniciador cria exemplos de postagens de blog.

```mdx:title=/content/posts/hello-world.mdx
---
title: Hello, world!
path: /hello-world
---

I'm an example post!
```

Depois de fazer algumas modificações, execute o `gatsby develop` para iniciar um servidor de desenvolvimento e visualizar suas alterações no navegador.

## Atualizando um tema

Para obter as atualizações mais recentes do seu tema, você pode atualizar a versão `gatsby-theme-blog` no` package.json` do seu site.

Você pode fazer isso executando a instalação do pacote de temas novamente: `npm install --save gatsby-theme-blog`.
