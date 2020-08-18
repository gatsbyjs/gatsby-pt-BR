---
title: Criando sub-plugins do Remark
---

[`gatsby-transformer-remark`](/packages/gatsby-transformer-remark) permite que desenvolvedores transformem arquivos Markdown em HTML que pode ser consumido através da API GraphQL do Gatsby. Blogs e outros sites baseados em exibição de conteúdo podem se beneficiar drasticamente das funcionalidades oferecidas por este plugin. Com ele, autores de conteúdo para o site não precisam se preocupar sobre como o site é escrito ou estruturado, concentrando-se ao invés disso em escrever conteúdo e posts engajadores!

Em certas instâncias, o desenvolvedor pode querer customizar o conteúdo de um arquivo Markdown e extender sua funcionalidade de algumas maneiras úteis; por exemplo, em casos como a adição de [realce da sintaxe em trechos de código](/packages/gatsby-remark-prismjs/), [interpretação e criação de imagens responsivas](/packages/gatsby-remark-images), [inserção de vídeos](/packages/gatsby-remark-embed-video), e muitos outros. Em cada um destes exemplos, um plugin será injetado através da Árvore de Sintaxe Abstrata do Markdown (na sigla em inglês, AST) e manipular conteúdo baseado em certos tipos de nó ou conteúdos de um nó em particular.

## O que você aprenderá nesse tutorial

- Conhecer de maneira aprofundada a Árvore de Sintaxe Abstrata do Markdown (AST)
- Como criar um plugin que é injetado com a AST através do `gatsby-transformer-remark`
- Como manipular o AST do remark a fim de adicionar funcionalidades

## Pré-requisitos

Há algumas coisas com a qual você deve ter certa familiaridade:

- Como trabalhar com o Remark no Gatsby, como descrito na [Parte Seis](/tutorial/part-six/) e [Parte Sete](/tutorial/part-seven/) do tutorial do Gatsby.
- Entendimento da Sintaxe do Markdown.

## Entendendo a Árvore de Sintaxe Abstrata:

