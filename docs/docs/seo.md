---
title: SEO com Gatsby
---

<<<<<<< HEAD
Gatsby ajuda seu site a ser melhor classificado nos motores de busca. Algumas vantagens vem prontas para uso e outras requerem algumas configurações.
=======
Gatsby can help your site rank and perform better in search engines. Using Gatsby makes your site fast and efficient for search engine crawlers, like Googlebot, to crawl your site and index your pages. Some advantages, like speed, come out of the box and others require configuration.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

## Renderização no servidor

<<<<<<< HEAD
Como as páginas Gatsby são renderizadas no servidor, todos os conteúdos das páginas estão disponíveis para o Google e outros motores de busca ou crawlers.

Você pode vizualizar o código-fonte desta página com o `curl`( no seu terminal): 
=======
Because Gatsby pages are server-side rendered, all the page content is available to Googlebot and other search engine crawlers.
You can see this by viewing the source for this page in your browser, Right-Click => View source. You'll see the fully rendered HTML document.

When you've installed [`gatsby-plugin-offline`](/packages/gatsby-plugin-offline/), you'll see a partial HTML document that does not contain the HTML you were hoping for. By using `gatsby-plugin-offline`, we can optimize bandwidth consumption and not let your users download too much data. Serving a partial HTML document is okay. Google and other search engines will still see the full HTML because `gatsby-plugin-offline` only starts working on the second-page load. A search engine always runs a page in Sandbox mode, which essentially is the first visit.

As a website owner, how do I test my site is serving its HTML correctly when `gatsby-plugin-offline` is being used? It would be best if you used your terminal of choice to visit your website. You can crawl your site by running the following command:

**on Windows (using powershell):**
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

```shell
Invoke-WebRequest https://www.gatsbyjs.org/docs/seo | Select -ExpandProperty Content
```
`Clique-botão-direito => Exibir código-fonte` isto não exibirá o html real (mesmo que elas ainda assim sejam renderizadas no servidor) já que este site está usando service workers. [Leia estas anotações](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-offline#notes) para aprender mais.

<<<<<<< HEAD
## Aumento de velocidade
=======
**on Mac OS/Linux:**

```shell
curl https://www.gatsbyjs.org/docs/seo
```
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Gatsby tem muitas otimizações de desempenho integradas, como renderização de arquivos estáticos, carregamento progressivo de imagem, e o [PRPL pattern](/docs/prpl-pattern/)—todos eles ajudam seu site a ser extremamente rápido por padrão.

Desde Janeiro de 2018, o Google têm [recompensado sites mais rápidos com um aumento no ranking de busca](https://searchengineland.com/google-speed-update-page-speed-will-become-ranking-factor-mobile-search-289904).

<<<<<<< HEAD
## Metadados da página
=======
In July 2018, [Google announced a new ranking factor for site speed](https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html), calling the algorithm update the "Speed Update". Google will possibly rank pages higher in the search results for faster loading times, however, the intent of the search query is still very relevant and a slower page can rank higher if the content is more relevant.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Adicionar metadados para as páginas, como título e descrição, ajuda os motores de busca a entenderem seu conteúdo e exibirem suas páginas nos resultados de buscas.

<<<<<<< HEAD
Uma forma comum para adicionar metadados as páginas é adicionar componentes [react-helmet](https://github.com/nfl/react-helmet) (juntamente com o [Gatsby React Helmet plugin](/packages/gatsby-plugin-react-helmet) para suporte SSR) para os componentes de sua página, aqui está um [guia de como adicionar um componente de SEO](https://www.gatsbyjs.org/docs/add-seo-component/) para sua aplicação Gatsby.
=======
Adding metadata to pages, such as page title, meta description, alt text and structured data using JSON-LD, helps search engines understand your content and when to show your pages in search results.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Alguns exemplos usando react-helmet:

- [Site Oficial GatsbyJS.org](https://github.com/gatsbyjs/gatsby/blob/87ad6e81b9bd78b25d089434600750f5903baaee/www/src/components/package-readme.js#L16-L25)
- [Oficial GatsbyJS default starter](https://github.com/gatsbyjs/gatsby/blob/776dc1d6fe8d5ce7b5ea6d884736bb3c76280975/starters/default/src/components/seo.js)
- [E-mail Gatsby](https://github.com/DSchau/gatsby-mail/blob/89b467e5654619ffe3073133ef0ae48b4d7502e3/src/components/meta.js)
- [Blog pessoal de Jason Lengstorf](https://github.com/jlengstorf/gatsby-theme-jason-blog/blob/e6d25ca927afdc75c759e611d4ba6ba086452bb8/src/components/SEO/SEO.js)

## Gerando rich snippets em motores de busca usando dados estruturados

<<<<<<< HEAD
Google utiliza dados estruturados encontrados na web para entender o conteúdo das páginas, bem como adquirir informações da web e do mundo em geral.
Por exemplo, aqui está um trecho de dados estruturados em [formato JSON-LD](https://developers.google.com/search/docs/guides/intro-structured-data) (Notação de Objetos JavaScript para vincular os dados) que podem aparecer na página de contato de uma companhia chamada Spooky Technologies, descrevendo suas informações de contatos:
=======
## Generate rich snippets in search engines using structured data

Google uses structured data that it finds on the web to understand the content of the page, as well as to gather information about the web and the world in general.

For example, here is a structured data snippet in the [JSON-LD format](https://developers.google.com/search/docs/guides/intro-structured-data) (JavaScript Object Notation for Linked Data) that might appear on the contact page of a company called Spooky Technologies, describing their contact information:
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

```html
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Organization",
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

<<<<<<< HEAD
Quando se utiliza dados estruturados, você vai precisar realizar testes durante o desenvolvimento e a [ferramenta de teste de dados estruturados](https://search.google.com/structured-data/testing-tool) do Google é um método recomendado. Depois da publicação, os [resultados dos relatórios de status](https://support.google.com/webmasters/answer/7552505?hl=en) podem ajudar a monitorar a integridade de sua página e mitigar quaisquer problemas de modelagem ou veiculação.
=======
When using structured data, you'll need to test during development and the [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool) from Google is one recommended method.

After deployment, their [Rich result status reports](https://support.google.com/webmasters/answer/7552505?hl=en) may help to monitor the health of your pages and mitigate any templating or serving issues.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

## Recursos adicionais

<<<<<<< HEAD
Você também pode estar interessado em [postagens no blog sobre SEO em Gatsby](/blog/tags/seo/)
=======
You might also be interested in [blog posts about SEO in Gatsby](/blog/tags/seo/).
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f
