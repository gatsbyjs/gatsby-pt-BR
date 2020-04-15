---
title: O que é um Headless CMS e como fornecer conteúdo através de um
overview: true
---

Um _headless CMS_ é um software para gerenciamento de conteúdo que permite a escritores produzirem e organizarem conteúdos, enquanto fornece aos desenvolvedores dados estruturados que podem ser exibidos utilizando um sistema separado no frontend de um site ou aplicativo. 

Um CMS monolítico, tradicional, é responsável tanto pelo gerenciamento do conteúdo no backend quanto por servir este conteúdo aos usuários finais. Em contraste, um headless CMS é desacoplado das preocupações do frontend, o que deixa os desenvolvedores livres para criar ricas experiências para os usuários finais utilizando as melhores tecnologias disponíveis.

Muitos sistemas gerenciadores de conteúdo (CMS) agora suportam um modo “headless” ou “desacoplado”, o que é perfeito para sites criados com Gatsby.

Através do uso de [plugins fornecedores de dados](/plugins/?=source), o Gatsby possui suporte a dezenas de opções de headless CMS permitindo a sua equipe de produção de conteúdo o conforto e a familiaridade do seu painel de administração preferido, e a sua equipe de desenvolvimento uma melhor experiência para o desenvolvedor e os ganhos de performance ao utilizar o Gatsby, GraphQL, e React para construir o frontend.

Os guias nesta seção irão te auxiliar através do processo de configuração do fornecimento de dados através de alguns dos mais populares headless CMS em uso da atualidade.
<GuideList slug={props.slug} />

<!--
  A ordenação nesta seção é direcionada pelos downloads dos plugins do Gatsby (/plugins/?=gatsby-source-) & pelo tamaho/adoção do fornecedor do CMS.
-->

Aqui estão mais recursos para guias, plugins e starters para sistemas CMS aos quais você pode se conectar:

| CMS                                           | Guias                                                                           | Documentação do Plugin                                          | Starter Oficial                                                    |
| --------------------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------- |
| [Contentful](https://www.contentful.com/)     | [guia](/docs/sourcing-from-contentful/)                                         | [documentação](/packages/gatsby-source-contentful)           | [starter](/starters/contentful-userland/gatsby-contentful-starter/) |
| [NetlifyCMS](https://www.netlifycms.org/)     | [guia](/docs/sourcing-from-netlify-cms/)                                        | [documentação](/packages/gatsby-plugin-netlify-cms)          | [starter](/starters/netlify-templates/gatsby-starter-netlify-cms/)  |
| [WordPress](https://www.wordpress.com/)       | [guia](/docs/sourcing-from-wordpress/)                                          | [documentação](/packages/gatsby-source-wordpress)            |                                                                     |
| [Prismic](https://www.prismic.io/)            | [guia](/docs/sourcing-from-prismic/)                                            | [documentação](/packages/gatsby-source-prismic)              |                                                                     |
| [Strapi](https://strapi.io/)                  | [guia](/blog/2018-1-18-strapi-and-gatsby/)                                      | [documentação](/packages/gatsby-source-strapi)               |
| [DatoCMS](https://www.datocms.com/)           | [guia](https://www.gatsbyjs.com/guides/datocms/)                                | [documentação](/packages/gatsby-source-datocms)              | [starter](/starters/datocms/gatsby-portfolio/)                      |
| [Sanity](https://www.sanity.io/)              | [guia](/docs/sourcing-from-sanity)                                              | [documentação](/packages/gatsby-source-sanity/)              |
| [Drupal](https://www.drupal.com/)             | [guia](/docs/sourcing-from-drupal/)                                             | [documentação](/packages/gatsby-source-drupal)               |                                                                     |
| [Shopify](https://www.shopify.com/)           |                                                                                  | [documentação](/packages/gatsby-source-shopify)              |                                                                     |
| [CosmicJS](https://cosmicjs.com/)             | [guia](/blog/2018-06-07-build-a-gatsby-blog-using-the-cosmic-js-source-plugin/) | [documentação](/packages/gatsby-source-cosmicjs)             | [starters](/starters/?s=cosmicjs&v=2)                               |
| [Contentstack](https://www.contentstack.com/) | [guia](/docs/sourcing-from-contentstack)                                        | [documentação](/packages/gatsby-source-contentstack)         | [starter](/starters/contentstack/gatsby-starter-contentstack/)      |
| [ButterCMS](https://buttercms.com/)           | [guia](/docs/sourcing-from-buttercms/)                                          | [documentação](/packages/gatsby-source-buttercms)            | [starter](/starters/ButterCMS/gatsby-starter-buttercms/)            |
| [Ghost](https://ghost.org/)                   | [guia](/docs/sourcing-from-ghost/)                                              | [documentação](/packages/gatsby-source-ghost/)               | [starter](/starters/TryGhost/gatsby-starter-ghost/)                 |
| [Kentico Cloud](https://kenticocloud.com/)    | [guia](/docs/sourcing-from-kentico-cloud)                                       | [documentação](/packages/gatsby-source-kentico-cloud)        | [starter](/starters/Kentico/gatsby-starter-kentico-cloud/)          |
| [Directus](https://directus.io/)              |                                                                                  | [documentação](/packages/gatsby-source-directus)             |
| [GraphCMS](https://graphcms.com/)             | [guia](/docs/sourcing-from-graphcms)                                            | [documentação](/packages/gatsby-source-graphql)              | [starter](/starters/GraphCMS/gatsby-graphcms-tailwindcss-example/)  |
| [Storyblok](https://www.storyblok.com/)       |                                                                                  | [documentação](/packages/gatsby-source-storyblok)            |
| [Cockpit](https://getcockpit.com/)            |                                                                                  | [documentação](/packages/gatsby-plugin-cockpit)              |
| [CraftCMS](https://craftcms.com/)             |                                                                                  | [documentação](/packages/gatsby-source-craftcms)             |
| [AgilityCMS](https://agilitycms.com/)         | [guia](/docs/sourcing-from-agilitycms/)                                         | [documentação](/packages/@agility/gatsby-source-agilitycms/) | [starter](/starters/agility/agility-gatsby-starter/)                |

## Como adicionar novos guias nesta seção

Se você não vê o seu CMS preferido nesta lista, você pode [escrever um novo guia você mesmo](/contributing/how-to-contribute/) ou [abrir uma issue para requisitar um](https://github.com/gatsbyjs/gatsby/issues/new/choose).

Você também pode [criar o seu próprio plugin fornecedor de dados](/docs/creating-a-source-plugin/) para integrar o Gatsby com um CMS que não está na lista.
