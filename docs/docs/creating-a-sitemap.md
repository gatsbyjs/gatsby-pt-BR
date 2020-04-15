---
title: Criando um Sitemap
---

## O que é um sitemap?

Um [XML sitemap](https://support.google.com/webmasters/answer/156184?hl=en) lista as páginas importantes de um site, assegurando que ferramentas de busca (como o Google) possam encontrar e rastrear todas elas. De maneira geral, um sitemap ajuda ferramentas de busca a entender a estrutura do seu site.

Pense como se fosse um mapa do seu site. Ele mostra todas as páginas que estão no seu site.

## Usando o [gatsby-plugin-sitemap](/packages/gatsby-plugin-sitemap/)

Para gerar um XML sitemap, você utilizará o pacote [`gatsby-plugin-sitemap`](/packages/gatsby-plugin-sitemap/).

Instale o pacote executando o seguinte comando:
`npm install --save gatsby-plugin-sitemap`

### Como configurar

Depois que a instalação estiver concluída, podemos adicionar este plugin ao nosso `gatsby-config.js`, da seguinte forma:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    siteUrl: `https://www.example.com`,
  },
  plugins: [`gatsby-plugin-sitemap`],
}
```

**Nota:**  A propriedade `siteUrl` deve ser definida e não deixada em branco.

Em seguida, execute um build (`npm run build`), pois a geração do sitemap ocorrerá apenas para builds de produção. Isso é tudo o que é necessário para obter um sitemap funcional com o Gatsby! Por padrão, o caminho do sitemap gerado é `/sitemap.xml` e inclui todas as páginas do seu site, mas é claro que o plugin expõe opções para configurar essa funcionalidade padrão.

### Modificações Adicionais

Passos para modificações adicionais estão disponiveis na [documentação do `gatsby-plugin-sitemap`](/packages/gatsby-plugin-sitemap)

## Mais informações

- Confira também esta postagem sobre [gatsby-plugin-advanced-sitemap](/blog/2019-05-07-advanced-sitemap-plugin-for-seo/) no blog do Gatsby
