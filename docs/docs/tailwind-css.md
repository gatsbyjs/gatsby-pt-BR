---
title: Tailwind CSS
---

Tailwind é uma estrutura [utility-first](https://tailwindcss.com/docs/utility-first/) CSS para criar rapidamente interfaces de usuário personalizadas. Este guia mostra como iniciar com Gatsby e o [Tailwind CSS](https://tailwindcss.com/).

## Visão geral

Existem duas maneiras de usar o Tailwind com o Gatsby:

1. Standard: Use o PostCSS para gerar classes Tailwind, e você poderá aplicá-las usando `className`.
2. CSS-in-JS: Integrar classes Tailwind com Styled-Components.

Você precisa instalar e configurar o Tailwind para ambos os métodos, portanto, este guia percorrerá essa etapa primeiro, e então você pode seguir as instruções para PostCSS ou CSS-in-JS.

## Instalando e configurando o Tailwind

Este guia pressupõe que você já tenha um projeto Gatsby configurado. Se você precisar configurar um projeto, acesse o [**Guia de Inicio Rápido**](/docs/quick-start), e depois volte aqui.

1. Instale o Tailwind

```shell
npm install tailwindcss --save-dev
```

2. Gere o arquivo de configuração Tailwind  (opcional)

**Nota**: Não é necessário um arquivo de configuração para o Tailwind 1.0.0+

Para configurar o Tailwind, você precisará adicionar um arquivo de configuração Tailwind. Felizmente, Tailwind tem um script interno para fazer isso. Basta executar o seguinte comando:

```shell
npx tailwind init
```

### Opção #1: PostCSS

1.  Instale o plugin Gatsby PostCSS [**gatsby-plugin-postcss**](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-postcss).

```shell
npm install --save gatsby-plugin-postcss
```

2.  Inclua o plugin no seu arquivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-postcss`],
```

3. Configure o PostCSS para usar o Tailwind

Crie um `postcss.config.js` na pasta raiz do seu projeto com o seguinte conteúdo.

```javascript:title=postcss.config.js
module.exports = () => ({
  plugins: [require("tailwindcss")],
})
```

4. Use as diretivas Tailwind no seu CSS

Agora você pode usar as diretivas `@tailwind` para adicionar os utilitários do Tailwind, [preflight](https://tailwindcss.com/docs/preflight/) e componentes em seu CSS. Você também pode usar o `@apply` e todas as outras diretivas e funções do Tailwind!

Para saber mais sobre como usar o Tailwind no seu CSS, visite a [Documentação do Tailwind](https://tailwindcss.com/docs/installation#3-use-tailwind-in-your-css).

### Opção #2: CSS-in-JS

Essas etapas supõem que você já tenha uma biblioteca CSS-in-JS instalada e os exemplos são baseados na biblioteca Styled Components.

1. Instale o Tailwind Babel Macro

**Nota**: `tailwind.macro` atualmente não é compatível com Tailwind 1.0.0+. Contudo, um beta compatível está disponível em `tailwind.macro@next`. Sinta-se à vontade para usar o beta ou reverter para o TailwindCSS 0.7.4.

**Opção 1**: Instale `tailwind.macro@next` e use o Tailwind 1.0.0+

```shell
npm install --save tailwind.macro@next
```

**Opção 2**: Instale a versão estável do `tailwind.macro` estável e use o Tailwind 0.7.4

```bash
// Remova o tailwind 1.0.0+ se você já o instalou
npm uninstall tailwindcss

// Instale o tailwind 0.7.4 e a versão estável do tailwind.macro
npm install tailwindcss@0.7.4
npm install tailwind.macro
```

2. Use o Babel Macro (tailwind.macro) no seu styled component

```javascript
import styled from "styled-components"
import tw from "tailwind.macro"

// Todas as versões
const Button = styled.button`
  ${tw`bg-blue hover:bg-blue-dark text-white p-2 rounded`};
`

// tailwind.macro@next
const Button = tw.button`
  bg-blue hover:bg-blue-dark text-white p-2 rounded
`
```

## Outros recursos

- [Introdução ao PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)
- [Documentação do Tailwind](https://tailwindcss.com/)
- [Projetos Gatsby que usam Tailwind](/starters/?c=Styling%3ATailwind&v=2)
