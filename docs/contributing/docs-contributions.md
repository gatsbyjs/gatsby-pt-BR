---
title: Contribuições para as Documentações
---

Gatsby, sem surpresas, usa Gatsby para o site de sua documentação. Agradecemos antecipadamente por contribuir com a documentação do Gatsby! Em fevereiro de 2019, mais de 800 pessoas já haviam contribuído. São pessoas como você que tornam essa comunidade ótima!

> _Quando decidir para onde contribuir com o Gatsby (documentações ou [blog](/contributing/blog-and-website-contributions/)?), veja a página com os [templates de documentações](/contributing/docs-templates/)._

## Principais prioridades

Procure no repositório do GitHub por _issues_ marcadas com ["documentation" e "good first issue"](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22type%3A+documentation%22+label%3A%22good+first+issue%22) para sua primeira contribuição com o Gatsby, ou ["documentation" e "help wanted"](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22type%3A+documentation%22+label%3A%22help+wanted%22) para ver todas as _issues_ de documentação prontas para receber ajuda da comunidade. Depois de abrir um _pull request_ para solucionar uma das _issues_, você pode remover a _label_ "help wanted". Além disso, dê uma conferida na lista de artigos que não foram totalmente detalhados na [lista de esboços](/contributing/stub-list).

## Opções para contribuir com as documentações do Gatsby

Ao trabalhar na documentação do Gatsby.js, você pode escolher entre duas formas de trabalhar mais comuns:

