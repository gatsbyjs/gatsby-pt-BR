---
title: Contribuições para as Documentações
---

Gatsby, sem surpresas, usa Gatsby para o site de sua documentação. Agradecemos antecipadamente por contribuir com a documentação do Gatsby! Em fevereiro de 2019, mais de 800 pessoas já haviam contribuído. São pessoas como você que tornam essa comunidade ótima!

> _Ao decidir para onde contribuir com o Gatsby (documentações ou [blog](/contributing/blog-and-website-contributions/)?), veja a página com os [templates de documentações](/contributing/docs-templates/)._

## Principais prioridades

Procure no repositório do GitHub por _issues_ marcadas com ["documentation" e "good first issue"](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22type%3A+documentation%22+label%3A%22good+first+issue%22) para sua primeira contribuição com o Gatsby, ou ["documentation" e "help wanted"](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22type%3A+documentation%22+label%3A%22help+wanted%22) para ver todas as _issues_ de documentação prontas para receber ajuda da comunidade. Depois de abrir um _pull request_ para solucionar uma das _issues_, você pode remover a _label_ "help wanted". Além disso, dê uma conferida na lista de artigos que não foram totalmente detalhados na [lista de esboços](/contributing/stub-list).

## Opções para contribuir com as documentações do Gatsby

Ao trabalhar na documentação do Gatsby.js, você pode escolher entre duas, mais comuns, formas de trabalhar:

