---
title: Contribuições para as Documentações
---

Gatsby, sem surpresas, usa Gatsby para a o site de sua documentação. Agradecemos antecipadamente e muito obrigado por contribuir com a documentação do Gatsby! Em fevereiro de 2019, mais de 800 pessoas já contribuíram. São pessoas como você que tornam essa comunidade ótima!

> _Ao decidir para onde contribuir com o Gatsby (documentações ou [blog](/contributing/blog-and-website-contributions/)?), veja a página com [templates de documentações](/contributing/docs-templates/)._

## Prioridades mais altas

Procure no repositório do GitHub pelas _issues_ marcadas com ["documentation" and "good first issue"](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22type%3A+documentation%22+label%3A%22good+first+issue%22) para sua primeira contribuição com o Gatsby, ou ["documentation" e "help wanted"](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22type%3A+documentation%22+label%3A%22help+wanted%22) para ver todas as _issues_ de documentação prontas para receber ajuda da comunidade. Depois de abrir um _pull request_ para solucionar uma das issues, você pode remover a _label_ "help wanted". Além disso, de uma conferida na lista de artigos que não foram totalmente detalhados na [lista de esboços](/contributing/stub-list).

## Opções para contribuir com as documentações do Gatsby

Ao trabalhar na documentação do Gatsby.js, você pode esconlher entre duas, mais comuns, formas de trabalhar:

