---
title: Trabalhando com imagens no Gatsby
---

Otimizar imagens é um desafio em qualquer site. Para utilizar as melhores práticas de desempenho em todos os dispositivos, você precisa de vários tamanhos e resoluções de cada imagem. Felizmente, o Gatsby possui vários [plugins](/docs/plugins/) úteis que trabalham juntos para te ajudar nessas tarefas, como pode ser visto em [page components](/docs/building-with-components/#page-components).

Recomenda-se usar [GraphQL queries](/docs/querying-with-graphql/) para obter imagens com o tamanho ou resolução ideais, e então, exibí-las com o componente [`gatsby-image`](/packages/gatsby-image/).

## Query de imagens com o GraphQL

Realizar a busca de imagens com GraphQL permite acesso aos dados da imagem além de permitir a realização de transformações com o [Sharp](https://github.com/lovell/sharp), uma biblioteca de processamento de imagem de alto desempenho.

Você precisará de alguns plugins para isso:

- O plugin [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) permite que você trate arquivos com o GraphQL. Veja como em [query files with GraphQL](/docs/querying-with-graphql/#images)
- [`gatsby-plugin-sharp`](/packages/gatsby-plugin-sharp) alimenta as conexões entre os plugins Sharp e Gatsby
- [`gatsby-transformer-sharp`](/packages/gatsby-transformer-sharp/) permite a criação várias imagens para que tenham tamanhos e resoluções corretos com uma única busca

Se a imagem final tiver um tamanho fixo, a otimização dependerá de várias resoluções da imagem. Se for responsivo, ou seja, se estende para preencher um contêiner ou página, a otimização depende de ter tamanhos diferentes da mesma imagem. Veja mais em [Gatsby Image documentation for more information](/packages/gatsby-image/#two-types-of-responsive-images).

Você também pode usar argumentos no tratamento para especificar dimensões exatas, mínimas e máximas. Veja como em [Gatsby Image documentation for complete options](/packages/gatsby-image/#two-types-of-responsive-images).

Este exemplo é para uma galeria de imagens onde as imagens se estendem quando a página é redimensionada. Ele usa o método `fluid` e o fragmento fluido para obter os dados corretos para usar no componente ` gatsby-image` e os argumentos para definir a largura máxima como 400px e a altura máxima como 250px.

```js
export const query = graphql`
  query {
    fileName: file(relativePath: { eq: "images/myimage.jpg" }) {
      childImageSharp {
        fluid(maxWidth: 400, maxHeight: 250) {
          ...GatsbyImageSharpFluid
        }
      }
    }
  }
`
```

## Otimizando imagens com o gatsby-image

[`gatsby-image`](/packages/gatsby-image/) é um plug-in que cria automaticamente componentes React para imagens otimizadas que:

> - Carrega o tamanho ideal da imagem para cada dispositivo e resolução de tela
> - Mantém a posição da imagem durante o carregamento para que sua página não se mova à medida que as imagens são carregadas
> - Usa o efeito "desfoque", ou seja, carrega uma versão minúscula da imagem para mostrar enquanto a imagem completa está sendo carregada
> - Como alternativa, fornece um SVG de "espaço reservado rastreado" da imagem
> - Reduz a largura de banda e acelera o tempo de carregamento inicial com carregamento lento de imagens 
> - Usa [WebP](https://developers.google.com/speed/webp/) se o navegador suportar o formato


Aqui está um componente de imagem que usa o tratamento do exemplo anterior:

```jsx
<Img fluid={data.fileName.childImageSharp.fluid} alt="" />
```

## Usando fragmentos para padronizar a formatação

E se você tiver um monte de imagens e quiser que todas tenham a mesma formatação?

Um fragmento personalizado é uma maneira fácil de padronizar a formatação e reutilizá-la em várias imagens:

```js
export const squareImage = graphql`
  fragment squareImage on File {
    childImageSharp {
      fluid(maxWidth: 200, maxHeight: 200) {
        ...GatsbyImageSharpFluid
      }
    }
  }
`
```

O fragmento pode ser referenciado no tratamento da imagem:

```js
export const query = graphql`
  query {
    image1: file(relativePath: { eq: "images/image1.jpg" }) {
      ...squareImage
    }

    image2: file(relativePath: { eq: "images/image2.jpg" }) {
      ...squareImage
    }

    image3: file(relativePath: { eq: "images/image3.jpg" }) {
      ...squareImage
    }
  }
`
```

### Recursos adicionais

- [Gatsby Image API docs](/docs/gatsby-image/)
- [Usando gatsby-image com Gatsby](https://egghead.io/playlists/using-gatsby-image-with-gatsby-ea85129e), playlist gratuita no egghead.io (em inglês) 
- [gatsby-image plugin README file](/packages/gatsby-image/)
- [gatsby-plugin-sharp README file](/packages/gatsby-plugin-sharp/)
- [gatsby-transformer-sharp README file](/packages/gatsby-transformer-sharp/)