- [Trabalhar diretamente na UI do GitHub](#modificando-arquivos-em-markdown), usando o _"Edit this File"_ e a função de _commit_. Isso é útil para atualizações rápidas da documentação, correções de erros de digitação e pequenas alterações no Markdown.
- Clone o repositório do Gatsby.js e configure para que o site dentro de `www` rode localmente. Isso é necessário para obter um conteúdo mais completo da documentação e de alterações na infraestrutura. Aprenda como configurar usando as [instruções para configurar a documentação do Gatsby](#instruções-para-configurar-a-documentação-do-Gatsby).

## Corrigindo o caminho de links e imagems

Se você encontrar uma URL de uma imagem corrompida na documentação do Gatsby, ela deve ser corrigida e mantida em relação à origem do site, ao invés de vinculado ao repositório remoto no GitHub. Isso garante que, quando o site for publicado, todas as imagens sejam incluídas na compilação.

Para resolver as imagens faltantes, consulte a fonte do documento ou tutorial [no repositório do Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/docs) ver no histórico se foram movidas e se as imagens ainda estão no local antigo. Verifique se essas imagens também são referenciadas em mais de um documento. Se não estiverem, mova-os para o novo diretório (e atualize as referências de URL relativas ao conteúdo, se necessário). Se eles estiverem sendo referenciados em mais de um local, use caminhos relativos e não duplique imagens.

Se você encontrar um link quebrado na documentação do Gatsby, fique à vontade para corrigí-lo e enviar um PR!

Lembre-se de que alguns links aqui já estão corretos porque funcionam no gatsbyjs.org. Embora seja bom ter links na documentação funcionando no GitHub, tê-los funcionando no gatsbyjs.org é prioritário!

## Títulos

Documentos com o _frontmatter_ no topo, com um `title` receberão um título `<h1>` na página renderizada, e este deve ser único. Títulos adicionais devem começar pelo `<h2>`, marcados com `##` no Markdown.

Para fins de tornar o documento acessível, os títulos do conteúdo devem ir de h2-h4 (`####`) até que todos os níveis tenham sido estabelecidos. Isso garantirá que os documentos do Gatsby tenham uma hierarquia de conteúdo que funcione bem para usuários de tecnologia assistida. Leia mais sobre a importância de [títulos e estrutura semântica no HTML](https://webaim.org/techniques/semanticstructure/).

## Modificando arquivos em Markdown

> 💡 Primeira vez escrevendo Markdown? Veja o [guia para Markdown do Gatsby](/docs/mdx/markdown-syntax/)!

1. Se você deseja adicionar/modificar qualquer documentação do Gatsby, vá para a
   [pasta _docs_](https://github.com/gatsbyjs/gatsby/tree/master/docs) ou para a [pasta _contributing_](https://github.com/gatsbyjs/gatsby/tree/master/docs/contributing) no GitHub e 
   use o editor de arquivos para editar e visualizar suas alterações.
2. Antes de enviar suas modificações e abrir o PR na UI, você precisa ter certeza que seu PR está de acordo com os critérios de contribuição para as documentações:
   - Seguindo os padrões descritos no [Guia de Estilo do Gatsby](/contributing/gatsby-style-guide/).
   - Se o seu PR não tem como origem uma issue escrita pelo _core team_, adicione um comentário no seu PR, explicando porque sua alteração deveria ser incluída na documentação, de acordo com os [quesitos para decisão da Documentação](/blog/2018-10-12-uptick-docs-contributions-hacktoberfest/#docs-decision-tree-and-examples).
     > Nota: Se a sua _issue_ e/ou PR não atender aos critérios de contribuição acima, ele poderá receber um comentário para lembrá-lo. Se, após duas semanas, essas alterações não tiverem sido feitas, sua _issue_ e/ou PR poderá ser encerrado, o que nos ajudará a triar _issues_ e PRs com eficiência. Você pode solicitar que seja reaberto se e quando estiver pronto para fazer as atualizações necessárias.
3. O GitHub permite você modificar e abrir um PR na própria UI. Essa é a forma mais fácil de contribuir com o projeto!

### Convertendo um documento a partir de um esboço

Se você escreveu um novo documento que era [anteriormente um esboço](/contributing/how-to-write-a-stub/), existem duas coisas que precisam ser atualizadas.

1. Remova o _frontmatter_ que tem o _link_ para a issue

```diff:title=docs/docs/example-doc.md
  ...
    title: Documento de exemplo
- - issue: https://github.com/gatsbyjs/gatsby/issues/00000
+ -
  ...
```

2. Edite o arquivo `www/src/data/sidebars/doc-links.yaml` removendo o asterisco antes do título do documento:

```diff:title=www/src/data/sidebars/doc-links.yaml
  ...
- - title: Documento de exemplo*
+ - title: Documento de exemplo
    link: /docs/example-document/
  ...
```

3. (Opcional) se o título parecer longo, considere adicionar um `breadcrumbTitle` no arquivo `doc-links.yaml`, isso é uma versão curta do seu título, a qual será mostrada como um _breadcrumb_ na página de documentação.

```diff:title=www/src/data/sidebars/doc-links.yaml
  ...
  - title: Exemplo de título muito grande, mas muito grande mesmo, da documentação
    link: /docs/example-document/
+   breadcrumbTitle: Título curto exibido
  ...
```

## Instruções para configurar a documentação do Gatsby

Depois de passar pelas [instruções de configuração para desenvolvimento](/contributing/setting-up-your-local-dev-environment/), existem algumas informações adicionais que você deve saber ao configurar o [site da documentação do Gatsby.js](/docs/), que está em sua maior parte nos diretórios [www](https://github.com/gatsbyjs/gatsby/tree/master/www) e [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs). Temos alguns [exemplos](https://github.com/gatsbyjs/gatsby/tree/master/examples) no repositório, os quais são referenciados na documentação.

<!-- - Prerequisites: install Node.js and Yarn. See [development setup instructions](/contributing/setting-up-your-local-dev-environment/).
- [Fork and clone the Gatsby repo](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions).
- For docs-only changes, consider using `git checkout -b docs/some-change` or `git checkout -b docs-some-change`, as this will short circuit the CI process and only run linting tasks.
- Change directories into the docs site folder: `cd www`
- Install dependencies with Yarn: `yarn install`
- Add the following env variable to an `.env.development` file inside the `www` directory to [enable image placeholders](https://github.com/gatsbyjs/gatsby/tree/master/www#running-slow-build-screenshots-placeholder): `GATSBY_SCREENSHOT_PLACEHOLDER=true`. This will speed up building the docs site significantly!
- Make sure you have the Gatsby CLI installed with `gatsby -v`, if not run `yarn global add gatsby-cli`
- Start a build of `www` with `gatsby develop`.
- Edit Markdown files in the [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs) and [contributing](https://github.com/gatsbyjs/gatsby/tree/master/docs/contributing) folders, as well as the [YAML sidebar files](https://github.com/gatsbyjs/gatsby/tree/master/www/src/data/sidebars).
- View the changes in your browser at `http://localhost:8000`.
- Commit your changes and [submit a pull request](/contributing/how-to-open-a-pull-request/)!

## Changing headers

It can be necessary to change a heading within the docs. It's important to note that headers automatically generate links with a corresponding URL that can be deep-linked from elsewhere on the site. When changing a header, be sure to point all corresponding links to the new URL. Here are some workflow tips:

- Determine the URL you're looking for. `Changing headers` is linked with a URL ending in `changing-headers`, `Docs renaming instructions` becomes `docs-renaming-instructions`, etc.
- Update all instances of the old URL to your new one. [Find and replace](https://code.visualstudio.com/docs/editor/codebasics#_search-across-files) in VS Code can help. Check that the context of the original link reference still makes sense with the new one.

## Adding a description

The site automatically creates description tags in order to boost SEO:

```html
<meta name="description" content="Documentation of Gatsby" />
<meta property="og:description" content="Documentation of Gatsby" />
<meta name="twitter:description" content="Documentation of Gatsby" />
```

By default, this description is generated from the `page.excerpt`. If you would like to add a custom description, you can use the `description` frontmatter tag:

```markdown
---
title: Gatsby Community Events
description: Learn about other events happening around the globe to connect with other members of the Gatsby community
---
```

## Configuring site navigation

The docs include custom built components to aid with navigation. In order to customize the navigation experience, these components allow some configurations without changing any of the React code.

### Adjusting breadcrumb titles

The `<Breadcrumb />` component is used in layout files to display the hierarchy of pages a user is currently browsing on at the top of each doc.

To alter the title of a doc that is displayed in the Breadcrumb component, `breadcrumbTitle` is supported as a key in the [sidebar YAML files](https://github.com/gatsbyjs/gatsby/tree/master/www/src/data/sidebars). It is commonly used to provide an abbreviated version of a doc's title when displayed next to its parent page title, e.g. shortening "Adding a Custom webpack Config" to "webpack Config".

```yaml
- title: Adding Page Transitions
  link: /docs/adding-page-transitions/
  breadcrumbTitle: Page Transitions # highlight-line
```

### Disabling or shortening Table of Contents

The `<TableOfContents />` component is used to render a list of subheaders from a docs page and automatically provide deep links to them. It can be tweaked by values set in the frontmatter of a doc's markdown.

In docs where the Table of Contents isn't required and should be disabled, a key in the frontmatter called `disableTableOfContents` can be set to `true` like this:

```markdown
---
title: Glossary
disableTableOfContents: true
---

When you're new to Gatsby there can be a lot of words to learn...
```

In other docs where the Table of Contents is extremely long it can make sense to only show headers from the doc up to a certain level, rather than all subheadings. You can set the `tableOfContentsDepth` key to a number that will limit the subheadings shown in the table of contents to that "depth". If it is set to 2, `<h2>`/`##`, and `<h3>`/`###` headers will be listed, if set to 3, `<h2>`/`##`, `<h3>`/`###`, and `<h4>`/`####` will all be shown. It is set like this:

```markdown
---
title: Glossary
tableOfContentsDepth: 2
---

When you're new to Gatsby there can be a lot of words to learn...
```

## Adding embedded GraphQL examples

There are embedded examples in a few places in the docs (like the [GraphQL Reference guide](/docs/graphql-reference/)) that provide a working version of the code described. In the specific example of the GraphQL Query Options Reference page, these examples of the GraphiQL interface show how data can be queried from Gatsby's data layer.

To write a new GraphQL example, a Codesandbox project with a Gatsby site can be opened at its server container link, for example: [https://711808k40x.sse.codesandbox.io/](https://711808k40x.sse.codesandbox.io/). Because Codesandbox is running a Gatsby site in [`develop` mode instead of `build` mode](/docs/overview-of-the-gatsby-build-process/) you can navigate to GraphiQL by adding `/___graphql` to the link. Write an example query, and when you have a query you are satisfied with, the query fields and names will be saved as URL parameters so you can share the link. Copy the URL and use it as the `src` of an iframe:

```mdx
Here's an example of a GraphQL query inline:

<iframe src="https://711808k40x.sse.codesandbox.io/___graphql?query=query%20TitleQuery%20%7B%0A%20%20site%20%7B%0A%20%20%20%20siteMetadata%20%7B%0A%20%20%20%20%20%20title%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false&operationName=TitleQuery" /> // highlight-line

More markdown content...
```

> Note that you should set the `explorerIsOpen` parameter in the URL to `false` if it isn't already. -->

## Docs renaming instructions

Às vezes faz sentido mover ou renomear um arquivo, como parte da reestruturação da documentação ou para esclarecimento de um conteúdo. Embora seja recomendável manter as URLs consistentes da melhor maneira possível, aqui estão algumas dicas para minimizar erros e manter as documentações em bom estado:

<!-- - Run proposed structure changes by the Gatsby docs team in [a GitHub issue](/contributing/how-to-file-an-issue/) to ensure your change is accepted.
- Update all instances of the old URL to your new one. [Find and replace](https://code.visualstudio.com/docs/editor/codebasics#_search-across-files) in VS Code can help. Check that the context of the original link reference still makes sense with the new one.
- For SEO purposes, add a redirect to [`www/redirects.yaml`](https://github.com/gatsbyjs/gatsby/tree/master/www/redirects.yaml). Here's an example: -->

```yaml:title=www/redirects.yaml
- fromPath: /docs/source-plugin-tutorial/
  toPath: /docs/pixabay-source-plugin-tutorial/
```

## Solicite seu brinde

Após a sua primeira contribuição em um repositório Gatsby (incluindo documentação) você se torna elegível para ganhar uma camiseta ou um par de meias. Veja a [página de brindes](/contributing/contributor-swag/) para mais detalhes!

## Quer saber mais?

Confira nossas páginas adicionais sobre contribuições para documentações:

- [Gatsby Style Guide](/contributing/gatsby-style-guide/)
- [Templates de documentações](/contributing/docs-templates/)
- [Como escrever um esboço](/contributing/how-to-write-a-stub/)
