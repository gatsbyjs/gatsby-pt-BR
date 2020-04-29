---
title: Recipes
tableOfContentsDepth: 2
---

<!-- Modelo básico para uma receita de Gatsby:

## Tarefa a realizar.
1-2 frases a respeito. Quanto mais conciso e focado, melhor!

### Pré-requisitos
- Requisitos de sistema / versão.
- Tudo o necessário para configurar a tarefa.
- Incluindo a configuração de contas em outros sites, como o Netlify.
- Consulte [docs templates](/docs/docs-templates/) para obter dicas de formatação

### Instruções
Instruções passo a passo. Cada passo deve ser repetível e direto ao ponto. Qualquer coisa que não seja crítica para a tarefa deve ser omitida.

#### Exemplo ao vivo (opcional)
Um exemplo ao vivo pode não ser possível, dependendo da natureza da receita; nesse caso, pode omitir.

### Recursos adicionais
- Tutoriais
- Páginas do Documentos
- README de plugins
- etc.

Consulte [docs templates](/docs/docs-templates/) nos documentos de contribuição para obter mais ajuda..
-->

Desejando um meio termo entre ler os [tutoriais completos](/tutorial/) e rastrear os [docs](/docs/)? Aqui está um livro de receitas orientadoras sobre como construir coisas, no estilo Gatsby.

## [1. Páginas e layouts](/docs/recipes/pages-layouts)

Adicione páginas ao seu site do Gatsby e use layouts para gerenciar elementos comuns da página.

