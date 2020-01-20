---
title: Extraindo dados do Drupal
---

## Por que utilizar Drupal + Gatsby juntos?

Utilizar Drupal como um _headless CMS_ com Gatsby é uma ótima maneira de conseguir um CMS de qualidade empresarial grautitamente, pareando com uma maneira moderna de desenvolvimento, além de todos benefícios da JAMstack, como performace, escalabilidade, e segurança.

Só são necessários alguns passos para utilizar Gatsby com o Drupal como um _headless CMS_ .

[Um exemplo de _site_ Gatsby + Drupal](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-drupal)

## Como implementar Drupal + Gatsby

### Início Rápido

Esse guia assume que você já possui um projeto Gatsby configurado. Se você precisa configurar um projeto, dê uma olhada no [guia de Início Rápido](/docs/quick-start/), e então volte.

### gatsby-config.js

Conectar Gatsby a um novo ou já existente _site_ Drupal leva apenas alguns poucos passos.

- Siga as [instruções de instalações](/packages/gatsby-source-drupal/?=drupal) do plugin `gatsby-source-drupal` para adicioná-lo ao seu _site_ Gatsby.

Um exemplo de como incluir o plugin `gatsby-source-drupal` ao seu arquivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Gatsby com Drupal`,
  },
  plugins: [
    {
      resolve: `gatsby-source-drupal`,
      options: {
        baseUrl: `https://live-contentacms.pantheonsite.io/`,
        apiBase: `api`,
      },
    },
    {
      resolve: `gatsby-plugin-google-analytics`,
      options: {
        trackingId: `UA-93349937-2`,
      },
    },
    `gatsby-plugin-offline`,
    `gatsby-plugin-glamor`,
    `gatsby-plugin-sharp`,
    `gatsby-transformer-sharp`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography.js`,
      },
    },
  ],
}
```

## Por que utilizar Gatsby e Drupal juntos?

["Drupal Desacoplado”](https://www.acquia.com/drupal/decoupled-drupal) tem se tornado uma abordagem cada vez mais popular para construir sites de nivel empresarial, e tem [suporte completo](https://dri.es/how-to-decouple-drupal-in-2018) dos líderes da comunidade Drupal. Usar Gatsby em uma configuração de Drupal desacoplado permite ao seu time acessar as poderosas modelagens de conteúdo e capacidades de acesso de fluxo de trabalho do Drupal 8, além da performance e poderosa criação de UI do Gatsby.

## Quando o Drupal é uma boa opção?

Muitos times de desenvolvedores, times de conteúdo e clientes "tomadores de decisão" são familiares com o Drupal. Aqui temos alguns cenários nos quais o Drupal é uma boa escolha (e alguns cenários no qual ele não é uma escolha tão boa):

### Drupal é bom para:

- Complexos layouts de páginas ou modelagens de conteúdo com múltiplas seções por página
- Times de conteúdo com vários estágios de processos de criação e revisão
- Times de desenvolvimento que valorizam utilizar tecnologias populares e de código aberto

### Drupal não é tão bom para:

- Times de conteúdo que requerem uma experiência de edição de conteúdo fluida mesmo quando as múltiplas seções presentes se tornarem complexas
- Times que requerem utilizar o Drupal UI Kit já que este está constantemente em desenvolvimento e as vezes não funciona como o esperado

## Interessado em aprender mais?

Usar Gatsby junto com Drupal oferece uma poderosa, cheia de funcionalidades, de código aberto, e gratuita alternativa para caros CMS's de nível empresarial. Para aprender mais:

- Leia uma [Introdução ao Gatsby da agência do Drupal](https://www.mediacurrent.com/what-is-gatsby.js/)
- Assista a [Apresentação de Kyle Mathews sobre Gatsby + Drupal](https://2017.badcamp.net/session/coding-development/beginner/headless-drupal-building-blazing-fast-websites-reactgatsbyjs)
- Comece com o  [Tutorial sobre Drupal Desacoplado com Gatsby](https://evolvingweb.ca/blog/decoupling-drupal-gatsby) de Robert Ngo e assista sua [apresentação sobre Drupal na conferência Evolving Web 2018](https://www.youtube.com/watch?v=s5kUJRGDz6I)
- Site de exemplo que demonstra [como construir _sites_ Gatsby que utilizam dados do CMS Drupal](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-drupal).
- Participe de um [curso gratuito sobre como construir um _site_ Gatsby com Drupal](https://gatsbyguides.com/).
- Leia os [posts do blog do Gatsby sobre Gatsby + Drupal](/blog/tags/drupal/).
