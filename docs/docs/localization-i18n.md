---
title: Localização e internacionalização com Gatsby (i18n)
---

Fornecer conteúdo aos usuários de uma maneira adaptada ao idioma e à cultura deles constrói uma ótima experiência do usuário. Quando você faz um esforço para adaptar o conteúdo da Web à localização de um usuário, essa prática é chamada internacionalização (i18n).

Na prática, o i18n envolve a tradução de texto e formatação de datas, números e sequências de caracteres com base no local do usuário. Por exemplo, uma data exibida para um usuário nos Estados Unidos seguiria o formato de data em mm/dd/aa, mas para um usuário no Reino Unido, o formato da data mudaria para dd/mm/aa.

Este guia é uma breve descrição das opções existentes para aprimorar a internacionalização do seu projeto Gatsby.

## Escolhendo um pacote

Existem alguns pacotes React i18n disponíveis. Várias opções incluem [react-intl](https://github.com/yahoo/react-intl), a comunidade [plugin do Gatsby](https://www.npmjs.com/package/gatsby-plugin-i18n) e [react-i18next](https://github.com/i18next/react-i18next/). Existem vários fatores a serem considerados ao escolher um pacote: Você já usa um pacote semelhante em outro projeto? Quão bem o pacote atende às necessidades de seus usuários? Você ou sua equipe já estão familiarizados com um determinado pacote? O pacote está bem documentado e mantido?


### gatsby-plugin-i18n

Este plugin ajuda você a usar `react-intl`, `i18next` ou qualquer outra biblioteca i18n com o Gatsby. Este plugin não traduz nem formata seu conteúdo, mas cria rotas para cada idioma, permitindo que o Google encontre mais facilmente a versão correta do seu site e, se necessário, designa interfaces de usuário alternativas.

O formato de nomeação segue .**languageKey**.js para arquivos e /**languageKey**/caminho/nomeDoArquivo para URLs.

**Exemplo:**

Arquivo - src/pages/about.**en**.js

URL - /**en**/about

[gatsby-plugin-i18n no GitHub](https://github.com/angeloocana/gatsby-plugin-i18n)

### react-intl

O React-intl faz parte do conjunto FormatJS de bibliotecas i18n e fornece suporte para mais de 150 idiomas. Ele se baseia na [API de internacionalização](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl) do JavaScript, que fornece APIs e componentes aprimorados. O React-intl usa o contexto React e os HOCs (Higher Order Components) para fornecer traduções, permitindo que você carregue dinamicamente os módulos de idioma conforme necessário. Também há opções de polyfill disponíveis para navegadores mais antigos que não suportam a API JavaScript i18n básica.

Informações mais detalhadas sobre as [APIs](https://github.com/formatjs/react-intl/blob/master/docs/API.md) de react-intl e [componentes](https://github.com/formatjs/react-intl/blob/master/docs/Components.md), incluindo [demos](https://github.com/formatjs/react-intl/tree/master/examples), estão disponíveis na [documentação](https://github.com/formatjs/react-intl/tree/master/docs).

### react-i18next

O React-i18next é uma biblioteca de internacionalização criada na estrutura do i18next. Ele usa componentes para garantir que as traduções sejam renderizadas corretamente ou para renderizar novamente seu conteúdo quando o idioma do usuário for alterado.

O React-i18next é mais extensível que outras opções com uma variedade de plugins, utilitários e configurações. Os plugins comuns permitem detectar o idioma de um usuário ou adicionar uma camada adicional de cache local. Outras opções incluem cache, um plugin de backend para carregar traduções do seu servidor ou empacotar traduções com o Webpack.

Este framework também possui suporte experimental para a API do React suspense e React hooks.

## Outros recursos

- [Construindo i18n com Gatsby](https://www.gatsbyjs.org/blog/2017-10-17-building-i18n-with-gatsby/)

- [Construindo Eviction Free NYC com GatsbyJS e Contentful](https://www.gatsbyjs.org/blog/2018-04-27-building-eviction-free-nyc-with-gatsbyjs-and-contentful/)

- [Pacotes do Gatsby i18n](https://www.gatsbyjs.org/packages/gatsby-plugin-i18n/?=i18)

- [Artigos Gatsby i18n](https://www.gatsbyjs.org/blog/tags/i-18-n/)
- [Recursos i18n do W3C](http://w3c.github.io/i18n-drafts/getting-started/contentdev.en#reference)
