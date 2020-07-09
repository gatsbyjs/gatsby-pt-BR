---
title: Componentes de layout
---

Nesse guia você vai entender qual a abordagem do Gatsby em relação a layouts, como criar, usar componentes de layout e como evitar que esses componentes desmontem.

## Abordagem da Gatsby para layouts

Por padrão, o gatsby não aplica o layout nas páginas de forma automática(Existem formas de fazer isso, mas serão abordadas em uma seção futura). Ao invés disso, o Gastsby segue o modelo composicional do React na sua forma de importar e usar componentes. Isso faz com que seja possível criar multiplos níveis de layout, como por exemplo, um cabeçalho e rodapé globais e em algumas páginas um menu lateral. Isso faz com que a transição de dados entre o layout e os componentes da página seja mais fácil de ser concretizada.

## O que são componentes de layout?

Componentes de layout existem para permitir o compartilhamento de seções do seu site entre diversas páginas. Por exemplo, os sites da Gatsby normalmente tem um componente de layout de cabeçalho e footer que são compartilhados. Outra coisa comum de se adicionar aos layouts são as barras laterais e/ou menus de navegação. Nessa página por exemplo, o cabeçalho no topo é parte do componente de layout da gatsbyjs.org.

## Como criar componentes de layout

É recomendável criar componentes de layout junto com o resto dos seus componentes (Por exemplo, dentro do `src/components/`).

Aqui está um exemplo de um componente bem básico dentro do `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

## Como importar e adicionar componentes de layout nas páginas

Se você quer aplicar algum layout a uma página você precisará incluir o componente `Layout` e colocar sua página dentro dele. O exemplo a seguir mostra como você pode aplicar seu layout a uma página inicial.

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>I’m in a layout!</h1>
  </Layout> {/* highlight-line */}
)
```

Repita isso para todas as páginas e templates que precisarem desse layout.

## Como previnir que os componentes de layout desmontem 

Como mencionado anteriormente, por padrão o Gastby não empacota as páginas que estão dentro de um componente de layout de forma automático. O componente "top level" é a própria página. Dessa forma, quando o componente "top level" muda de uma página pra outra o React vai re-renderizar todos os seus filhos. Isso significa que os componentes compartilhados, como navegação por exemplo, irão ser desmontados e remontados. Isso causará a quebra das transições do CSS ou do estado do React dentro daqueles componentes compartilhados.

Se você precisar criar um componente wrapper junto a componentes da página que não serão desmontados com as alterações dessa página, use a [API de navegação](/docs/browser-apis/#wrapPageElement) **`wrapPageElement`** e o [SSR equivalente](/docs/ssr-apis/#wrapPageElement).

Você também pode evitar que o componente layout seja desmontado usando o [gatsby-plugin-layout](/packages/gatsby-plugin-layout/), que implementa as APIs `wrapPageElement` por você. 

## Outros recursos

- [Criando componentes de layout aninhado com o Gatsby](/tutorial/part-three/)
- [A vida depois dos layouts no Gatsby V2](/blog/2018-06-08-life-after-layouts/)
- [Migrando da v1 para a v2](/docs/migrating-from-v1-to-v2/#remove-or-refactor-layout-components)
- [gatsby-plugin-layout](/packages/gatsby-plugin-layout/)
- [API de navegação do WrapPageElement](/docs/browser-apis/#wrapPageElement)
- [API SSR do wrapPageElement](/docs/ssr-apis/#wrapPageElement)