Para entender o que está disponível na AST do Markdown, dê uma olhada nas especificações da AST do Markdown que é usada no remark e em outros projetos `unist`: [syntax-tree/mdast](https://github.com/syntax-tree/mdast).

Começando com um arquivo Markdown como abaixo:

```markdown
# Hello World!

This is a [Real page](https://google.com)
```

O Remark irá traduzir isso em uma AST que estará disponível para os plugins do `gatsby-transformer-remark`. A AST irá aparecer desta forma:

```json
{
  "type": "root",
  "children": [
    {
      "type": "heading",
      "depth": 1,
      "children": [
        {
          "type": "text",
          "value": "Hello World!",
          "position": {
            "start": { "line": 1, "column": 3, "offset": 2 },
            "end": { "line": 1, "column": 15, "offset": 14 },
            "indent": []
          }
        }
      ],
      "position": {
        "start": { "line": 1, "column": 1, "offset": 0 },
        "end": { "line": 1, "column": 15, "offset": 14 },
        "indent": []
      }
    },
    {
      "type": "paragraph",
      "children": [
        {
          "type": "text",
          "value": "This is a ",
          "position": {
            "start": { "line": 3, "column": 1, "offset": 16 },
            "end": { "line": 3, "column": 11, "offset": 26 },
            "indent": []
          }
        },
        {
          "type": "link",
          "title": null,
          "url": "https://google.com",
          "children": [
            {
              "type": "text",
              "value": "Real page",
              "position": {
                "start": { "line": 3, "column": 12, "offset": 27 },
                "end": { "line": 3, "column": 21, "offset": 36 },
                "indent": []
              }
            }
          ],
          "position": {
            "start": { "line": 3, "column": 11, "offset": 26 },
            "end": { "line": 3, "column": 42, "offset": 57 },
            "indent": []
          }
        }
      ],
      "position": {
        "start": { "line": 3, "column": 1, "offset": 16 },
        "end": { "line": 3, "column": 42, "offset": 57 },
        "indent": []
      }
    }
  ],
  "position": {
    "start": { "line": 1, "column": 1, "offset": 0 },
    "end": { "line": 4, "column": 1, "offset": 58 }
  }
}
```

Adicionalmente, o [AST Explorer](https://astexplorer.net/#/gist/d9029a2e8827265fbb9b190083b59d4d/3384f3ce6a3084e50043d0c8ce34628ed7477603) é um site que lhe fornece uma visão lado-a-lado do Markdown e sua saída correspondente no formato AST.

## Configurando um plugin

Você irá criar um plugin que fará com que todos os cabeçalhos de alto nível no Markdown tenham a cor roxa.

Primeiro, crie um plugin local adicionando um diretório `plugins` ao seu site e gerando um arquivo `package.json` para ele. Crie também um arquivo `index.js`. Nesse arquivo, exportaremos uma função que irá ser invocada pelo `gatsby-transformer-remark`:

```js:title=plugins/gatsby-remark-purple-headers/index.js
module.exports = ({ markdownAST }, pluginOptions) => {
  // Manipulação do AST

  return markdownAST
}
```

O primeiro parâmetro refere-se à todas as propriedades padrão que podem ser usadas em plugins (actions, store, getNodes, schema, etc.), e, adicionalmente, alguns usados apenas para plugins do `gatsby-transformer-remark`. O campo mais relevante para os nossos propósitos é o `markdownAST`, que foi desestruturado no trecho de código acima.

Similarmente à outros plugins do Gatsby, o segundo parâmetro é o `pluginOptions` que é obtido da definição no arquivo `gatsby-config.js`.

Finalmente, a função irá retornar o `markdownAST` após os campos que você deseja que sejam editados serem transformados.

## Adicionando o plugin ao seu site

Você provavelmente irá querer usar `gatsby-source-filesystem` para injetar os nós de arquivos no schema do GraphQL do Gatsby. Nesse exemplo, assumimos que os arquivos Markdown existam em um diretório `src/data/`.

O plugin agora está inicialmente configurado para que você possa adicioná-lo como um sub-plugin dentro do `gatsby-transformer-remark`.

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-source-filesystem",
      options: {
        name: `data`,
        path: `${__dirname}/src/data/`,
      },
    },
    {
      resolve: `gatsby-transformer-remark`,
      options: {
        plugins: [`gatsby-remark-purple-headers`],
      },
    },
  ],
}
```

Caso queira adicionar mais opções, você poderá mudar para a sintaxe de objeto:

```js
{
  resolve: `gatsby-remark-purple-headers`,
  options: {
    // Opções aqui
  }
}
```

## Encontrando e Modificando Nós do Markdown

Quando estiver modificando nós, você irá querer navegar pela árvore e então implementar novas funcionalidades em nós específicos.

Um node-module que pode lhe ajudar é o [unist-util-visit](https://github.com/syntax-tree/unist-util-visit), um navegador para nós `unist`. Para referência, Unist (Unified Syntax Tree) é um padrão adotado por árvores de sintaxe Markdown e interpretadores que inclui interpretadores já bem conhecidos no mundo do Gatsby como Remark e MDX.

Como exemplificado no arquivo README do `unist-util-visit`, isso permite que uma interface visite nós particulares baseados em uma tipagem particular:

```js
var remark = require("remark")
var visit = require("unist-util-visit")

var tree = remark().parse("Some _emphasis_, **importance**, and `code`.")

visit(tree, "text", visitor)

