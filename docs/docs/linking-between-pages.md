---
title: Vinculação entre páginas
---

Este guia aborda como vincular páginas em um site que use o Gatsby.

## O componente _link_ do Gatsby

O componente `<Link />` do Gatsby é usado para vincular as páginas do seu site. Para links externos não controlados pelo Gatsby use a tag regular `<a>` do HTML.

## Usando o componente `<Link />` para vinculações internas

Aqui está um exemplo de criação de um vínculo entre duas páginas em um site com o Gatsby.

Abra o componente de página (ex. `src/pages/index.js`) no seu site. Importe o componente `Link` do Gatsby, o que permite que ele seja usado dentro do componente de página.
Adicione o componente `<Link />` abaixo do cabeçalho, e adicione a propriedade `to` e como valor o caminho `"/contato/"`:

```jsx
import React from "react"
import { Link } from "gatsby"

export default () => (
  <div>
    <Link to="/contato/">Contato</Link>
  </div>
)
```

O código acima adicionará um vínculo à página de contato, renderizado automaticamente em HTML como `<a href="/contact/">` mas com benefícios adicionais de desempenho. O valor do link é baseado no nome do arquivo da página, que nesse caso seria `contact.js`.

> **Nota:** o valor `"/"` para a propriedade `to` levará os usuários para a página inicial.

## Usando `<a>` para vínculos externos

Se você estiver vinculando páginas que não são controladas pelo seu site Gatsby (como em um domínio diferente), use a tag nativa do HTML `<a>`, em vez do _Link_ do Gatsby.

Além disso se você deseja abrir um vínculo externo em uma nova janela usando o atributo `target`, use o atributo `rel` para evitar uma vulnerabilidade onde a [página de referência](https://developer.mozilla.org/en-US/docs/Web/Security/Referer_header:_privacy_and_security_concerns) pode ser substituída dinamicamente via JavaScript:

```jsx
import React from "react"

export default () => (
  <div>
    <a href="https://example.com" target="_blank" rel="noopener noreferrer">
      Link Externo
    </a>
  </div>
)
```

Também é recomendado adicionar um [ícone visual](https://thenounproject.com/term/new-window/2864/) ou algum tipo identificando que trata-se de um vínculo externo.

## Outros materiais

- Para obter o exemplo completo de como vincular páginas, veja na [primeira parte](/tutorial/part-one/#linking-between-pages/) do tutorial
- Confira mais detalhes sobre o roteamento no Gatsby na [documentação da API do Gatsby Link](/docs/gatsby-link/).
