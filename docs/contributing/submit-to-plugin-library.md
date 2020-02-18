---
title: Enviar para a biblioteca de plugins
---

## Publicando um plugin na biblioteca

Para adicionar o seu plugin à [biblioteca de plugins](/plugins), você precisa:

<<<<<<< HEAD
1.  publicar um pacote no npm (aprenda como [aqui](https://docs.npmjs.com/getting-started/publishing-npm-packages)),
2.  incluir os [arquivos requeridos](/docs/files-gatsby-looks-for-in-a-plugin/) no seu plugin,
3.  **incluir o campo `keywords` (palavras-chave)** no `package.json` do seu plugin, contendo `gatsby` e `gatsby-plugin`,
4.  e documentar o seu plugin com um arquivo README, existem [modelos de plugin](/contributing/docs-templates/#plugin-readme-template) disponíveis que podem ser usados como referência.
=======
1.  Publish a package to npm (learn how on the [npm docs](https://docs.npmjs.com/getting-started/publishing-npm-packages)).
2.  Include the [required files](/docs/files-gatsby-looks-for-in-a-plugin/) in your plugin code.
3.  **Include a `keywords` field** in your plugin's `package.json`, containing `gatsby` and `gatsby-plugin`. If your plugin is a theme, please also include `gatsby-theme`.
4.  Document your plugin with a README, there is a [plugin template](/contributing/docs-templates/#plugin-readme-template) available to be used as reference.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Depois de fazer isso, o sistema de busca Algolia levará cerca de 12 horas para incluir seu plugin na busca da biblioteca de plugins (o tempo exato ainda não é conhecido), e é preciso aguardar o rebuild diário do https://gatsbyjs.org para incluir automaticamente o seu plugin na página do site. Então, tudo que você precisa fazer é compartilhar o seu maravilhoso plugin com a comunidade!

## Notas

### Palavras-chave

Você pode incluir outras palavras-chave _relevantes_ no seu arquivo `package.json` para ajudar os usuários a encontrarem o seu plugin. Por exemplo, um plugin que transforma marcações em MathJax para Markdown incluiria:

```json:title=package.json
"keywords": [
  "gatsby",
  "gatsby-plugin",
  "gatsby-transformer-plugin",
  "mathjax",
  "markdown",
]
```

### Imagens

Se você utiliza imagens no arquivo README do seu plugin, certifique-se que você está referenciando as imagens usando uma URL absoluta para que sejam exibidas na página do plugin.
