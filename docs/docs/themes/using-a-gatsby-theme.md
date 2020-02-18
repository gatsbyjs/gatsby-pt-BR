---
title: Usando um tema Gatsby
---

<<<<<<< HEAD
A forma mais rápida de usar um tema Gatsby é usando um starter que está configurado para usar o tema.

Por exemplo, `gatsby-starter-blog-theme` é um tema starter para o pacote `gatsby-theme-blog`.

Um **starter normal Gatsby** cria um novo site Gatsby que é pré-configurado para um uso específico. O site resultante é realmente uma bifurcação do starter — após criado, ele não mantém conexões com o starter.

Um **tema starter do Gatsby** cria um novo site Gatsby que instala e configura um ou mais temas. Quando um starter instala um tema, mantém-se a conexão com aquele tema como um pacote npm _standalone_.

Instalar um blog Gatsby a partir de um tema starter é o mesmo processo de um starter normal:
=======
While you can [get started quickly with a Gatsby theme starter](/docs/themes/getting-started/), you can also install a Gatsby theme directly to an existing Gatsby site. Gatsby themes are plugins, so you can [install and use them like any other Gatsby plugin](/docs/using-a-plugin-in-your-site/).

## Installing a Theme

Like any Gatsby plugin, Gatsby themes are Node.js packages, so you can install them like other published packages in Node using npm or [yarn, including local workspaces](#using-yarn-workspaces).

For example, `gatsby-theme-blog` is the official Gatsby theme for creating a blog.

To install it, run in the root of your site:
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
npm install --save gatsby-theme-blog
```

<<<<<<< HEAD
## O que um tema starter faz?

O starter oficial para o tema do blog faz o seguinte:

### 1. O starter instala o tema e o configura.

Quando você usa um starter que foi criado com um tema, você irá ver frequentemente que foi gerado uma versão mais leve do `gatsby-config.js`. Temas irão começar a fazer sua mágica quando instalados através do array `plugins`.
=======
## Theme options

Depending on the theme, there may be theme options that can be configured via `gatsby-config.js`.

For example, `gatsby-theme-blog` can take in 4 potential options: `basePath`, `contentPath`, `assetPath`, and `mdx`. These options are also documented in the [theme's README](/packages/gatsby-theme-blog/) file.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

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

<<<<<<< HEAD
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
=======
To learn how to further customize a theme, check out the docs on [Gatsby theme shadowing](/docs/themes/shadowing/).

## Published Themes

Public Gatsby themes are published on npm for anyone to use. You can also publish private themes for use by your organization. Examples of private theme package hosting include the [npm registry](https://docs.npmjs.com/about-private-packages) and [GitHub Package Registry](https://help.github.com/en/github/managing-packages-with-github-package-registry/about-github-package-registry).

## Using Yarn Workspaces

If you would like to work with unpublished themes, consider [setting up Yarn Workspaces for theme development](/blog/2019-05-22-setting-up-yarn-workspaces-for-theme-development/) and [using Yarn](/docs/gatsby-cli/#how-to-change-your-default-package-manager-for-your-next-project) instead of npm.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1
