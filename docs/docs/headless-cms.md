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
| [Contentful](https://www.contentful.com/)     | [guide](/docs/sourcing-from-contentful/)                                         | [docs](/packages/gatsby-source-contentful)           | [starter](/starters/contentful-userland/gatsby-contentful-starter/) |
| [NetlifyCMS](https://www.netlifycms.org/)     | [guide](/docs/sourcing-from-netlify-cms/)                                        | [docs](/packages/gatsby-plugin-netlify-cms)          | [starter](/starters/netlify-templates/gatsby-starter-netlify-cms/)  |
| [WordPress](https://www.wordpress.com/)       | [guide](/docs/sourcing-from-wordpress/)                                          | [docs](/packages/gatsby-source-wordpress)            |                                                                     |
| [Prismic](https://www.prismic.io/)            | [guide](/docs/sourcing-from-prismic/)                                            | [docs](/packages/gatsby-source-prismic)              |                                                                     |
| [Strapi](https://strapi.io/)                  | [guide](/blog/2018-1-18-strapi-and-gatsby/)                                      | [docs](/packages/gatsby-source-strapi)               |
| [DatoCMS](https://www.datocms.com/)           | [guide](https://www.gatsbyjs.com/guides/datocms/)                                | [docs](/packages/gatsby-source-datocms)              | [starter](/starters/datocms/gatsby-portfolio/)                      |
| [Sanity](https://www.sanity.io/)              | [guide](/docs/sourcing-from-sanity)                                              | [docs](/packages/gatsby-source-sanity/)              |
| [Drupal](https://www.drupal.com/)             | [guide](/docs/sourcing-from-drupal/)                                             | [docs](/packages/gatsby-source-drupal)               |                                                                     |
| [Shopify](https://www.shopify.com/)           |                                                                                  | [docs](/packages/gatsby-source-shopify)              |                                                                     |
| [CosmicJS](https://cosmicjs.com/)             | [guide](/blog/2018-06-07-build-a-gatsby-blog-using-the-cosmic-js-source-plugin/) | [docs](/packages/gatsby-source-cosmicjs)             | [starters](/starters/?s=cosmicjs&v=2)                               |
| [Contentstack](https://www.contentstack.com/) | [guide](/docs/sourcing-from-contentstack)                                        | [docs](/packages/gatsby-source-contentstack)         | [starter](/starters/contentstack/gatsby-starter-contentstack/)      |
| [ButterCMS](https://buttercms.com/)           | [guide](/docs/sourcing-from-buttercms/)                                          | [docs](/packages/gatsby-source-buttercms)            | [starter](/starters/ButterCMS/gatsby-starter-buttercms/)            |
| [Ghost](https://ghost.org/)                   | [guide](/docs/sourcing-from-ghost/)                                              | [docs](/packages/gatsby-source-ghost/)               | [starter](/starters/TryGhost/gatsby-starter-ghost/)                 |
| [Kentico Kontent](https://kontent.ai/)        | [guide](/docs/sourcing-from-kentico-kontent)                                     | [docs](/packages/@kentico/gatsby-source-kontent)     | [starter](/starters/Kentico/gatsby-starter-kontent/)                |
| [Directus](https://directus.io/)              |                                                                                  | [docs](/packages/gatsby-source-directus)             |
| [GraphCMS](https://graphcms.com/)             | [guide](/docs/sourcing-from-graphcms)                                            | [docs](/packages/gatsby-source-graphql)              | [starter](/starters/GraphCMS/gatsby-graphcms-tailwindcss-example/)  |
| [Storyblok](https://www.storyblok.com/)       |                                                                                  | [docs](/packages/gatsby-source-storyblok)            |
| [Cockpit](https://getcockpit.com/)            |                                                                                  | [docs](/packages/gatsby-plugin-cockpit)              |
| [CraftCMS](https://craftcms.com/)             |                                                                                  | [docs](/packages/gatsby-source-craftcms)             |
| [AgilityCMS](https://agilitycms.com/)         | [guide](/docs/sourcing-from-agilitycms/)                                         | [docs](/packages/@agility/gatsby-source-agilitycms/) | [starter](/starters/agility/agility-gatsby-starter/)                |
| [Forestry](https://forestry.io/)              | [guide](/docs/sourcing-from-forestry/)                                           |                                                      |                                                                     |
| [Gentics Mesh](https://getmesh.io)            | [guide](/docs/sourcing-from-gentics-mesh)                                        |                                                      |                                                                     |
| [Seams-CMS](https://seams-cms.com/)           | [guide](/docs/sourcing-from-seams-cms)                                           |                                                      |                                                                     |

## Como adicionar novos guias nesta seção

Se você não vê o seu CMS preferido nesta lista, você pode [escrever um novo guia você mesmo](/contributing/how-to-contribute/) ou [abrir uma issue para requisitar um](https://github.com/gatsbyjs/gatsby/issues/new/choose).

Você também pode [criar o seu próprio plugin fornecedor de dados](/docs/creating-a-source-plugin/) para integrar o Gatsby com um CMS que não está na lista.
