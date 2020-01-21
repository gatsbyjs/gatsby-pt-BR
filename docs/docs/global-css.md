---
title: Estilo padrão com arquivos CSS globais
---

Tradicionalmente, os sites são estilizados utilizando arquivos CSS globais.

As regras de escopo global são declaradas em arquivos `.css` externos, e a [Especificação CSS](https://developer.mozilla.org/pt-BR/docs/Web/CSS/Specificity) e [Cascade](https://developer.mozilla.org/pt-BR/docs/Web/CSS/Cascade) determinam como os estilos são aplicados.

## Adicionando estilos globais com um componente de layout

A melhor maneira de adicionar estilos globais é com um [componente de layout compartilhado](/tutorial/part-three/#your-first-layout-component). Esse componente é utilizado para itens que são compartilhados em todo o site, incluindo estilos, componentes do cabeçalho e outros itens comuns.

> **NOTA:** Esse padrão é implementado [no _starter_ padrão](https://github.com/gatsbyjs/gatsby-starter-default/blob/02324e5b04ea0a66d91c7fe7408b46d0a7eac868/src/layouts/index.js#L6).

Para criar um layout compartilhado com estilos globais, comece criando um novo _site_ Gatsby com o [_starter_ hello world](https://github.com/gatsbyjs/gatsby-starter-hello-world).

```shell
gatsby new estilos-globais https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Abra seu novo site em seu editor e crie um novo diretório em `/src/components`. Dentro, crie dois novos arquivos:

```diff
  estilos-globais/
  └───src/
      └───components/
+     │   │─  layout.js
+     │   └─  layout.css
      │
      └───pages/
          └─  index.js
```

Dentro de `src/components/layout.css`, adicione alguns estilos globais como:

```css:title=src/components/layout.css
div {
  background: red;
  color: white;
}
```

Em `src/components/layout.js`, inclua a folha de estilos e exporte como um componente de layout:

```jsx:title=src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

Finalmente, atualize o arquivo `src/pages/index.js` para usar o novo componente de layout:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

Execute o comando `npm run develop` e você irá ver o novo estilo global aplicado.

![Estilos globais](./images/global-styles.png)

## Adicionando estilos globais sem um componente de layout

Em alguns casos, usar um componente de layout compartilhado não é o ideal. Nesses casos, você pode incluir uma folha de estilos global usando o `gatsby-browser.js`.

> **NOTA:** Esse método _não_ funciona com CSS-in-JS. Use componentes de estilos compartilhados para utilizar com CSS-in-JS.

Primeiro, abra uma nova janela do terminal e execute os seguintes comandos para criar um novo site padrão em Gatsby e iniciar um servidor de desenvolvimento:

```shell
gatsby new estilos-globais-tutorial https://github.com/gatsbyjs/gatsby-starter-default
cd estilos-globais-tutorial
npm run develop
```

Em seguida, crie um arquivo CSS e defina os estilos como desejar. Por exemplo:

```css:title=src/styles/global.css
html {
  background-color: peachpuff;
}

a {
  color: rebeccapurple;
}
```

E então, inclua a sua folha de estilos no arquivo `gatsby-browser.js` do seu site.

> **NOTA:** Essa solução somente funciona ao incluir o css, pois esses estilos são extraídos ao criar o JavaScript, mas não para o css-in-js.
> Incluir estilos em um componente de layout ou um global-styles.js é a melhor forma de fazer isso.

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"

// ou:
// require('./src/styles/global.css')
```

> _Nota: Você pode usar o require do Node.js ou o import. Além disso, o local do arquivo css na pasta `src/styles` é de sua escolha._

Você verá que seus estilos globais estão tendo efeito em seu site:

![Exemplo estilos globais no site](./images/global-styles-example.png)

### Importando arquivos CSS dentro de componentes

Também é possivel dividir seus estilos CSS em arquivos separados, para que membros da sua equipe possam trabalhar enquanto ainda usam o CSS tradicional. Você pode [importar arquivos diretamente](/docs/importing-assets-into-files/) dentro de páginas, templates ou componentes:

```css:title=menu.css
.menu {
  background-color: black;
  color: #fff;
  display: flex;
}
```

```javascript:title=components/menu.js
import "css/menu.css"
```

Essa abordagem pode simplificar a integração dos estilos CSS ou [Sass](/packages/gatsby-plugin-sass/) no seu _site_ Gatsby, permitindo que os membro da equipe consumam e escrevam um CSS mais tradicional baseado em classes. No entando, existem [contrapartidas](#limitations) que devem ser consideradas com relação ao desempenho web e à falta de exclusão em códigos não utilizados.

### Adicionando classes nos componentes

Como `class` é uma palavra reservada em JavaScript, você irá precisar utilizar o prop `className`, que será renderizado como um atributo, suportado pelo navegador, `class` em seu HTML.

```jsx
<button className="primary">Clique aqui</button>
```

```css
.primary {
  background: orangered;
}
```

### Limitações

O maior problema com arquivos de CSS globais é o risco de conflitos no nome e outros efeitos colaterais como herança não intencional.

Metodologias CSS como o BEM podem ajudar a resolver isso, porém uma solução mais moderna seria escrever o CSS com um escopo local utilziando [Módulos CSS](/docs/css-modules/) ou [CSS-in-JS](/docs/css-in-js/).
