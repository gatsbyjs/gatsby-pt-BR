---
title: Usando o _Gatsby Image_ para impedir _Image Bloat_
---

`gatsby-image` é um componente do React projetado para funcionar perfeitamente com as consultas GraphQL do Gatsby ([`gatsby-image` plugin README](/packages/gatsby-image/)). Ele combina os recursos de [processamento nativo de imagens do Gatsby](https://image-processing.gatsbyjs.org/) com técnicas avançadas de carregamento de imagens para otimizar fácil e completamente o carregamento de imagens para seus sites. O `gatsby-image` usa o [gatsby-plugin-sharp](/packages/gatsby-plugin-sharp/) para tranformações de imagens.

> _Aviso: gatsby-image **não** é um substituto para `<img />`. É otimizado para imagens de largura/altura fixas e imagens que ampliam a largura total de um contêiner. Algumas maneiras de usar o <img /> `não funcionarão com o gatsby-image._

[Demonstração](https://using-gatsby-image.gatsbyjs.org/)

`gatsby-image` inclui os truques que você espera de um componente de imagem moderno. Como:

- usa a nova [IntersectionObserver API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) para carregar imagens usando a técnica _lazy load_
- mantém a posição de uma imagem para que sua página não pule à medida que as imagens são carregadas
- facilita a adição de um _placeholder_ - um plano de fundo cinza ou uma versão borrada da imagem.

_Para obter informações mais completas sobre a API, consulte a documentação do [Gatsby Image API](/docs/gatsby-image/)._

## Problema

Imagens grandes e não otimizadas diminuem drasticamente a velocidade do seu site.

Mas criar imagens otimizadas para sites há muito tempo é um problema difícil. Idealmente você deve:

- Redimensionar imagens grandes para o tamanho necessário ao seu design
- Gerar várias imagens menores para que smartphones e tablets não baixem imagens em tamanho de desktop
- Remover todos os metadados desnecessários e otimizar a compactação JPEG e PNG
- Carregar imagens em modo _lazy load_ (assícrona) para acelerar o carregamento inicial da página e economizar largura de banda
- Usar a técnica de "desfoque" ou um "'_placeholder_ rastreado" no SVG para mostrar uma pré-visualização da imagem enquanto ela carrega
- Manter a posição da imagem para que sua página não pule enquanto as imagens são carregadas

Fazer isso de forma consistente em um site parece um trabalho complicado. Você otimiza suas imagens manualmente e então... várias imagens são alteradas no último minuto ou um aprimoramento de design reduz 100px na largura das imagens.

A maioria das soluções envolve muito trabalho manual e contabilidade para garantir que todas as imagens sejam otimizadas.

Isso não é o ideal. Imagens otimizadas devem ser fáceis e padrão.

## Solução

Com o Gatsby, podemos melhorar a experiência de trabalhar com imagens.

`gatsby-image` foi projetado para funcionar perfeitamente com os recursos nativos de processamento de imagens do Gatsby, equipados com GraphQL e Sharp. Para produzir imagens perfeitas com o mínimo esforço, você pode:

1. Instalar `gatsby-image` e outras dependências necessárias como `gatsby-plugin-sharp` e `gatsby-transformer-sharp`

```shell
  npm install --save gatsby-image gatsby-transformer-sharp gatsby-plugin-sharp
```

2. Adicionar os plugins e os plugins transformadores recém-instalados ao seu `gatsby-config.js`

```js:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-sharp`, `gatsby-transformer-sharp`],
}
```

3. Configurar o `gatsby-source-filesystem` para carregar imagens de uma pasta. Para usar o GraphQL na consulta dos arquivos de imagem, os mesmos precisam estar em um local conhecido pelo Gatsby. Isso requer uma atualização no `gatsby-config.js` para configurar o plugin. Sinta-se livre para substituir a opção `path` para referenciar onde quer que suas imagens estejam localizadas no seu projeto.

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-transformer-sharp`,
    `gatsby-plugin-sharp`,
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/data/`,
      },
    },
    // highlight-end
  ],
}
```

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-install-gatsby-image-and-source-local-images-from-the-filesystem"
  lessonTitle="Install gatsby-image and source local images from the filesystem"
/>

4. Escrever uma consulta GraphQL usando um dos ["fragmentos" do GraphQL](/packages/gatsby-image/#fragments) que especificam os campos necessários para o `gatsby-image` criar uma imagem responsiva e otimizada. Este exemplo consulta uma imagem em um caminho relativo ao local especificado nas opções `gatsby-source-filesystem` usando o fragmento `GatsbyImageSharpFluid`.

```graphql
file(relativePath: { eq: "images/default.jpg" }) {
      childImageSharp {
        # Specify the image processing specifications right in the query.
        fluid {
          ...GatsbyImageSharpFluid
        }
      }
}
```

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-gatsby-image-with-an-image-from-a-relative-path"
  lessonTitle="Use gatsby-image with an image from a relative path"
/>

5. Importar o `Img` para exibir o fragmento em JSX. Existem recursos adicionais disponíveis com a tag `Img`, como o atributo `alt` para acessibilidade.

```jsx
import Img from "gatsby-image"

export default ({ data }) => (
  <div>
    <h1>Hello gatsby-image</h1>
    <Img
      fluid={data.file.childImageSharp.fluid}
      alt="Gatsby Docs are awesome"
    />
  </div>
)
```

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-gatsby-image-s-graphql-fragments-for-blurred-up-and-traced-svg-images"
  lessonTitle="Use gatsby-image's GraphQL fragments for blurred-up and traced SVG images"
/>

Essa consulta do GraphQL cria vários tamanhos da imagem e, quando a página é renderizada, é usada a imagem apropriada para a resolução de tela atual (computador, dispositivo móvel, etc.). O componente `gatsby-image` ativa automaticamente um efeito de desfoque, bem como imagens _lazy loading_ que não estão atualmente na tela.

Portanto, tudo isso é muito bom e é muito melhor poder usar isso pelo npm do que implementá-lo você mesmo ou juntar várias bibliotecas independentes.

### Recursos adicionais

- [Documentação da API Gatsby Image](/docs/gatsby-image/)
- [Arquivo README do plugin gatsby-image](/packages/gatsby-image/)
- [Código-fonte de um exemplo de um site usando o gatsby-image](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-gatsby-image)
- [Artigos sobre o gatsby-image](/blog/tags/gatsby-image/)
- [Starters que usam o gatsby-image](/starters/?d=gatsby-image&v=2)
- [Outros plugins de imagem image](/plugins/?=image)
- ["Otimização de imagem ridiculamente fácil com o gatsby-image" by Kyle Gill](https://medium.com/@kyle.robert.gill/ridiculously-easy-image-optimization-with-gatsby-js-59d48e15db6e)
