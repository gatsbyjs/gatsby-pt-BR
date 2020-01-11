---
title: Preparando um site para ir ao ar
typora-copy-images-to: ./
disableTableOfContents: true
---

Uau! você chegou bem longe! Você aprendeu até o momento:

- criar novos sites com Gatsby
- criar páginas e componentes
- estilizar componentes
- adicionar plugins ao site
- código & tratamento de dados
- usar GraphQL para consultar dados para a página
- criar páginas automaticamente a partir dos seus dados

Nesta seção final, você passará por alguns dos passos comuns ao preparar um site para ir ao ar, introduzindo uma poderosa ferramenta chamada [Lighthouse](https:/developers.google.com/web/tools/lighthouse/). Ao longo do caminho nós iremos introduzir alguns plugins a mais que você gostará de usar nos seus sites com Gatsby.

## Auditando com o Lighthouse

Citando o [site do Lighthouse](https://developers.google.com/web/tools/lighthouse/):

> Lighthouse é uma ferramenta de código aberto, automatizada para melhorar a qualidade de páginas na web. Você pode executar em qualquer página, seja ela pública ou que precise de autenticação. É possível realizar auditorias de performance, acessibilidade, progressive web apps (PWAs) entre outras.

Lighthouse está incluso no Chrome DevTools. Executar sua auditoria - e então consertar os erros apontados e implementar as melhorias sugeridas - é uma ótima forma de preparar o seu site para ir ao ar. Isso te ajuda a ganhar confiança que o seu site é rápido e acessível o máximo possível.

Tente você mesmo!

Primeiro, você precisa criar um build de produção do seu site Gatsby. O servidor de desenvolvimento do Gatsby é otimizado para tornar o desenvolvimento rápido. Porém, o site que é gerado, apesar de semelhante à uma versão de produção do site, não é tão otimizado quanto.

### ✋ Criando o build de produção

1. Pare o servidor de desenvolvimento (se você ainda estiver executando) e execute o seguinte comando:

```shell
gatsby build
```

> 💡 Como você aprendeu na [parte 1](/tutorial/part-one/), esse comando gera um
build de produção do seu site, gerando arquivos estáticos na pasta `public`

2.  Para ver a versão de produção do seu site localmente, execute:

```shell
gatsby serve
```

Uma vez iniciado, você pode ver o seu site em [`localhost:9000`](http://localhost:9000).

### Executando uma auditoria do Lighthouse

Agora você vai executar o seu primeiro teste com o Lighthouse

1. Se você ainda não fez isso, abra o seu site numa aba anônima do Google Chrome
para que nenhuma extensão interfira no teste. Depois, abra o Chrome DevTools.

2. Clique na aba "Audits" onde você verá uma tela parecida com isso:

![Começo da auditoria do Lighthouse](./lighthouse-audit.png)

3. Clique em "Perform an audit..." (Todos os tipos de auditoria estarão habilitados por padrão). Então clique em "Run audit". (isso deve demorar alguns minutos). Uma vez que a auditoria esteja completa, você verá os resultados dessa maneira:

![Resultados da auditoria do Lighthouse](./lighthouse-audit-results.png)

Como você pode ver, a performance do Gatsby é excelente por padrão, mas estão faltando algumas coisas para PWA, acessibilidade, melhores práticas e SEO que te ajudarão a  melhorar a sua pontuação (e tornar o seu site muito mais amigável para visitantes e mecanismos de busca durante o processo).

## Adicionando o arquivo de manifesto

Parece que você tem uma pontução baixa para a categoria "Progressive Web App". Vamos arrumar isso!

Mas primeiro, o que exatamente _são_ PWAs?

Eles são sites normais que aproveitam a vantagem de funcionalidades de browsers modernos para oferecer uma experiência próxima de um app mobile com funcionalidades e benefícios similares. Dê uma olhada na [definição do Google](https://developers.google.com/web/progressive-web-apps/) sobre o que define a experiência com PWAs

A inclusão de um _web app manifest_ é um dos três [requisitos básicos para um PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1) mais amplamente aceitos.

Citando o [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> O _web app manifest_ é um simples arquivo JSON que indica ao browser sobre sua aplicação web e como ela deveria se comportar ao ser "instalada" no seu dispositivo mobile ou desktop.

[Plugin de manifesto Gatsby](/packages/gatsby-plugin-manifest/)
configura o Gatsby para criar um arquivo `manifest.webmanifest` a cada build do seu site

### ✋ Usando o `gatsby-plugin-manifest`

1. Instale o plugin:

```shell
npm install --save gatsby-plugin-manifest
```

2. Adicione o favicon para o seu app no formato `src/images/icon.png`. Para o propósito desse tutorial você pode usar [esse ícone de exemplo](https://raw.githubusercontent.com/gatsbyjs/gatsby/master/docs/tutorial/part-eight/icon.png) caso não tenha nenhum disponível. O ícone é necessario para construir todas as imagens para o manifesto. Para mais informações, dê uma olhada na documentação necessária do [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Adicione o plugin dentro do _array_ de `plugins` em seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Habilita o comando "Adicionar para a tela inicial" e desabilita toda a interface do browser (incluindo o botão de voltar)
        // Veja em: https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // Esse caminho é relativo à raiz do site.
      },
    },
  ]
}
```

Isso é tudo o que você precisa para começar a adicionar um manifesto web para um site Gatsby. O exemplo mostrado reflete a configuração básica -- Veja a [documentação do plugin](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) para mais opções.

## Adicionando suporte offline

Um outro requisito para um site ser classificado como PWA é o uso de um [service worker](https://developer.mozilla.org/pt-BR/docs/Web/API/Service_Worker_API). Um service worker é executado em segundo plano e é capaz de decidir qual conteúdo carregar através da rede ou cache baseado na conectividade do usuário, permitindo uma incrível experiência offline.

[O Gatsby's offline plugin](/packages/gatsby-plugin-offline/) faz com que um site Gatsby funcione offline e seja mais resistente a conexões ruins de rede ao criar um service worker para o seu site.

### ✋ Usando o `gatsby-plugin-offline`

1. Instale o plugin:

```shell
npm install --save gatsby-plugin-offline
```

2. Adicione o plugin dentro do _array_ de `plugins` em seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Habilita o comando "Adicionar para a tela inicial" e desabilita toda a interface do browser (incluindo o botão de voltar)
        // Veja em: https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // Esse caminho é relativo à raiz do site.
      },
    },
    // highlight-next-line
    `gatsby-plugin-offline`,
  ]
}
```

Isso é tudo o que você precisa para começar a utilizar service workers com Gatsby.

> 💡 O plugin offline deve ser listado _depois_ do plugin do manifesto. Dessa forma o plugin offline pode fazer um cache do arquivo `manifest.webmanifest`.

## Adicione metadados da página

Adicionar metadados nas páginas (como título e descrição) é o ponto chave para ajudar mecanismos de busca como o Google a entender seu conteúdo e decidir quando exibir nos resultados das buscas

[React Helmet](https://github.com/nfl/react-helmet) é um pacote que possui um componente React que permite manipular o [elemento head](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/head).

O [plugin react helmet](/packages/gatsby-plugin-react-helmet/) do Gatsby possui suporte para a renderização _server-side_ de dados. Usando o plugin, atributos adicionados ao React Helmet serão adicionados aos arquivos estáticos HTML gerados no build do Gatsby.'

### ✋ Usando `React Helmet` e `gatsby-plugin-react-helmet`

1. Instale os dois pacotes:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2. Tenha certeza que você possua os atributos `description` e `author` configurados dentro do seu objeto `siteMetadata`. Adicione também o plugin `gatsby-plugin-react-helmet` ao array `plugins` no seu arquivo `gatsby-config.js`

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
    // highlight-start
    description: `A simple description about pandas eating lots...`,
    author: `gatsbyjs`,
    // highlight-end
  },
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Habilita o comando "Adicionar para a tela inicial" e desabilita toda a interface do browser (incluindo o botão de voltar)
        // Veja em: https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
    // highlight-next-line
    `gatsby-plugin-react-helmet`,
  ],
}
```

3. Na pasta `src/components`, crie um arquivo chamado `seo.js` e adicione a seguinte parte:

```jsx:title=src/components/seo.js
import React from "react"
import PropTypes from "prop-types"
import Helmet from "react-helmet"
import { useStaticQuery, graphql } from "gatsby"

