---
Título: Adicionando o Arquivo _Manifest
---

Se você executou uma [verificação com o Lighthouse](/docs/audit-with-lighthouse/), pode ter notado uma pontuação ruim na categoria "Progressive Web App". Vamos abordar como você pode melhorar essa pontuação.

Mas primeiro, o que _são_ exatamente PWAs?

São sites regulares que aproveitam as funcionalidade modernas dos navegadores para aumentar a experiência na web com recursos e benefícios semelhantes a dos aplicativos. Confira [Google's overview](https://developers.google.com/web/progressive-web-apps/) para saber o que define uma experiência de PWA e [Progressive web apps (PWAs) doc](/docs/progressive-web-app/) para saber como um site Gatsby é um progressive web app.

A inclusão de um manifesto de aplicativo da web é um dos três, geralmente aceitos, [requisitos mínimos para um PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1).

Citação [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> O manifesto do aplicativo da web é um arquivo JSON simples que informa ao navegador sobre seu aplicativo web e como ele deve se comportar quando 'instalado' no dispositivo móvel ou na área de trabalho do usuário.

[Gatsby's manifest plugin](/packages/gatsby-plugin-manifest/) configura o Gatsby para criar um arquivo `manifest.webmanifest` em cada compilação do site.

### Usando `gatsby-plugin-manifest`

1.  Instale o plugin:

```shell
npm install --save gatsby-plugin-manifest
```

2. Adicione um favicon para o seu aplicativo em `src/images/icon.png`. O ícone é necessário para criar todas as imagens para o manifesto. Para mais informações, consulte os documentos em[`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Adicione o plugin ao array `plugins` no seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: "GatsbyJS",
        short_name: "GatsbyJS",
        start_url: "/",
        background_color: "#6b37bf",
        theme_color: "#6b37bf",
        // Ativa o prompt "Adicionar à tela inicial" e desativa a interface do usuário do navegador (incluindo o botão Voltar)
        // veja https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: "standalone",
        icon: "src/images/icon.png", // Esse caminho é relativo a raiz do site.
        // Um atributo opcional que fornece suporte para verificação CORS
        // Se você não fornecer a opção crossOrigin, ele pulará o CORS para manifesto
        // Qualquer palavra-chave inválida ou string vazia assume o padrão "anônimo"
        crossOrigin: `use-credentials`,
      },
    },
  ]
}
```

Isso é tudo o que você precisa para começar a adicionar um manifesto da web a um site do Gatsby. O exemplo dado reflete uma configuração básica - Confira [plugin reference](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) para mais opções.
