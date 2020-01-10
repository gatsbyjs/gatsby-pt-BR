---
title: SEO com Gatsby
---

Gatsby ajuda seu site a ser melhor classificado nos motores de busca. Algumas vantagens vem prontas para uso e outras requerem algumas configurações.

## Renderização no servidor

Como as páginas Gatsby são renderizadas no servidor, todos os conteúdos das páginas estão disponíveis para o Google e outros motores de busca ou crawlers.

Você pode vizualizar o código-fonte desta página com o `curl`( no seu terminal): 

```shell
curl https://www.gatsbyjs.org/docs/seo
```
`Clique-botão-direito => Exibir código-fonte` isto não exibirá o html real (mesmo que elas ainda assim sejam renderizadas no servidor) já que este site está usando service workers. [Leia estas anotações](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-offline#notes) para aprender mais.

## Aumento de velocidade

Gatsby tem muitas otimizações de desempenho integradas, como renderização de arquivos estáticos, carregamento progressivo de imagem, e o [PRPL pattern](/docs/prpl-pattern/)—todos eles ajudam seu site a ser extremamente rápido por padrão.

Desde Janeiro de 2018, o Google têm [recompensado sites mais rápidos com um aumento no ranking de busca](https://searchengineland.com/google-speed-update-page-speed-will-become-ranking-factor-mobile-search-289904).

## Metadados da página

Adicionar metadados para as páginas, como título e descrição, ajuda os motores de busca a entender seu conteúdo e exibir suas páginas nos resultados de buscas.

Uma forma comum para adicionar metadados as páginas é adicionar componentes [react-helmet](https://github.com/nfl/react-helmet) (juntamente com o [Gatsby React Helmet plugin](/packages/gatsby-plugin-react-helmet) para suporte SSR) para os componentes de sua página, aqui está um [guia de como adicionar um componente de SEO](https://www.gatsbyjs.org/docs/add-seo-component/) para sua aplicação Gatsby.

Alguns exemplos usando react-helmet:

- [Site Oficial GatsbyJS.org](https://github.com/gatsbyjs/gatsby/blob/87ad6e81b9bd78b25d089434600750f5903baaee/www/src/components/package-readme.js#L16-L25)
- [Oficial GatsbyJS default starter](https://github.com/gatsbyjs/gatsby/blob/776dc1d6fe8d5ce7b5ea6d884736bb3c76280975/starters/default/src/components/seo.js)
- [E-mail Gatsby](https://github.com/DSchau/gatsby-mail/blob/89b467e5654619ffe3073133ef0ae48b4d7502e3/src/components/meta.js)
- [Blog pessoal de Jason Lengstorf](https://github.com/jlengstorf/gatsby-theme-jason-blog/blob/e6d25ca927afdc75c759e611d4ba6ba086452bb8/src/components/SEO/SEO.js)

## Gerando ricos fragmentos em motores de busca usando dados estruturados

Google utiliza dados estruturados encontrados na web para entender o conteúdo das páginas, bem como adquirir informações da web e do mundo em geral.
Por exemplo, aqui está um trecho de dados estruturados em [formato JSON-LD](https://developers.google.com/search/docs/guides/intro-structured-data) (Notação de Objetos JavaScript para vincular os dados) que podem aparecer na página de contato de uma companhia chamada Spooky Technologies, descrevendo suas informações de contatos:

```js
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Company",
  "url": "http://www.spookytech.com",
  "name": "Spooky technologies",
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+5-601-785-8543",
    "contactType": "Customer Support"
  }
}
</script>
```

Quando se utiliza dados estruturados, você vai precisar realizar testes durante o desenvolvimento e a [ferramenta de teste de dados estruturados](https://search.google.com/structured-data/testing-tool) do Google é um método recomendado. Depois da publicação, os [resultados dos relatórios de status](https://support.google.com/webmasters/answer/7552505?hl=en) podem ajudar a monitorar a integridade de sua página e mitigar quaisquer problemas de modelagem ou veiculação.

## Recursos adicionais

Você também pode estar interessado em [postagens no blog sobre SEO em Gatsby](/blog/tags/seo/)
