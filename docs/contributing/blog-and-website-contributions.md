---
title: Contribuições ao Blog & site
---

Nós sinceramente agradecemos as contribuições para o blog e o site do Gatsby! 

Aqui estão algumas coisas a ter em mente ao decidir para onde contribuir com o Gatsby:

- [Postagens de Blog](#contribuindo-para-o-blog): funcionam melhor para estudos de caso e narrações sensíveis ao tempo (veja o [formato de postagem do blog](#formato-de-postagem-do-blog)).
- [Docs](/contributing/docs-contributions/): são materiais de aprendizagem continuamente relevantes e notáveis, que vão além de qualquer estudo de caso ou outra situação.
- [Modificações do site](#fazendo-modificações-para-o-site): melhorias aqui são sempre bem-vindas!

## Contribuindo para o blog
Nota: Antes de adicionar uma postagem ao blog, certifique-se de ter a aprovação de um membro do time do Gatsby. Você pode fazer isso [abrindo uma issue](https://github.com/gatsbyjs/gatsby/issues/new/choose) ou entrando em contato com [@gatsbyjs no Twitter](https://twitter.com/gatsbyjs).

<<<<<<< HEAD
Para adicionar uma nova postagem ao blog do gatsbyjs.org:

- Clone [o repositório do Gatsby](https://github.com/gatsbyjs/gatsby/) e navegue até `/www`.
- Execute `yarn` para instalar todas as dependências do site ([Por que Yarn?](/contributing/setting-up-your-local-dev-environment#using-yarn))
- Execute `npm run develop` para pré-visualizar o blog em `http://localhost:8000/blog`.
- O conteúdo do blog fica na pasta `/docs/blog`. Faça modificações ou adições aqui.
- Adicione sua imagem de avatar em `/docs/blog/avatars`.
- Adicione seu nome no `/docs/blog/author.yaml`.
- Adiciome uma nova pasta seguindo o padrão `/docs/blog/yyyy-mm-dd-title`. Com essa pasta recém criada adicione um arquivo `index.md`.
- Adicione `title`, `date`, `author`, `excerpt`, e `tags` ao cabeçalho do seu `index.md`. Você pode [ver as tags existentes](/blog/tags/), ou [adicionar uma nova](https://github.com/gatsbyjs/gatsby/blob/master/www/src/data/tags-docs.js) se você acha que merece sua própria tag, no entanto recomendamos que você use as tags existentes.
- Se você estiver publicando sua postagem em outros lugares, você pode adicionar `canonicalLink` para obter benefícios no SEO. 
Você pode checar as outras postagens em `/docs/blog` como referência.
- Se a sua postagem contém imagens, você deve adicionar ela na pasta da sua postagem e referênciar ela no seu `index.md`.
- Certifique-se que todos links do gatsbyjs.org sejam relativos - `/contributing/how-to-contribute/` ao invés de `https://gatsbyjs.org/contributing/how-to-contribute`.
- Siga o [Guia de Estilo](/contributing/gatsby-style-guide/#word-choice) para ter certeza que você está usando as palavras apropriadas.
- Cheque novamente a gramática e adicione as letras maiúsculas corretamente.
- Faça o Commit e envie para o seu fork.
- Abra um pull request da sua branch.
  - Nós recomendamos usar o prefixo `docs`, ex. `docs/your-change` ou `docs-your-change`. ([Exemplo de PR](https://github.com/gatsbyjs/gatsby/commit/9c21394add7906974dcfd22ad5dc1351a99d7ceb#diff-bf544fce773d8a5381f64c37d48d9f12))

### Formato de postagem do Blog

O formato a seguir pode ajudá-lo a criar seu novo conteúdo para o blog. No topo está o "frontmatter" (cabeçalho): um nome mais elegante para metadados no Markdown. O cabeçalho para seu post deve incluir um título, data, um único autor (por hora, nós estamos aceitando issues/PR para isso) e uma ou mais tags. Seu conteúdo deve estar depois do segundo grupo de traços (`---`).

```md
---
title: "Sua grande postagem no blog"
date: YYYY-MM-DD
author: Jamie Doe
excerpt: "Aqui é um trecho útil ou breve descrição deste post."
tags:
  - awesome
  - post
---

Sua próxima grande postagem o aguarda!

Inclua imagens criando uma pasta para sua postagem e adicionando
Markdown e arquivos de imagem para facilitar a vinculação.

![exemplo fantástico](./image.jpg)
```
=======
If you'd like to contribute a post to the Gatsby blog, please review the process and guidelines outlined below and submit your
idea for the post to our [Gatsby blog proposal form](https://airtable.com/shr3449954866i3iF)

### Blog proposal submission process

1. Complete and submit the [Gatsby blog proposal form](https://airtable.com/shr3449954866i3iF).
2. A Gatsby team member will review your proposal and let you know if the proposal has been accepted within the next week or so.
   - **If the post is accepted:** A Gatsby team member will work with you on a timeline for submitting and reviewing a draft of your blog post and set a tentative publishing date.
   - **If the post is not accepted:** We’ll let you know if there are any alternative offers we can make (e.g. offer to retweet if you publish the piece elsewhere, suggest submitting it as an addition to a Gatsby doc, etc.). We’ll also do our best to explain why your proposal was not accepted and encourage you to revise your proposal based on that feedback and resubmit. Please don’t be discouraged from submitting another post in the future!

If you have any questions about the process or your submission, please email [marketing@gatsbyjs.com](mailto:marketing@gatsbyjs.com).

### Content guidelines for submitting a blog post proposal

As a Gatsby community member, you have unique insight into the ins and outs of learning Gatsby, building with Gatsby, and contributing to Gatsby’s open source community. Contributing to the Gatsby blog is a great way to share your experiences and insights. Here are some guidelines for what kind of content is and isn’t a good fit for the Gatsby blog.

Things we’re looking for in Gatsby blog content:

- Information to help others overcome challenges you’ve faced while working with Gatsby
- Stories about how Gatsby helped you overcome different challenges on work and personal projects
- Gatsby case studies
- Showcasing a tool, fix, or other content you or someone else have contributed to Gatsby’s open source community
- Showcasing a tool, fix, or other content someone else has contributed to Gatsby’s open source community
- Clear and thoughtful explanations of technical details or complex concepts related to React, GraphQL, web and application development, open-source contribution, Gatsby core, and other Gatsby-adjacent subject matter
- Guidance and resources for learning React, GraphQL, HTML/CSS, web development, best practices, accessibility, SEO, Gatsby, different tool and CMS integrations, and other Gatsby-adjacent subject matter.
- Other topics that you think would be valuable to people learning about or working with Gatsby

Things we’d like to avoid on the Gatsby blog:

- **Docs content.** Some content is better found in the Gatsby docs guides and tutorials, as it can be found in a section for related content and not buried under pages of other paginated blog posts.
- **Promotional content.** Please don’t submit content to the Gatsby blog solely for the purpose of promoting a product, yourself, or link-building.
  - **Here’s what you can do instead:** If you have a product or project you want to share on the Gatsby blog, focus on practical information, and make sure there’s a clear relationship with Gatsby or Gatsby-adjacent topics. You could write a step by step guide to using your product with Gatsby. You could write a case study highlighting the direct impact Gatsby had on your awesome project and offer helpful tips for others to recreate your success.
- **Content that doesn’t seem to have a clear benefit for Gatsby users and/or the Gatsby community.** For example, if you’re writing about a use-case or integration that’s extremely niche or unique to specific conditions that are really uncommon outside of your organization, the Gatsby blog might not be the best place for your content. Likewise, if your blog post doesn’t seem to have any direct relationship with Gatsby (or an interesting indirect relationship with Gatsby), then it may be more appropriate for a personal blog or another community blog.

**Please note** that these are guidelines, not rules. If you think your blog post belongs on the Gatsby blog, we absolutely encourage you to submit it. While we reserve the right to decide what is and isn’t appropriate for the Gatsby blog, we also value and encourage your creativity and your contributions.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

## Fazendo modificações no site

Se você deseja fazer alterações, melhorias ou adicionar novas funcionalidades ao site, não é necessário configurar o repositório completo do Gatsby para contribuir. Você pode criar sua própria instância do site do Gatsby com estas etapas:

- Clone [o repositório do Gatsby](https://github.com/gatsbyjs/gatsby/) e navegue até `/www`
- Execute `yarn` para instalar todas as dependências do site.
- Execute `npm run develop` para pré-visualizar o site em `http://localhost:8000/`.

> Nota: Se você estiver tendo problemas com uma máquina Linux, execute `sudo apt install libvips-dev`, para instalar uma dependência nativa. Você também pode consultar o [Guia para Gatsby no Linux](/docs/gatsby-on-linux/) para outros requisitos específicos do Linux'.

Agora você pode fazer e visualizar suas alterações antes de abrir seu pull request!

Para obter instruções completas de configuração do repositório, visite a página de [contribuições de código](/contributing/code-contributions/).
