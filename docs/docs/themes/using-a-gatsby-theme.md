---
title: Usando um tema Gatsby
---

A forma mais rápida de usar um tema Gatsby é usando um starter que está configurado para usar o tema.

Por exemplo, `gatsby-starter-blog-theme` é um tema starter para o pacote `gatsby-theme-blog`.

Um **starter normal Gatsby** cria um novo site Gatsby que é pré-configurado para um uso específico. O site resultante é realmente uma bifurcação do starter — após criado, ele não mantém conexões com o starter.

Um **tema starter do Gatsby** cria um novo site Gatsby que instala e configura um ou mais temas. Quando um starter instala um tema, mantém-se a conexão com aquele tema como um pacote npm _standalone_.

Instalar um blog Gatsby a partir de um tema starter é o mesmo processo de um starter normal:

```shell
npm install --save gatsby-theme-blog
```

## O que um tema starter faz?

O starter oficial para o tema do blog faz o seguinte:

### 1. O starter instala o tema e o configura.

Quando você usa um starter que foi criado com um tema, você irá ver frequentemente que foi gerado uma versão mais leve do `gatsby-config.js`. Temas irão começar a fazer sua mágica quando instalados através do array `plugins`.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        /*
        - basePath defaults to `/`
        - contentPath defaults to `content/posts`
        - assetPath defaults to `content/assets`
        - mdx defaults to `true`
        */
        basePath: `/blog`,
        contentPath: `content/blogPosts`,
        assetPath: `content/blogAssets`,
        mdx: false,
      },
    },
  ],
}
```

### 2. O starter cria exemplos de posts no blog.

```md:title=/content/posts/hello-world.mdx
---
title: Hello, world!
path: /hello-world
---

I'm an example post!
```

Assim que você fizer algumas edições, rode `gatsby develop` para iniciar o servidor de desenvolvimento e ver as alterações no navegador

## Atualizando um tema

Para carregar as últimas atualizações do seu tema, você pode atualizar a versão do `gatsby-theme-blog` no `package.json` do seu site.

Você pode fazer isso rodando o instalador do pacote do tema novamente: `npm install --save gatsby-theme-blog`.