function visitor(node) {
  console.log(node)
}
```

Aqui, ele encontrará todos os nós de texto e irá logar todos com um `console.log`. O segundo argumento pode ser substituído com qualquer tipagem descrita na [especificação Markdown AST (mdast)](https://github.com/syntax-tree/mdast#nodes) do Unist, incluindo tipagens como `paragraph`, `blockquote`, `link`, `image` ou, em nosso caso, `heading`.

Com essa técnica em mente, nós podemos atravessar a AST similarmente com o seu plugin e adicionar uma funcionalidade adicional desta forma:

```js:title=plugins/gatsby-remark-purple-headers/index.js
const visit = require("unist-util-visit")

module.exports = ({ markdownAST }, pluginOptions) => {
  // destaque-próxima-linha
  visit(markdownAST, "heading", node => {
    // Faz alguma coisa com os nós do cabeçalho
  })

  return markdownAST
}
```

Em seguida, visitando todos os nós de cabeçalho e passando-os por uma função do transformer, você pode manipular nós particulares que estejam alinhados ao seu caso de uso.

Olhando novamente para o nó da AST para o cabeçalho:

```json
{
  "type": "heading",
  "depth": 1,
  "children": [
    {
      "type": "text",
      "value": "Hello World!",
      "position": {
        "start": { "line": 1, "column": 3, "offset": 2 },
        "end": { "line": 1, "column": 15, "offset": 14 },
        "indent": []
      }
    }
  ],
  "position": {
    "start": { "line": 1, "column": 1, "offset": 0 },
    "end": { "line": 1, "column": 15, "offset": 14 },
    "indent": []
  }
},
```

Você agora tem contexto sobre o texto, assim como a profundidade em que o cabeçalho encontra-se (por exemplo, aqui há uma profundidade de valor 1, o que corresponde à um elemento `h1`).

Com a função interna da chamada `visit`, você pode interpretar todo o texto, e se ele for mapeado para um elemento `h1`, configurar o tipo do nó para `html`, atribuindo seu valor à algum HTML customizado.

```js
const visit = require("unist-util-visit")
const toString = require("mdast-util-to-string")

module.exports = ({ markdownAST }, pluginOptions) => {
  visit(markdownAST, "heading", node => {
    let { depth } = node

    // Ignora caso não seja um h1
    if (depth !== 1) return

    // Pega o innerText do nó do cabeçalho
    let text = toString(node)

    const html = `
        <h1 style="color: rebeccapurple">
          ${text}
        </h1>
      `

    node.type = "html"
    node.children = undefined
    node.value = html
  })

  return markdownAST
}
```

A pequena biblioteca [mdast-util-to-string](https://github.com/syntax-tree/mdast-util-to-string) da Unified foi usada para extrair o texto sem formatação dos nós internos. Isso removeria links ou outros tipos de nós dentro do cabeçalho, mas visto que você possui acesso completo à AST do markdown, você pode modificá-lo da maneira que desejar.

## Carregando mudanças e vendo efeito

À essa altura, nosso plugin está pronto para ser utilizado. Para ver o resultado da funcionalidade, é recomendável revisitar a [Parte 7 do Tutorial do Gatsby](/tutorial/part-seven/) para criar páginas programaticamente através dos dados Markdown. Quando isso estiver configurado, você pode observar que seu plugin funciona como visto abaixo baseado no Markdown que foi escrito anteriormente.

![Output](./images/remark-ast-output.png)

## Publicando o plugin

Para compartilhar esse plugin com outros, você pode extraí-lo em seu próprio diretório fora do site e então publicá-lo no NPM para que ele possa ser acessado tanto do NPM, quanto [Submetido à Biblioteca de Plugins](/contributing/submit-to-plugin-library).

## Sumário

Você acabou de escrever um plugin local do Gatsby que opera como um sub-plugin para o `gatsby-transformer-remark` manipulando a AST do Remark. Agora você deve possuir um melhor entendimento da estrutura das Árvores de Sintaxe Abstrata do Markdown! Yay!

## Qual o próximo passo?

Se você gostaria de ver outros plugins que manipulam a AST do Remark, pesquise por `gatsby-remark-` na [biblioteca de plugins](/plugins).