function SEO({ description, lang, meta, title }) {
  const { site } = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
            description
            author
          }
        }
      }
    `
  )

  const metaDescription = description || site.siteMetadata.description

  return (
    <Helmet
      htmlAttributes={{
        lang,
      }}
      title={title}
      titleTemplate={`%s | ${site.siteMetadata.title}`}
      meta={[
        {
          name: `description`,
          content: metaDescription,
        },
        {
          property: `og:title`,
          content: title,
        },
        {
          property: `og:description`,
          content: metaDescription,
        },
        {
          property: `og:type`,
          content: `website`,
        },
        {
          name: `twitter:card`,
          content: `summary`,
        },
        {
          name: `twitter:creator`,
          content: site.siteMetadata.author,
        },
        {
          name: `twitter:title`,
          content: title,
        },
        {
          name: `twitter:description`,
          content: metaDescription,
        },
      ].concat(meta)}
    />
  )
}

SEO.defaultProps = {
  lang: `en`,
  meta: [],
  description: ``,
}

SEO.propTypes = {
  description: PropTypes.string,
  lang: PropTypes.string,
  meta: PropTypes.arrayOf(PropTypes.object),
  title: PropTypes.string.isRequired,
}

export default SEO
```

O código acima configura valores padrão para as tags de metadados mais comuns e cria um componente `<SEO>` para se integrar ao resto do seu projeto. Bem legal, né?

