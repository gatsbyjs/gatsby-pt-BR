---
title: API de imagem do Gatsby
---

Parte do que faz com que sites feitos em Gatsby sejam tão rápidos, é o método recomendado para lidar com imagens no mesmo. O `gatsby-image` é um componente do React projetado para funcionar de forma integrada com as ferramentas do Gatsby de [processamento nativo de imagens](https://image-processing.gatsbyjs.org/) alimentado pelo GraphQL e o plugin [gatsby-plugin-sharp](/packages/gatsby-plugin-sharp/), para otimizar de forma fácil e completa o carregamento de imagens para os seus sites.

> _Nota: O gatsby-image **não** é um substituto para `<img />`. O mesmo é otimizado para imagens responsivas de largura/altura fixa e imagens que expandem para ocupar toda a largura de um contêiner. Existem ainda outros modos de [trabalhar com imagens](/docs/images-and-files/) no Gatsby que não exigem GraphQL.

Demonstração: [https://using-gatsby-image.gatsbyjs.org/](https://using-gatsby-image.gatsbyjs.org/)

## Nesse documento

- [Configurando o Gatsby Image](#configurando-o-gatsby-image)
- [Tipos de imagens com o gatsby-image](#tipos-de-imagens-com-o-gatsby-image)
  - [Imagens fixas e parâmetros](#imagens-com-largura-e-altura-fixas)
  - [Imagens fluidas e parâmetros](#imagens-que-expandem-por-todo-o-contêiner-fluido)
  - [Imagens redimensionadas](#imagens-redimensionadas)
  - [Parametros de consulta compartilhados](#parâmetros-de-consulta-compartilhados)
- [Fragmentos de consulta do Image](#fragmentos-de-consulta-do-image)
- [props do Gatsby-image](#props-do-gatsby-image)

## Configurando o Gatsby Image

Para começar a trabalhar com o Gatsby Image, instale o pacote `gatsby-image` junto com os plugins necessários `gatsby-transformer-sharp` e `gatsby-plugin-sharp`. Faça referência ao pacote em seu arquivo `gatsby-config.js`. Você pode ainda adicionar opções extras para o [`gatsby-plugin-sharp`](/packages/gatsby-plugin-sharp/) no seu arquivo de configuração.

Um meio comum de adicionar imagens, é instalar e usar o `gatsby-source-filesystem` para conectar os seus arquivos locais, mas outros plugins de fontes podem ser usados também, como os plugins `gatsby-source-contentful`, `gatsby-source-datocms` e `gatsby-source-sanity`.

```bash
npm install --save gatsby-image gatsby-plugin-sharp gatsby-transformer-sharp
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-transformer-sharp`,
    `gatsby-plugin-sharp`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/data/`,
      },
    },
  ],
}
```

_Para instruções de instalação aprofundadas, acesse a documentação de [Usando o Gatsby Image](/docs/using-gatsby-image/)._

### O Gatsby image começa com uma consulta

Para alimentar dados de arquivos no Gatsby Image, configure uma [consulta do GraphQL](/docs/graphql-reference/) e ou passe a mesma como uma prop ou a escreva diretamente no componente. Uma técnica é utilizar o hook [`useStaticQuery`](/docs/use-static-query/).

Consultas comuns do GraphQL para adicionar imagens incluem `file` através do plugin [gatsby-source-filesystem](/packages/gatsby-source-filesystem/),  e ambos `imageSharp` e `allImageSharp` do [gatsby-plugin-sharp](/packages/gatsby-plugin-sharp/), mas no final das contas as opções disponíveis para você vão depender das suas fontes de conteúdo.

> Nota: você pode ainda utilizar [pseudônimos no GraphQL](/docs/graphql-reference/#aliasing) para consultar múltiplas imagens do mesmo tipo.

Veja abaixo exemplos de códigos de consultas, e como usá-las em componentes.

## Tipos de imagens com o `gatsby-image`

Objetos de imagem do Gatsby são criados através de métodos do GraphQL. Dois tipos de otimização de imagens são disponíveis, _fixed_ (fixo) e _fluid_ (fluido), que cria imagens de múltiplos tamanhos(1x, 1.5x, etc.). Existe ainda o método _resize_ (redimensionar), que retorna uma única imagem.

### Imagens com largura e altura fixas

Cria imagens automaticamente para diferentes resoluções a uma dada largura e altura - o Gatsby cria imagens responsivas para densidades de pixel de 1x, 1.5x, e 2x utilizando o elemento `<picture>`.

Tendo feito a consulta de uma imagem `fixed` para obter os seus dados, você pode passar os dados para o componente Img.

```jsx
import { useStaticQuery, graphql } from "gatsby"
import Img from "gatsby-image"

export default () => {
  const data = useStaticQuery(graphql`
    query {
      file(relativePath: { eq: "images/default.jpg" }) {
        childImageSharp {
          # Especifica uma imagem fixa e fragmento.
          # A largura padrão é de 400 pixels
          // highlight-start
          fixed {
            ...GatsbyImageSharpFixed
          }
          // highlight-end
        }
      }
    }
  `)
  return (
    <div>
      <h1>Hello gatsby-image</h1>
      <Img
        fixed={data.file.childImageSharp.fixed} {/* highlight-line */}
        alt="A documentação do Gatsby é o máximo"
      />
    </div>
  )
}
```

#### Parâmetros de consulta de uma imagem fixa

Na consulta, você pode especificar opções para imagens fixas.

- `width` (int, padrão: 400)
- `height` (int)
- `quality` (int, padrão: 50)

#### Retorna

- `base64` (string)
- `aspectRatio` (float)
- `width` (float)
- `height` (float)
- `src` (string)
- `srcSet` (string)

Neste ponto, fragmentos como `GatsbyImageSharpFixed` são úteis, pois eles retornam todos os itens acima em uma linha unica sem ter que escrever todos:

```graphql
file(relativePath: { eq: "images/default.jpg" }) {
  childImageSharp {
    // highlight-start
    fixed(width: 400, height: 400) {
      ...GatsbyImageSharpFixed
      // highlight-end
    }
  }
}
```

Leia mais no `README` do plugin [gatsby-plugin-sharp](/packages/gatsby-plugin-sharp/?=#fixed).

### Imagens que expandem por todo o contêiner fluido

Cria tamanhos flexíveis para imagens que expandem para preencher todo o seu contêiner. E.g. para um contêiner cuja largura máxima seja 800px, os tamanhos automáticos seriam: 200px, 400px, 800px, 1200px e 1600px - o suficiente para fornecer tamanhos ótimos de imagem para todo tamanho de dispositivo / resolução de tela. Caso você queira mais controle sobre quais tamanhos são criados, você pode utilizar o parâmetro `srcSetBreakpoints`.

Tendo feito a consulta por uma imagem do tipo `fluid` para obter os seus dados, você pode passar os mesmos para o componente `Img`:

```jsx
import { useStaticQuery, graphql } from "gatsby"
import Img from "gatsby-image"

export default () => {
  const data = useStaticQuery(graphql`
    query {
      file(relativePath: { eq: "images/default.jpg" }) {
        childImageSharp {
          # Específica uma imagem fluida e o fragmento
          # O valor padrão para o parâmetro maxWidth é de 800 pixels
          // highlight-start
          fluid {
            ...GatsbyImageSharpFluid
          }
          // highlight-end
        }
      }
    }
  `)
  return (
    <div>
      <h1>Hello gatsby-image</h1>
      <Img
        fluid={data.file.childImageSharp.fluid} {/* highlight-line */}
        alt="A documentação do Gatsby é o máximo"
      />
    </div>
  )
}
```

#### Parâmetros de consulta de uma imagem fluida

Em uma consulta, você pode especificar opções para imagens fluidas.

- `maxWidth` (int, default: 800)
- `maxHeight` (int)
- `quality` (int, default: 50)
- `srcSetBreakpoints` (array of int, default: [])
- `fit` (string, default: `[sharp.fit.cover][6]`)
- `background` (string, default: `rgba(0,0,0,1)`)

#### Retorna

- `base64` (string)
- `src` (string)
- `width` (int)
- `height` (int)
- `aspectRatio` (float)
- `src` (string)
- `srcSet` (string)

Neste ponto, fragmentos como `GatsbyImageSharpFluid` são úteis, pois eles retornam todos os itens acima em uma linha sem ter que digitar todos:

```graphql
file(relativePath: { eq: "images/default.jpg" }) {
  childImageSharp {
    // highlight-start
    fluid(maxWidth: 400) {
      ...GatsbyImageSharpFluid
      // highlight-end
    }
  }
}
```

Leia mais no `README` do plugin [gatsby-plugin-sharp](/packages/gatsby-plugin-sharp/?=#fluid).

### Imagens redimensionadas

Além de imagens _fixed_ (fixas) e _fluid_ (fluidas), a API gatsby-image permite que você utilize o método `resize` (redimensionar) com o `gatsby-plugin-sharp` para retornar imagens únicas, ao invés de múltiplos tamanhos. Não existem fragmentos padrões disponíveis para utilizar com o método de redimensionamento.

#### Parâmetros

- `width` (int, default: 400)
- `height` (int)
- `quality` (int, default: 50)
- `jpegProgressive` (bool, default: true)
- `pngCompressionLevel` (int, default: 9)
- `base64`(bool, default: false)

#### Retorna

Redimensionar retorna um objeto com os seguintes itens:

- `src` (string)
- `width` (int)
- `height` (int)
- `aspectRatio` (float)

```graphql
allImageSharp {
  edges {
    node {
        resize(width: 150, height: 150, grayscale: true) {
          src
        }
    }
  }
}
```

### Parâmetros de consulta compartilhados

Além das configurações do `gatsby-plugin-sharp` em `gatsby-config.js`, existem opções de consulta adicionais que aplicam para imagens _fluid_ ou _fixed_:

- `grayscale` (bool, default: false)
- `duotone` (bool|obj, default: false)
- `toFormat` (string, default: \`\`)
- `cropFocus` (string, default: `[sharp.strategy.attention][6]`)
- `pngCompressionSpeed` (int, default: 4)

Abaixo temos um exemplo de uso da opção `duotone` com uma imagem fixa:

```graphql
fixed(
  width: 800,
  duotone: {
    highlight: "#f00e2e",
    shadow: "#192550"
  }
)
```

<figure>
  <img alt="Jay Gatsby segurando uma taça  de vinho em cores normais e duotone." src="./images/duotone-before-after.png" />
  <figcaption>
    Duotone | Antes - Depois
  </figcaption>
</figure>

E um exemplo do uso da opção `grayscale` com uma imagem fixa:

```graphql
fixed(
  grayscale: true
)
```

<figure>
  <img alt="Jay Gatsby segurando uma taça  de vinho em cores normais e preto e branco." src="./images/grayscale-before-after.png" />
  <figcaption>
    Grayscale | Antes - Depois
  </figcaption>
</figure>

Leia mais no `README` do plugin [`gatsby-plugin-sharp`](/packages/gatsby-plugin-sharp).

## Fragmentos de consulta do Image

O GraphQL inclui um conceito chamado "fragmentos de consulta", que são partes de uma consulta que podem ser reutilizados. Para projetar facilmente com o `gatsby-image`, o plugin de processamento de imagens do Gatsby, que suporta o `gatsby-image`, e feito com fragmentos que você pode facilmente incluir em suas consultas.

> Nota: utilizar fragmentos em suas consultas depende da fonte de dados que você configurou. Leia mais no `README` do plugin [gatsby-image](/packages/gatsby-image#fragments).

### Fragmentos populares do `gatsby-transformer-sharp`

#### Imagens fixas

- `GatsbyImageSharpFixed`
- `GatsbyImageSharpFixed_noBase64`
- `GatsbyImageSharpFixed_tracedSVG`
- `GatsbyImageSharpFixed_withWebp`
- `GatsbyImageSharpFixed_withWebp_noBase64`
- `GatsbyImageSharpFixed_withWebp_tracedSVG`

#### Imagens fluidas

- `GatsbyImageSharpFluid`
- `GatsbyImageSharpFluid_noBase64`
- `GatsbyImageSharpFluid_tracedSVG`
- `GatsbyImageSharpFluid_withWebp`
- `GatsbyImageSharpFluid_withWebp_noBase64`
- `GatsbyImageSharpFluid_withWebp_tracedSVG`

#### Sobre `noBase64`

Caso você não queira utilizar o [efeito de desfocar](https://using-gatsby-image.gatsbyjs.org/blur-up/), escolha o fragmento com `noBase64` no final.

#### Sobre `tracedSVG`

Caso você queira utilizar o [SVG traçado para reserva do espaço](https://using-gatsby-image.gatsbyjs.org/traced-svg/), escolha o fragmento com `tracedSVG` no final.

#### Sobre `withWebP`

Caso você queira utilizar automaticamente [imagens WebP](https://developers.google.com/speed/webp/) quando o navegador tiver suporte ao formato, utilize o fragmento 'withWebp'. Caso o navegador não tenha suporte a Webp, o `gatsby-image` volta para o formato de imagem padrão.

Aqui temos um exemplo da utilização de fragmentos não padrões do `gatsby-transformer-sharp`. Sempre escolha um que corresponda ao tipo de imagem desejada por você (_fixed_ ou _fluid_):

```graphql
file(relativePath: { eq: "images/default.jpg" }) {
  childImageSharp {
    fluid {
      // highlight-next-line
      ...GatsbyImageSharpFluid_tracedSVG
    }
  }
}
```

Para mais informações de como essas opções funcionam, confira a demonstração do Gatsby Image: [https://using-gatsby-image.gatsbyjs.org/](https://using-gatsby-image.gatsbyjs.org/)

#### Fragmentos adicionais do plugin

Adicionalmente, plugins com suporte ao `gatsby-image` atualmente incluem [gatsby-source-contentful](/packages/gatsby-source-contentful/), [gatsby-source-datocms](https://github.com/datocms/gatsby-source-datocms) e [gatsby-source-sanity](https://github.com/sanity-io/gatsby-source-sanity). Veja o `README` do [gatsby-image](/packages/gatsby-image/#fragments) para mais detalhes.

## props do Gatsby-image

Após ter feito a sua consulta, você pode passar opções adicionais para o componente gatsby-image.

| Nome                   | Tipo                | Descrição                                                                                                                   |
| ---------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `fixed`                | `object`            | Dados retornados da consulta `fixed`                                                                                          |
| `fluid`                | `object`            | Dados retornados da consulta `fluid`                                                                                          |
| `fadeIn`               | `bool`              | Muda o padrão para fading no carregamento da imagem                                                                                       |
| `durationFadeIn`       | `number`            | A duração do fade-in é configurada para 500ms por padrão                                                                                |
| `title`                | `string`            | Passado para o elemento HTML `img` renderizado.                                                  |
| `alt`                  | `string`            | Passado para o elemento HTML `img` renderizado. Por padrão é passada uma string vazia, e.g. `alt=""`                                                  |
| `crossOrigin`          | `string`            | Passado para o elemento HTML `img` renderizado                                                  |
| `className`            | `string` / `object` | Passado para o elemento de empacotador. Um objeto é necessário para ter suporte a propriedade css Glamor's                                                  |
| `style`                | `object`            | Se espalha para o estilo padrão do elemento empacotador                                                                         |
| `imgStyle`             | `object`            | Se espalha para o estilo padrão do elemento `img`                                                                    |
| `placeholderStyle`     | `object`            | Se espalha para o estilo padrão do elemento de reserva de espaço do elemento `img`                                                                |
| `placeholderClassName` | `string`            | Uma classe que é passada para o elemento de reserva de espaço do elemento `img`|
| `backgroundColor`      | `string` / `bool`   | Configura um elemento de reserva de espaço colorido. Caso seja verdadeiro, utiliza "lightgray" (cinza claro) como a cor. Você pode ainda passar qualquer string de cor válida.   |
| `onLoad`               | `func`              | Uma função callback que é chamada quando a imagem tiver carregado em tamanho completo.                                                                |
| `onStartLoad`          | `func`              | Uma função callback que é chamada quando a imagem em tamanho completo começar a carregar, ela recebe o parâmetro fornecido `{ wasCached: <boolean> }`. |
| `onError`              | `func`              | Uma função callback que é chamada quando a imagem falha em carregar. |
| `Tag`                  | `string`            | Qual tag HTML utilizar para o elemento empacotador. O padrão utilizado é `div`.                                                               |
| `objectFit`            | `string`            | Passado para o `object-fit-images` polyfill quando importando do `gatsby-image/withIEPolyfill`. Por padrão é utilizada a opção `cover`. |
| `objectPosition`       | `string`            | Passado para o `object-fit-images` polyfill quando importando do `gatsby-image/withIEPolyfill`. Por padrão e passado o valor `50% 50%`.          |
| `loading`              | `string`            | Configura o atributo de carregamento com atraso nativo do navegador. Uma das seguintes opcoes `lazy`, `eager` ou `auto`. Por padrão e passada a opção `lazy`.                        |
| `critical`             | `bool`              | Optar por não utilizar a opção de carregamento com atraso. Por padrão é utilizado o valor `false`. Obsoleto, utilize a opção `loading` no lugar.                                     |

Aqui temos alguns exemplos do uso:

```jsx
<Img
  fluid={data.file.childImageSharp.fluid}
  alt="Gato ocupando por completo uma cadeira"
  fadeIn="false"
  className="customImg"
  placeholderStyle={{ `backgroundColor`: `black` }}
  onLoad={() => {
    // do loading stuff
  }}
  onStartLoad={({ wasCached }) => {
    // faça algo quando começar a carregar
    // opcionalmente com o parâmetro booleano wasCached
  }}
  onError={(error) => {
    // faça algo quando encontrar erro
  }}
  Tag="imagem-personalizada"
  loading="ansioso"
/>
```
