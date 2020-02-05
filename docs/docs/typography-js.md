---
title: Typography.js
---

## Usando Typography.js no Gatsby

Typography.js é uma biblioteca JavaScript que permite explorar o design tipográfico do seu site e definir belos temas tipográficos personalizados e pré-existentes. Ele permite que você altere a fonte do seu site com facilidade. Atualmente, o Typography.js mantém mais de 30 temas para você usar. Você também pode criar seus próprios temas de fonte personalizados, se nenhum tema disponível atender aos seus requisitos. Para usar Typography em seu projeto, você instalará um [plugin Gatsby](https://www.gatsbyjs.org/packages/gatsby-plugin-typography/) e especificará um objeto de configuração para Typography.

## Instalando o plugin Typography

O Gatsby possui o plugin `gatsby-plugin-typography` para integrar o Typography.js ao seu projeto.

Você pode instalar o plugin e suas dependências no seu projeto executando o comando `npm install gatsby-plugin-typography react-typography typography --save`

Após a instalação do plugin, navegue até o arquivo `gatsby-config.js` localizado na raiz do diretório do seu projeto e adicione o plugin à configuração:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
    // highlight-end
  ],
}
```

`gatsby-plugin-typography` tem duas opções para que você especifique:

- **pathToConfigModule** (string): O caminho para o arquivo para o qual você exporta sua configuração do Typography.
- **omitGoogleFont** (boolean, `default: false`): Por padrão, o Typography inclui um auxiliar que solicita à CDN do Google Font as fontes necessárias. Você pode usar suas próprias fontes, injetando fontes ou usando um CDN de sua escolha. Ao definir `omitGoogleFont: true`, o `gatsby-plugin-typography` ignorará a adição do auxiliar de fonte. Em vez disso, você deverá incluir as fontes apropriadas - veja [Adicionando uma fonte local](/docs/recipes/styling-css#adding-a-local-font)

## Criando a configuração do Typography

Agora que você adicionou o plugin, crie o diretório `src/utils/` se ele ainda não existir no seu projeto e adicione um novo arquivo chamado `typography.js`. Você usará esse arquivo para especificar a configuração do Typography e definir esse arquivo como o caminho para a opção `pathToConfigModule`.

Dentro do arquivo `typography.js` que você criou, você define a configuração de tipografia do seu site. Uma configuração básica do typography.js é semelhante a esta:

```js:title=src/utils/typography.js
import Typography from "typography"

const typography = new Typography({
  baseFontSize: "18px",
  baseLineHeight: 1.666,
  headerFontFamily: [
    "Avenir Next",
    "Helvetica Neue",
    "Segoe UI",
    "Helvetica",
    "Arial",
    "sans-serif",
  ],
  bodyFontFamily: ["Georgia", "serif"],
})

export default typography
```

Se você estiver instalando o Typography.js em um projeto existente do Gatsby que iniciou, precisará excluir todos os estilos de fonte CSS conflitantes da sua base de código em favor das novas configurações do Typography.js.

Os tamanhos das fontes de todos os elementos no Typography.js aumentam e diminuem em relação ao `baseFontSize` definido acima. Tente brincar com esse valor e veja a diferença visual que ele pode fazer no seu site.

Para encontrar ou criar um novo tema de tipografia, você pode visitar [Typography.js](https://kyleamathews.github.io/typography.js/) para ver uma lista de opções.

## Instalando temas Typography

O Typography.js possui temas incorporados que podem economizar tempo ao definir o estilo da fonte do seu site. O tema Funston, mantido pelo Typography, é um dos temas incorporados. Para instalar o tema Funston a partir do npm, execute o comando: `npm install typography-theme-funston --save`

Para usar o tema, edite o arquivo `typography.js` que você criou antes e informe a Typography sobre a nova configuração:

```diff:title=src/utils/typography.js
import Typography from "typography";
// highlight-start
+ import funstonTheme from 'typography-theme-funston'
// highlight-end
const typography = new Typography(
- {
-     baseFontSize: '18px',
-     baseLineHeight: 1.666,
-     headerFontFamily: ['Avenir Next', 'Helvetica Neue', 'Segoe UI', 'Helvetica', 'Arial', 'sans-serif'],
-     bodyFontFamily: ['Georgia', 'serif'],
- },
// highlight-start
+ funstonTheme
// highlight-end
);

export default typography;
```

Após concluir os passos acima, você pode iniciar o servidor de desenvolvimento usando o comando `gatsby develop` e navegar para o site local `http://localhost:8000`. Se tudo der certo, você deverá ver o texto em seu site usando o tema tipográfico da Funston.

**Nota**: Se suas fontes permanecerem inalteradas, remova todas as chamadas `font-family` no seu CSS e verifique novamente.

Para encontrar mais temas para instalar, consulte o site oficial do [Typography.js](https://kyleamathews.github.io/typography.js/).
