---
title: Estilo de Componentes de Escopo com CSS Modules
---

Componentes de Escopo CSS permite que você escreva um CSS portável com um efeito colateral mínimo: com eles, desaparecem as preocupações de colisões de nomes de seletor ou de afetar o estilo de outros componentes

Gatsby funciona por padrão com [CSS Modules](https://github.com/css-modules/css-modules), uma solução popular para escrita de Componentes de Escopo CSS. Aqui está um [exemplo de site que usa CSS Modules](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-css-modules).

## O que é CSS Module?

Citação da [CSS Module homepage](https://github.com/css-modules/css-modules):

> Um **CSS Module** é um arquivo CSS onde todos os nomes de classe e animação são de escopo local por padrão

CSS Modules permite você escrever estilos em arquivos CSS mas consumi-los como objetos JavaScript para processamento adicional e segurança. CSS Modules são bastante populares por que eles fazem automaticamente nomes de classes e animações únicos para que você não tenha que se preocupar com colisões de nomes de seletor.

### Exemplo de CSS Module

O CSS em um módulo CSS não é diferente de um CSS comum, mas a extensão do arquivo é diferente para marcar que aquele arquivo será processado.

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

```jsx:title=src/components/container.js
import React from "react"
// highlight-next-line
import containerStyles from "./container.module.css"

export default ({ children }) => (
  // highlight-next-line
  <section className={containerStyles.container}>{children}</section>
)
```

Neste exemplo, um módulo CSS foi importado e declarado como um objeto JavaScript chamado `containerStyles`. Então, uma classe CSS daquele objeto é referenciada no atributo JSX `className` com `containerStyles.container` que renderiza em HTML com nomes de classes CSS dinâmicas como `container-module--container--3MbgH`.

### Habilitando stylesheets do usuário com um nome de classe estável

Adicionando um CSS `className` persitente à sua marcação JSX juntamente com o seu código de CSS Modules facilita usuários a ter vantagem sobre o [User Stylesheets](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para ter acessibilidade.

Aqui está um exemplo onde o nome de classe `container` é adicionado ao DOM junto com os nomes de classe criados dinamicamente pelo módulo:

```jsx:title=src/components/container.js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <section className={`container ${containerStyles.container}`}>
    {children}
  </section>
)
```
Um usuário do site poderia então escrever seus próprios estilos CSS combinando elementos HTML com um nome de classe de `.container`, e ele não seria afetado se o nome ou caminho do módulo CSS mudasse.

## Quando usar CSS Modules

CSS Modules são altamente recomendados para aqueles que começaram um projeto com Gatsby (e com React em geral) pois eles permitem que você escreva arquivos CSS regulares e portáteis enquanto obtém benefícios de desempenho como apenas empacotar código referenciado.

## Como construir uma página usando CSS Modules

Visite a [seção CSS Modules deste tutorial](/tutorial/part-two/#css-modules) para uma visita guiada à construção de uma página com módulos CSS.
