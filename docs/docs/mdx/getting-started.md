---
title: Iniciando com MDX
---

A maneira mais facil de iniciar com Gatsby + MDX é usando o [MDX
starter](https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic). Ele permite escrever arquivos .mdx na pasta `src/pages` para criar novas páginas no seu site.

## 🚀 Iniciando rapidamente

1. **Inicie o MDX starter** com o CLI do Gatsby

   ```shell
   gatsby new my-mdx-starter https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic
   ```

1. **Inicie o o servidor dev** trocando de pasta para a do projeto e instalando as dependências

   ```shell
   cd my-mdx-starter/
   gatsby develop
   ```

1. **Abra o site** que está rodando em `http://localhost:8000`

1. **Atualize o conteúdo do arquivo MDX** abrindo a pasta `my-mdx-starter` 
   no seu editor de código e edite o arquivo `src/pages/index.mdx`.
   Salve as alterações e o navegador irá atualizar automaticamente!

## Adicionando arquivos MDX a um site Gatsby já existente

Se você já tem um site em Gatsby e quer adicionar arquivos MDX, você pode seguir os passos de configuração do plugin [gatsby-plugin-mdx](/packages/gatsby-plugin-mdx/):

1. **Adicione o `gatsby-plugin-mdx`** e as dependências do MDX

   ```shell
   npm install gatsby-plugin-mdx @mdx-js/mdx @mdx-js/react
   ```

   > **Nota:** Se você está fazendo o upgrade a partir da versão 0, [confira o guia de migração do MDX v0 para v1](https://mdxjs.com/migrating/v1).

1. **Atualize seu arquivo `gatsby-config.js`** para usar o `gatsby-plugin-mdx`

   ```javascript:title=gatsby-config.js
   module.exports = {
     plugins: [
       // ....
       `gatsby-plugin-mdx`,
     ],
   }
   ```

1. **Reinicie com o comando `gatsby develop`** e adicione um arquivo `.mdx` na pasta `src/pages`

> **Nota:** Se você quer fazer uma query para `frontmatter`, `exports`, ou outro tipo de campo como
> `tableOfContents` e você ainda não adicionou um campo `gatsby-source-filesystem`
> apontando para a pasta `src/pages` no seu projeto, você deve adicionar agora.

## O que vem a seguir?

Confira o artigo [como escrever arquivos MDX](/docs/mdx/writing-pages) para saber o que você pode fazer com Gatsby e MDX.
