---
title: Estrutura de um projeto em Gatsby
---

Dentro de um projeto Gatsby, você pode ver algumas ou todas as seguintes pastas e arquivos:

```
/
|-- /.cache
|-- /plugins
|-- /public
|-- /src
    |-- /pages
    |-- /templates
    |-- html.js
|-- /static
|-- gatsby-config.js
|-- gatsby-node.js
|-- gatsby-ssr.js
|-- gatsby-browser.js
```

### Pastas

- **`/.cache`** _Gerada automaticamente._ Essa pasta é um cache interno criado automaticamente pelo Gatsby. Os arquivos dentro desta pasta não são para ser modificados. Deve ser adicionado ao arquivo `.gitignore` se ainda não estiver adicionado.

- **`/public`** _Gerada automaticamente._ A saída do processo de _build_ será inserido dentro desta pasta. Deve ser adicionado ao arquivo `.gitignore` se ainda não estiver adicionado.

- **`/plugins`** Essa pasta contém qualquer plugin específico do projeto ("_local_") que não seja publicado como um pacote `npm`. Confira a documentação de [plugins](/docs/plugins) para mais detalhes.

- **`/src`** Esse diretório irá conter todo o código relacionado ao que você verá no _front-end_ do seu site (o que você vê no navegador), como o cabeçalho do site ou um _template_ de página. "Src" é uma convenção para "_source code_".

  - **`/pages`** Componentes no diretório src/pages se tornam páginas automaticamente com caminhos baseados no nome do arquivo. Confira a [documentação de páginas](/docs/recipes.md#criando-páginas-automaticamente) para mais detalhes.
  - **`/templates`** Contém modelos de programação para automatizar a criação de páginas. Confira a [documentação de _templates_](/docs/building-with-components/#page-template-components) para mais detalhes.
  - **`html.js`** Para customizar a configuração diferente do padrão de .cache/default_html.js. Confira a documentação, [customizando o html](/docs/custom-html/) para mais detalhes.

- **`/static`** Caso você coloque um arquivo na pasta _static_, ele não será processado pelo Webpack. Em vez disso, ele será copiado para a pasta _public_ sem ser modificado. Confira a documentação sobre [_assets_ estáticos](/docs/static-folder.md#adicionando-assets-fora-do-sistema-de-módulos) para mais detalhes.

### Arquivos

- **`gatsby-browser.js`**: Esse arquivo é onde o Gatsby espera encontrar qualquer uso das [APIs do navegador](/docs/browser-apis) (caso houver alguma). Isso permite a customização e modificação do padrão de configurações do Gatsby que afetam o navegador.

- **`gatsby-config.js`**: Esse é o principal arquivo de configuração de um _site_ Gatsby. É aqui que você pode especificar informações sobre seu _site_ (metadados), como o título e a descrição do site, quais plugins do Gatsby você gostaria de incluir, etc. Confira a [documentação das configurações](/docs/gatsby-config/) para mais detalhes.

- **`gatsby-node.js`**: Neste arquivo é onde o Gatsby espera encontrar o uso de [node APIs](/docs/node-apis/) (caso houver). Isso permite a personalização e modificação das configurações padrões do Gatsby que afetam partes do processo de _build_ do site.

- **`gatsby-ssr.js`**: Esse arquivo é o local onde o Gatsby espera encontrar qualquer uso de [APIs de renderização _server-side_](/docs/ssr-apis/) (caso houver). Isso permite a customização das configurações padrões do Gatsby que afetam a renderização _server-side_.

### Diversos

A estrutura de arquivos/pastas descrita acima reflete em arquivos e pastas específicos do Gatsby. Como os _sites_ Gatsby também são aplicações em React, é comum usar padrões de organização semelhantes como pastas de `/components` e `/utils` dentro do diretório `/src`. A [documentação do React](https://reactjs.org/docs/faq-structure.html) tem mais informações sobre uma estrutura típica de pastas de uma aplicação em React.
