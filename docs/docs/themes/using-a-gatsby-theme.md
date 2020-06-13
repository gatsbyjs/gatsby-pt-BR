---
title: Usando um tema Gatsby
---

Além de você [iniciar rapidamente um novo projeto utilizando o starter de tema do Gatsby](docs/docs/themes/getting-started.md), você também pode instalar um tema Gatsby diretamente em um site Gatsby já existente. Os temas do Gatsby são plugins, então você pode [instalar e usar como qualquer outro plugin do Gatsby](docs/docs/using-a-plugin-in-your-site.md).

## Instalando um Tema

Como qualquer plugin do Gatsby, os temas do Gatsby são pacotes Node.js, então você pode instalá-los como qualquer outro pacote publicado em Node usando npm ou [yarn, incluindo workspaces locais](#using-yarn-workspaces).

Por exemplo, `gatsby-theme-blog` é o tema oficial do Gatsby para criar um blog.

Para instalá-lo, execute o comando na raiz do seu site:

```shell
npm install --save gatsby-theme-blog
```

## Opções de temas

Dependendo do tema, pode haver opções de temas a serem configuradas no arquivo `gatsby-config.js`

Por exemplo, `gatsby-theme-blog` pode conter 4 opções possíveis: `basePath`, `contentPath`, `assetPath`, e `mdx`. Estas opções também estão documentadas no arquivo [README do tema](/packages/gatsby-theme-blog/).

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

Para aprender como personalizar ainda mais um tema, confira as documentações em [Gatsby theme shadowing](/docs/themes/shadowing/).

## Publicando temas

Temas públicos do Gatsby são publicados no npm para todos utilizá-lo. Você também pode publicar um tema privado para usar na sua empresa. Exemplos de hospedagem de temas privados incluem o [npm registry](https://docs.npmjs.com/about-private-packages) e o [GitHub Package Registry](https://help.github.com/en/github/managing-packages-with-github-package-registry/about-github-package-registry).

## Usando Workspaces Yarn

Se você gostaria de trabalhar com temas não publicados, considere [configurar o Yarn Workspaces para o desenvolvimento de temas](/blog/2019-05-22-setting-up-yarn-workspaces-for-theme-development/) e [usando yarn](/docs/gatsby-cli/#how-to-change-your-default-package-manager-for-your-next-project) ao invés do npm.