4. Agora, você pode usar o componente `<SEO>` nos seus templates de página e passar algumas props para ele. Por exemplo, adicione ele ao seu `blog-post.js` dessa forma:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
// highlight-next-line
import SEO from "../components/seo"

export default ({ data }) => {
  const post = data.markdownRemark
  return (
    <Layout>
      // highlight-start
      <SEO title={post.frontmatter.title} description={post.excerpt} />
      // highlight-end
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
      // highlight-next-line
      excerpt
    }
  }
`
```

O exemplo acima é baseado no [blog de exemplo do Gatsby](/starters/gatsbyjs/gatsby-starter-blog/). Passando props para o componente `<SEO>`, você pode dinamicamente mudar os metadados para o seu post. Nesse caso, o `title` e `excerpt` do seu blog (se existir no arquivo markdown do post) serão utilizados ao invés dos padrões configurados no  `siteMetadata` do seu arquivo `gatsby-config.js`.

Agora, se você executar novamente a auditoria do Lighthouse, você deve atingir uma nota próxima --se não perfeita-- de 100 pontos!

> 💡 Para uma leitura futura e exemplos, leia [Adicionando um componente SEO](/docs/add-seo-component/) e a [documentação do React Helmet](https://github.com/nfl/react-helmet#example)!

## Deixando ainda melhor

Nessa seção, nós mostramos para você algumas ferramentas específicas do Gatsby para melhorar a performance do seu site e prepará-lo para ir ao ar.

Lighthouse é uma ferramenta incrível para a performance de sites e aprendizado -- fique de olho no feedback detalhado fornecido e continue deixando seu site melhor!

## Próximos passos

### Documentação oficial

- [Documentação oficial](https://www.gatsbyjs.org/docs/): Veja nossa documentação oficial para um _[Início rápido](https://www.gatsbyjs.org/docs/quick-start/)_, _[Guias detalhados](https://www.gatsbyjs.org/docs/preparing-your-environment/)_, _[referências da API](https://www.gatsbyjs.org/docs/gatsby-link/)_, e muito mais.

### Plugins oficiais

- [Plugins oficiais](https://github.com/gatsbyjs/gatsby/tree/master/packages): 
A lista completa de todos os plugins oficiais mantidos pelo Gatsby.

### Guias oficiais

1. [Guia padrão do Gatsby](https://github.com/gatsbyjs/gatsby-starter-default): Início rápido para seu projeto com esse modelo padrão. Esse modelo básico vem junto com os principais arquivos de configuração que você pode precisar  _[Exemplo funcional](http://gatsbyjs.github.io/gatsby-starter-default/)_
2. [Guia inicial de um blog Gatsby](https://github.com/gatsbyjs/gatsby-starter-blog): Guia do Gatsby para criar um  blog incrível e absurdamente rápido. _[Exemplo funcional](http://gatsbyjs.github.io/gatsby-starter-blog/)_
3. [Olá mundo inicial do Gatsby](https://github.com/gatsbyjs/gatsby-starter-hello-world): Guia do Gatsby com o mínimo necessário para criar um site Gatsby. _[Exemplo funcional](https://gatsby-starter-hello-world-demo.netlify.com/)_

## Isso é tudo, pessoal

Bem, não tudo; apenas para esse tutorial. Aqui tem alguns [Tutoriais Adicionais](/tutorial/additional-tutorials/) apresentando alguns outros casos de uso

Esse é só o começo. Continue indo!

- Você criou alguma coisa legal? Compartilhe no Twitter, com a hashtag [#buildwithgatsby](https://twitter.com/search?q=%23buildwithgatsby), e [@nos mencione](https://twitter.com/gatsbyjs)!
- Você escreveu um post legal sobre o que você aprendeu? Compartilhe conosco também!
- Contribua!
- Contribute! Dê uma olhada nas [issues abertas](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) No repoisitório do e [vire um contribuidor](/contributing/how-to-contribute/).

Veja a documentação sobre ["como contribuir"](/contributing/how-to-contribute/) para ainda mais ideias.

Nós estamos ansiosos pra ver o que você é capaz de fazer 😄.
