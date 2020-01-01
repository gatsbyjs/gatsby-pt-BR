---
title: Iniciando com MDX
---

A maneira mais facil de iniciar com Gatsby + MDX é usando o [MDX
starter](https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic). Ele permite escrever arquivos .mdx na pasta `src/pages` para criar novas paginas no seu site.

## 🚀 Iniciando rapidamente

1. **Inicie o MDX starter** com o CLI do Gatsby

   ```shell
   gatsby new my-mdx-starter https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic
   ```

1. **Iniciando o servidor dev** troque de pasta para a do projeto e instale as dependências

   ```shell
   cd my-mdx-starter/
   gatsby develop
   ```

1. **Abra o site** que esta rodando no http://localhost:8000

1. **Atualizando o conteúdo do arquivo MDX** abra a pasta `my-mdx-starter` 
   no seu editor de codigo e edit o arquivo `src/pages/index.mdx`.
   Save as alterações e o navegador ira atualizar automaticamente!

## Adicionamento arquivos MDX a um site Gatsby que já existe

Se você já tem um site em Gatsby e quer adicionar arquivos MDX, você pode seguir os passos de configuração do plugin [gatsby-plugin-mdx](/packages/gatsby-plugin-mdx/):

1. **Adicione o `gatsby-plugin-mdx`** e as dependencias do MDX

   ```shell
   npm install gatsby-plugin-mdx @mdx-js/mdx @mdx-js/react
   ```

   > **Nota:** Se você esta fazendo o upgrade apartir da versão 0, verifique o link para mais detalhes: [confifra o guia de migração do MDX v0 para v1](https://mdxjs.com/migrating/v1).

1. **Atualize seu arquivo `gatsby-config.js`** para usar o `gatsby-plugin-mdx`

   ```javascript:title=gatsby-config.js
   module.exports = {
     plugins: [
       // ....
       `gatsby-plugin-mdx`,
     ],
   }
   ```

1. **Reinicie com o comando `gatsby develop`** e adicione um aruivo `.mdx` na pasta `src/pages`

> **Nota:** Se você quer fazer uma query para frontmatter, exports, ou outro tipo de campo como
> `tableOfContents` e você ainda não adicionou ao `gatsby-source-filesystem`
> apontado para a pasta `src/pages` no seu projeto, você deve adicionar agora.

## O que vem a seguir?

Confira o artigo [como escrever arquivos MDX](/docs/mdx/writing-pages) para saber oque você pode fazer com Gatsby e MDX.