- [Trabalhar diretamente na UI do GitHub](#modificando-arquivos-em-markdown), usando o _"Edit this File"_ e a função de _commit_. Isso é útil para atualizações rápidas da documentação, correções de erros de digitação e alterações pequenas no Markdown.
- Clone o repositório do Gatsby.js e configure para que o site dentro de `www` rode localmente. Isso é necessário para obter um conteúdo mais completo da documentação e alterações na infraestrutura. Aprenda a configurar usando as [instruções para configurar a documentação do Gatsby](#instruções-para-configurar-a-documentação-do-Gatsby).

## Corrigindo o caminho de link e imagem

Se você encontrar uma URL de uma imagem corrompida na documentação do Gatsby, ela deve ser corrigida e mantida em relação à origem do site, em vez de vinculado ao repositório remoto no GitHub. Isso garante que, quando o site for publicado, todas as imagens sejam incluídas na compilação.

Para resolver as imagens faltantes, consulte a fonte do documento ou tutorial [no repositório do Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/docs) ver no histórico se foi movida e se as imagens ainda estão no local antigo. Verifique se essas imagens também são referenciadas em mais de um documento. Se não estiverem, mova-os para o novo diretório (e atualize as referências de URL relativas ao conteúdo, se necessário). Se eles forem referenciados em mais de um local, use caminhos relativos e não duplique imagens.

Se você encontrar um link quebrado na documentação do Gatsby, fique à vontade para corrigi-lo e enviar um PR!

Lembre-se de que alguns links aqui já estão corretos porque funcionam no gatsbyjs.org. Embora seja bom ter links na documentação funcionando no GitHub, tê-los funcionando no gatsbyjs.org é prioritário!

## Títulos

Documentos com o _frontmatter_ no topo, com um `title` terão um título `<h1>` na página renderizada, e este deve ser único. Títulos adicionais devem começar pelo `<h2>`, marcados com `##` no Markdown.

Para fins de um documento acessível, os títulos do conteúdo devem ir de h2-h4 (`####`) até que todos os níveis tenham sido estabelecidos. Isso garantirá que os documentos do Gatsby tenham uma hierarquia de conteúdo que funcione bem para usuários de tecnologia assistida. Leia mais sobre a importância de [títulos e estrutura semântica no HTML](https://webaim.org/techniques/semanticstructure/).

## Modificando arquivos em Markdown

> 💡 Primeira vez escrevendo Markdown? Veja o [guia para Markdown do Gatsby](/docs/mdx/markdown-syntax/)!

1. Se você deseja adicionar / modificar qualquer documentação do Gatsby, vá para a
   [pasta _docs_](https://github.com/gatsbyjs/gatsby/tree/master/docs) ou para a [pasta _contributing_](https://github.com/gatsbyjs/gatsby/tree/master/docs/contributing) no GitHub e 
   use o editor de arquivos para editar e visualizar suas alterações.
2. Antes de enviar suas modificações e abrir o PR na UI, você precisa ter certeza que seu PR está de acordo com os critérios de contribuição para as documentações:
   - Seguindo os padrões descritos no [Guia de Estilo do Gatsby](/contributing/gatsby-style-guide/).
   - Se o seu PR não tem como origem uma issue escrita pelo _core team_, por favor adicione um comentário no seu PR, explicando o porque deveria ser incluido na documentação, de acordo com os [quesitos para decisão da Documentação](/blog/2018-10-12-uptick-docs-contributions-hacktoberfest/#docs-decision-tree-and-examples).
     > Nota: Se a sua _issue_ e/ou PR não atender aos critérios de contribuição acima, ele poderá receber um comentário para lembrá-lo. Se, após duas semanas, essas atualizações não tiverem sido feitas, sua _issue_ e/ou PR poderá ser encerrado, o que nos ajudará a triar _issues_ e PRs com eficiência. Você pode solicitar que seja reaberto se e quando estiver pronto para fazer as atualizações necessárias.
3. O GitHub permite você modificar e abrir um PR na própria UI. Essa é a forma mais fácil de contribuir com o projeto!

### Convertendo um documento a partir de um esboço

Se você escreveu um novo documento que era [anteriormente um esboço](/contributing/how-to-write-a-stub/), existe duas coisas que precisam ser atualizadas.

1. Remova o _frontmatter_ que tem o _link_ para a issue

```diff:title=docs/docs/example-doc.md
  ...
    title: Documento de exemplo
- - issue: https://github.com/gatsbyjs/gatsby/issues/00000
+ -
  ...
```

2. Edite o `www/src/data/sidebars/doc-links.yaml` revomendo o asterisco antes do título do documento:

```diff:title=www/src/data/sidebars/doc-links.yaml
  ...
- - title: Documento de exemplo*
+ - title: Documento de exemplo
    link: /docs/example-document/
  ...
```

3. (Opcional) se o nome do título parecer longo, considere adicionar um `breadcrumbTitle` no arquivo `doc-links.yaml`, isso e uma versão curta do seu título, a qual será mostrada no _breadcrumb_ na página de documentação.

```diff:title=www/src/data/sidebars/doc-links.yaml
  ...
  - title: Exemplo de título muito grande, mas muito grande mesmo, da documentação
    link: /docs/example-document/
+   breadcrumbTitle: Título curto para mostrar
  ...
```

## Instruções para configurar a documentação do Gatsby

Depois de passar pelas [instruções de configuração para desenvolvimento](/contributing/setting-up-your-local-dev-environment/), existe algumas informações adicionais que você deve saber ao configurar o [site da documentação do Gatsby.js](/docs/), que está em sua maior parte nos diretórios [www](https://github.com/gatsbyjs/gatsby/tree/master/www) e [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs). Temos alguns [exemplos](https://github.com/gatsbyjs/gatsby/tree/master/examples) no repostiório, os quais são referenciados na documentações.

- [Fork e Clone o repositório do Gatsby](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions).
- Para modificações apenas na documentação, considere usar `git checkout -b docs/some-change` ou `git checkout -b docs-some-change`, isso irá fazer com que o CI execute apenas as tarefas de _lint_
- Navegue até a pasta do site da documentação: `cd www`
- Instale as dependências Yarn: `yarn install`
- Adicione a seguinte variável de ambiente no arquivo `.env.development` dentro do diretório `www` para [habilitar as imagens temporárias](https://github.com/gatsbyjs/gatsby/tree/master/www#running-slow-build-screenshots-placeholder): `GATSBY_SCREENSHOT_PLACEHOLDER=true`. This will speed up building the docs site significantly!
- Começe o build do `www` com o comando `gatsby develop`.
- Edite os arquivos de Markdown dentro das pastas [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs) e [contributing](https://github.com/gatsbyjs/gatsby/tree/master/docs/contributing), bem como [os arquivos YAML da barra lateral](https://github.com/gatsbyjs/gatsby/tree/master/www/src/data/sidebars).
- Veja as modificações em `http://localhost:8000`.
- Commit suas modificações e [abra um pull request](/contributing/how-to-open-a-pull-request/)!

## Instruções para renomear documentações

Às vezes faz sentido mover ou renomear um arquivo, como parte da reestruturação da documentação ou para esclarecimento de um conteúdo. Embora seja recomendável manter as URLs consistentes da melhor maneira possível, aqui estão algumas dicas para minimizar erros e manter as documentações em bom estado:

- Execute as alterações de estrutura propostas conforme o time de documentação do Gatsby em [uma issue no GitHub](/contributing/how-to-file-an-issue/) para garantir que sua mudança seja aceita.
- Atualize todas as referências de URL antigas para a nova. O comando [Find and replace](https://code.visualstudio.com/docs/editor/codebasics#_search-across-files) do VS Code pode ajudar. Veja se o contexto original onde o link era usado ainda faz sentido como o novo.
- Para questões de SEO, adicione um redirecionamento na função `createPages` em [`www/gatsby-node.js`](https://github.com/gatsbyjs/gatsby/tree/master/www/gatsby-node.js). Aqui tem um exemplo:

```js:title=www/gatsby-node.js
createRedirect({
  fromPath: `/docs/source-plugin-tutorial/`,
  toPath: `/docs/pixabay-source-plugin-tutorial/`,
  isPermanent: true,
})
```

## Solicite seu brinde

Após seu primeiro código como contribuição (incluindo documentação) você torna-se elegível para ganhar uma camiseta ou um par de meias. Veja a página de [página de brindes](/contributing/contributor-swag/) para mais detalhes!

## Gostaria de mais?

Confira nossas páginas adicionais sobre contribuições para documentações:

- [Gatsby Style Guide](/contributing/gatsby-style-guide/)
- [Templates de documentações](/contributing/docs-templates/)
- [Como escrever um esboço](/contributing/how-to-write-a-stub/)
