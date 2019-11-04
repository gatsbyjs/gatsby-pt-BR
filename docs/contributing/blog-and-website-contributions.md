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

Note: Before adding a blog post, ensure you have approval from a member of the Gatsby team. You should [open an issue](https://github.com/gatsbyjs/gatsby/issues/new/choose) or contact [@gatsbyjs on Twitter](https://twitter.com/gatsbyjs) before opening a PR with your blog post. Check out past blog posts for examples of posted content.

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

## Fazendo modificações no site

Se você deseja fazer alterações, melhorias ou adicionar novas funcionalidades ao site, não é necessário configurar o repositório completo do Gatsby para contribuir. Você pode criar sua própria instância do site do Gatsby com estas etapas:

- Clone [o repositório do Gatsby](https://github.com/gatsbyjs/gatsby/) e navegue até `/www`
- Execute `yarn` para instalar todas as dependências do site.
- Execute `npm run develop` para pré-visualizar o site em `http://localhost:8000/`.

> Nota: Se você estiver tendo problemas com uma máquina Linux, execute `sudo apt install libvips-dev`, para instalar uma dependência nativa. Você também pode consultar o [Guia para Gatsby no Linux](/docs/gatsby-on-linux/) para outros requisitos específicos do Linux'.

Agora você pode fazer e visualizar suas alterações antes de abrir seu pull request!

Para obter instruções completas de configuração do repositório, visite a página de [contribuições de código](/contributing/code-contributions/).