- [Estrutura do projeto](/docs/recipes/pages-layouts#project-structure)
- [Criando páginas automaticamente](/docs/recipes/pages-layouts#creating-pages-automatically)
- [Vinculação entre páginas](/docs/recipes/pages-layouts#linking-between-pages)
- [Criando um componente de layout](/docs/recipes/pages-layouts#creating-a-layout-component)
- [Criando páginas programaticamente com o createPage](/docs/recipes/pages-layouts#creating-pages-programmatically-with-createpage)

=======
>>>>>>> master
## [2. Estilizar com CSS](/docs/recipes/styling-css)

Existem muitas maneiras de adicionar estilos ao seu site; O Gatsby suporta quase todas as opções possíveis, através de plugins oficiais e da comunidade.

- [Usando arquivos CSS globais sem um componente de layout](/docs/recipes/styling-css#using-global-css-files-without-a-layout-component)
- [Usando estilos globais em um componente de layout](/docs/recipes/styling-css#using-global-styles-in-a-layout-component)
- [Usando Styled Components](/docs/recipes/styling-css#using-styled-components)
- [Usando módulos CSS](/docs/recipes/styling-css#using-css-modules)
- [Usando Sass/SCSS](/docs/recipes/styling-css#using-sassscss)
- [Adicionando uma Fonte Local](/docs/recipes/styling-css#adding-a-local-font)
- [Usando Emotion](/docs/recipes/styling-css#using-emotion)
- [Usando Google Fonts](/docs/recipes/styling-css#using-google-fonts)

## [3. Trabalhando com starters](/docs/recipes/working-with-starters)

[Starter](/docs/starters/) são sites padronizados do Gatsby mantidos oficialmente ou pela comunidade.

- [Usando um starter](/docs/recipes/working-with-starters#using-a-starter)

## [4. Trabalhando com temas](/docs/recipes/working-with-themes)

Um tema Gatsby permite centralizar a aparência do seu site. Você pode atualizar perfeitamente um tema, compor temas juntos e até trocar um tema compatível por outro.

- [Criando um novo site usando um tema](/docs/recipes/working-with-themes#creating-a-new-site-using-a-theme)
- [Criando um novo site usando o tema starter](/docs/recipes/working-with-themes#creating-a-new-site-using-a-theme-starter)
- [Construindo um novo tema](/docs/recipes/working-with-themes#building-a-new-theme)

<<<<<<< HEAD
  // consulta para todas as remarcações
=======
## [5. Fornecendo dados](/docs/recipes/sourcing-data)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Puxe dados de vários locais, como um sistema de arquivos ou mesmo banco de dados, para o site do Gatsby.

- [Adicionando dados ao GraphQL](/docs/recipes/sourcing-data#adding-data-to-graphql)
- [Fornecendo Dados de Markdown para postagens e páginas de blog com GraphQL](/docs/recipes/sourcing-data#sourcing-markdown-data-for-blog-posts-and-pages-with-graphql)
- [Fornecendo Dados do WordPress](/docs/recipes/sourcing-data#sourcing-from-wordpress)
- [Fornecendo Dados do Contentful](/docs/recipes/sourcing-data#sourcing-data-from-contentful)
- [Puxando dados de uma fonte externa e criando páginas sem GraphQL](/docs/recipes/sourcing-data#pulling-data-from-an-external-source-and-creating-pages-without-graphql)
- [Fornecendo conteúdo do Drupal](/docs/recipes/sourcing-data#sourcing-content-from-drupal)

## [6. Consulta de dados](/docs/recipes/querying-data)

O Gatsby permite acessar seus dados em todas as fontes usando uma única interface GraphQL.

- [Consultando dados com uma consulta de página](/docs/recipes/querying-data#querying-data-with-a-page-query)
- [Consultando dados com o componente StaticQuery](/docs/recipes/querying-data#querying-data-with-the-staticquery-component)
- [Consultando dados com o hook do useStaticQuery](/docs/recipes/querying-data/#querying-data-with-the-usestaticquery-hook)
- [Limitando com GraphQL](/docs/recipes/querying-data#limiting-with-graphql)
- [Ordenando com GraphQL](/docs/recipes/querying-data#sorting-with-graphql)
- [Filtrando com GraphQL](/docs/recipes/querying-data#filtering-with-graphql)
- [GraphQL Query Aliases](/docs/recipes/querying-data#graphql-query-aliases)
- [GraphQL Query Fragments](/docs/recipes/querying-data#graphql-query-fragments)
- [Querying data client-side with fetch](/docs/recipes/querying-data#querying-data-client-side-with-fetch)

## [7. Trabalhando com imagens](/docs/recipes/working-with-images)

Acesse imagens como recursos estáticos ou automatize o processo de otimização através de plugins poderosos.

- [Importar uma imagem para um componente com o webpack](/docs/recipes/working-with-images#import-an-image-into-a-component-with-webpack)
- [Referenciar uma imagem da pasta estática](/docs/recipes/working-with-images#reference-an-image-from-the-static-folder)
- [Otimizando e consultando imagens locais com gatsby-image](/docs/recipes/working-with-images#optimizing-and-querying-local-images-with-gatsby-image)
- [Otimizando e consultando imagens em post frontmatter com gatsby-image](/docs/recipes/working-with-images#optimizing-and-querying-images-in-post-frontmatter-with-gatsby-image)

## [8. Transformando dados](/docs/recipes/transforming-data)

A transformação de dados no Gatsby é orientada por plug-ins. Os plug-ins de transformador obtêm dados buscados usando plug-ins de origem e os transformam em algo mais utilizável (por exemplo, JSON em objetos JavaScript e muito mais).

- [Transformando Markdown em HTML](/docs/recipes/transforming-data#transforming-markdown-into-html)
- [Transformando imagens em grayscale usando GraphQL](/docs/recipes/transforming-data#transforming-images-into-grayscale-using-graphql)

<<<<<<< HEAD
- A Gatsby site with `gatsby-config.js` and an `index.js` page
- Um site do Gatsby com a página `gatsby-config.js` e uma página` index.js`
- Um arquivo Markdown salvo no diretório `src` do site Gatsby
- Um plugin de origem instalado, como `gatsby-source-filesystem`
- O plugin `gatsby-transformer-comment` instalado

#### Instruções

1. Adicione o plug-in do transformador no seu `gatsby-config.js`:

```js:title=gatsby-config.js
plugins: [
  // não mostrado: gatsby-source-filesystem para criar _nodes_ para transformar
  `gatsby-transformer-remark`
],
```

2. Adicione a pesquisa GraphQL no arquivo `index.js` do seu site Gatsby para trazer os nó do `MarkdownRemark`:

```jsx:title=src/pages/index.js
export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

3. Reinicie o servidor de desenvolvimento e abra o GraphiQL em `http://localhost:8000/___graphql`. Explore os campos disponíveis no nó `MarkdownRemark`.

#### Recursos adicionais

- [Tutorial sobre como transformar Markdown em HTML](/tutorial/part-six/#transformer-plugins) usando `gatsby-transformer-remark`
- Procure plugins de transformadores disponíveis na [Gatsby plugin library](/plugins/?=transformer)

## 9. Implantando seu site
=======
## [9. Implantando seu site](/docs/recipes/deploying-your-site)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Hora do Show. Quando estiver satisfeito com o seu site, você estará pronto para publicá-lo!

- [Preparando para Implantação](/docs/recipes/deploying-your-site#preparing-for-deployment)
- [Implantando no Netlify](/docs/recipes/deploying-your-site#deploying-to-netlify)
- [Implantando no ZEIT Now](/docs/recipes/deploying-your-site#deploying-to-zeit-now)