- [Trabalhar diretamente na UI do GitHub](#modificando-arquivos-em-markdown), usando o _"Edit this File"_ e a função de _commit_. Isso é útil para atualizações rápidas da documentação, correções de erros de digitação e pequenas alterações no Markdown.
- Clone o repositório do Gatsby.js e configure para que o site dentro de `www` rode localmente. Isso é necessário para obter um conteúdo mais completo da documentação e de alterações na infraestrutura. Aprenda como configurar usando as [instruções para configurar a documentação do Gatsby](#instruções-para-configurar-a-documentação-do-Gatsby).

## Corrigindo o caminho de links e imagems

Se você encontrar uma URL de uma imagem corrompida na documentação do Gatsby, ela deve ser corrigida e mantida em relação à origem do site, ao invés de vinculado ao repositório remoto no GitHub. Isso garante que, quando o site for publicado, todas as imagens sejam incluídas na compilação.

Para resolver as imagens ausentes, consulte a fonte do documento ou do tutorial [no repositório do Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/docs) para ver, no histórico, se foram movidas e se as imagens ainda estão no local antigo. Verifique se essas imagens também são referenciadas em mais de um documento. Se não estiverem, mova-as para o novo diretório (e atualize as referências de URL relativas ao conteúdo, se necessário). Se elas estiverem sendo referenciados em mais de um local, use caminhos relativos e não duplique imagens.

Se você encontrar um link quebrado na documentação do Gatsby, fique à vontade para corrigí-lo e enviar um PR!

Lembre-se de que alguns links aqui já estão corretos porque funcionam no gatsbyjs.org. Embora seja bom ter links na documentação funcionando no GitHub, tê-los funcionando no gatsbyjs.org é prioritário!

## Títulos

Documentos com o _frontmatter_ no topo, com um `title` receberão um título `<h1>` na página renderizada, e este deve ser único. Títulos adicionais devem começar pelo `<h2>`, marcados com `##` no Markdown.

Para fins de tornar o documento acessível, os títulos do conteúdo devem ir de h2-h4 (`####`) até que todos os níveis tenham sido estabelecidos. Isso garantirá que os documentos do Gatsby tenham uma hierarquia de conteúdo que funcione bem para usuários de tecnologia assistida. Leia mais sobre a importância de [títulos e estrutura semântica no HTML](https://webaim.org/techniques/semanticstructure/).

## Modificando arquivos em Markdown

> 💡 Primeira vez escrevendo Markdown? Veja o [guia para Markdown do Gatsby](/docs/mdx/markdown-syntax/)!

1. Se você deseja adicionar ou modificar qualquer documentação do Gatsby, vá para a [pasta documentos](https://github.com/gatsbyjs/gatsby/tree/master/docs) ou para a [pasta _contributing_](https://github.com/gatsbyjs/gatsby/tree/master/docs/contributing) no GitHub e use o editor de arquivos para editar e visualizar suas alterações.
2. Antes de enviar suas modificações e abrir o PR na UI, você precisa ter certeza que seu PR está de acordo com os critérios de contribuição para as documentações:
   - Seguindo os padrões descritos no [Guia de Estilo do Gatsby](/contributing/gatsby-style-guide/).
   - Se o seu PR não tem como origem uma _issue_ escrita pelo _core team_, adicione um comentário no seu PR, explicando porque sua alteração deveria ser incluída na documentação, de acordo com os [quesitos para decisão da Documentação](/blog/2018-10-12-uptick-docs-contributions-hacktoberfest/#docs-decision-tree-and-examples).
     > Nota: Se a sua _issue_ e/ou PR não atender aos critérios de contribuição acima, ela poderá receber um comentário para lembrá-lo. Se, após duas semanas, essas alterações não tiverem sido feitas, sua _issue_ e/ou PR poderá ser encerrada, o que nos ajudará a triar _issues_ e PRs com eficiência. Você pode solicitar que seja reaberta se, e quando, estiver pronto para fazer as atualizações necessárias.
3. O GitHub permite você modificar e abrir um PR na própria UI. Essa é a forma mais fácil de contribuir com o projeto!

### Convertendo um documento a partir de um esboço

Se você escreveu um novo documento que era [anteriormente um esboço](/contributing/how-to-write-a-stub/), existem duas coisas que precisam ser atualizadas.

1. Remova o _frontmatter_ que tem o link para a issue

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

- Pré-requisitos: instale o Node.js e Yarn. Veja as [instruções de configuração de desenvolvimento](/contributing/setting-up-your-local-dev-environment/).
- [Faça um fork e clone o repositório do Gatsby](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions).
- Para mudanças únicas nos documentos, considere usar `git checkout -b docs/some-change` ou `git checkout -b docs-some-change`, isto parará o processo de CI e rodará apenas tarefas de limpeza.
- Altere os diretórios para a pasta de documentos do site: `cd www`
- Instale as dependências com Yarn: `yarn install`
- Adicione a variável _env_ para um arquivo `.env.development` dentro do diretório `www` para [habilitar imagens de placeholders](https://github.com/gatsbyjs/gatsby/tree/master/www#running-slow-build-screenshots-placeholder):`GATSBY_SCREENSHOT_PLACEHOLDER=true`. Isto irá aumentar a velocidade de _build_ do documento do site significativamente!
- Certifique-se de que você tem o Gatsby CLI instalado com `gatsby -v`, caso não, execute `yarn global add gatsby-cli`
- Inicie uma _build_ de `www` com `gatsby develop`.
- Edite arquivos de marcação nas pastas [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs) e [contribuição](https://github.com/gatsbyjs/gatsby/tree/master/docs/contributing), assim como [arquivos YAML de _sidebar_](https://github.com/gatsbyjs/gatsby/tree/master/www/src/data/sidebars).
- Veja as mudanças no seu navegador em `http://localhost:8000`.
- _Commit_ suas alterações e [envie um pull request](/contributing/how-to-open-a-pull-request/)!

## Alterando headers

Pode ser necessário alterar o _heading_ dentro dos documentos. É importante notar que os _headers_ geram automaticamente links com uma URL correspondente, que podem ser vinculados à outras partes do site, por meio de _deep-link_. Ao alterá-lo, assegure-se de redirecionar todos os links correspondentes à nova URL. Estas são algumas dicas de como realizar:

- Determinar a URL que você procura. `Changing headers` está vinculada com a URL terminada em `changing-headers`, `Docs renaming instructions` se torna `docs-renaming-instructions`, etc.
- Atualizar todas as instâncias da antiga URL para a nova. [Encontrar e substituir](https://code.visualstudio.com/docs/editor/codebasics#_search-across-files) no VS Code pode ajudar. Assegure-se que ainda há sentido quanto ao contexto de referência do link original com o novo.

## Adicionando uma nova descrição

O site cria automaticamente _tags_ de descrição para otimizar o SEO:

```html
<meta name="description" content="Documentação do Gatsby" />
<meta property="og:description" content="Documentação do Gatsby" />
<meta name="twitter:description" content="Documentação do Gatsby" />
```

Por padrão, esta descrição é gerada a partir da `page.excerpt`. Caso queira adicionar uma descrição customizada, você pode usar a _frontmatter tag_ `decription`:

```markdown
---
title: Eventos da comunidade do Gatsby
description: Aprenda sobre outros eventos acontecendo pelo mundo para conectar-se com outros membros da comunidade do Gatsby
---
```

## Configurando a navegação do site

Os documentos incluem componentes customizáveis para ajudar na navegação. Para personalizar a experiência de navegação, estes componentes permitem algumas configurações sem alterar quaisquer códigos do React.

### Ajustando títulos _breadcrumb_

O componente `<Breadcrumb />` é usado em arquivos de _layout_ para exibir a hierarquia das páginas que um usuário está navegando no topo do documento.
Para alterar o título de um documento mostrado no componente _Breadcrumb_, `breadcrumbTitle` é aceito como _key_ nos [arquivos YAML da _sidebar_](https://github.com/gatsbyjs/gatsby/tree/master/www/src/data/sidebars). Isto é comumente usado para fornecer uma versão abreviada do título de um documento quando este é mostrado ao lado do título da página pai, por exemplo, encurtando "Adicionando uma configuração personalizada do webpack" para "webpack Config".

```yaml
- title: Adicionando transição de páginas
  link: /docs/adding-page-transitions/
  breadcrumbTitle: Transição de Páginas # linha-realçada
```

### Desabilitando ou abreviando Tabela de Conteúdos

O componente `<TableOfContents />` é usado para renderizar uma lista de _subheaders_ de uma página documentos e, automaticamente, prover _deep links_ para estes. Pode ser ajustado por valores definidos no _frontmatter_ de um markdown do documento.

Em documentos que a Tabela de Conteúdo não é requerida e deve ser desabilitada, uma _key_ no _frontmatter_ chamada `disableTableOfContents` pode ser definida como `true`, desta forma:

```markdown
---
title: Glossário
disableTableOfContents: true
---

Quando você é novato no Gatsby, pode haver diversas palavras para se aprender...
```

Em outros documentos em que a Tabela de Conteúdo é extremamente longa, pode fazer sentido mostrar apenas os _headers_ do documento até um certo nível, em vez de todos os _subheadings_. Você pode definir a _key_ `tableOfContentsDepth` como um número que irá limitar as _subheadings_ mostradas na tabela de conteúdos a esta "profundidade". Caso esta seja definida para 2, os _headers_ `<h2>`/`##`, e `<h3>`/`###` serão listados, caso seja definida para 3, `<h2>`/`##`, `<h3>`/`###`, and `<h4>`/`####` serão todos mostrados. Caso esteja definida assim:

```markdown
---
title: Glossário
tableOfContentsDepth: 2
---

Quando você é novato no Gatsby, pode haver diversas palavras para se aprender...
```

## Incluindo exemplos incorporados do GraphQL

Existem exemplos incorporados em vários locais nos documentos (como o [Guia de Referência do GraphQL](/docs/graphql-reference/)) que provém uma versão funcional do código descrito. No exemplo específico da Página de Referência de Opções de Consulta do GraphQL, estes exemplos da interface do GraphiQL mostra como os dados podem ser consultados a partir da camada de dados do Gatsby.

Para escrever um novo exemplo do GraphQL, um projeto Codesandbox com um site Gatsby pode ser aberto no link do _container_ do servidor, por exemplo: [https://711808k40x.sse.codesandbox.io/](https://711808k40x.sse.codesandbox.io/). Como o Codesandbox está rodando um site Gatsby em [modo _`develop`_ em vez do modo _`build`_](/docs/overview-of-the-gatsby-build-process/), você pode navegar para GraphiQL adicionando `/___graphql` ao link. Escreva uma consulta de exemplo e, quando estiver satisfeito, os campos e nomes da consulta serão salvos como parâmetros da URL, assim você poderá compartilhar o link. Copie a URL e use-a no `src` de um iframe:

```mdx
Aqui está um exemplo de uma consulta GraphQL no código:

<iframe src="https://711808k40x.sse.codesandbox.io/___graphql?query=query%20TitleQuery%20%7B%0A%20%20site%20%7B%0A%20%20%20%20siteMetadata%20%7B%0A%20%20%20%20%20%20title%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false&operationName=TitleQuery" /> // linha-realçada

Mais conteúdo de markdown...
```

>Note que você deve definir o parâmetro `explorerIsOpen` na URL para `false` caso não esteja.

## Instruções de renomeação de documentos

Às vezes faz sentido mover ou renomear um arquivo, como parte da reestruturação da documentação ou para esclarecimento de um conteúdo. Embora seja recomendável manter as URLs consistentes da melhor maneira possível, aqui estão algumas dicas para minimizar erros e manter as documentações em bom estado:

- Execute as alterações de estrutura propostas pela equipe de documentação do Gatsby em [um _issue_ do GitHub](/contributing/how-to-file-an-issue/) para garantir que sua alteração será aceita.
- Atualize todas as instâncias da antiga URL para a nova. [Encontrar e substituir](https://code.visualstudio.com/docs/editor/codebasics#_search-across-files) no VS Code pode ajudar. Assegure-se que ainda há sentido quanto ao contexto de referência do link original com o novo.
- Para fins de SEO, adicione um redirecionamento para [`www/redirects.yaml`](https://github.com/gatsbyjs/gatsby/tree/master/www/redirects.yaml). Aqui está um exemplo:

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
