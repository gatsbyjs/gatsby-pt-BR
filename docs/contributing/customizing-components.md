# Customizando Componentes

Usando o MDX, você pode substituir cada elemento HTML que o Markdown processa por uma implementação customizada. Isso permite que você utilize um conjunto de componentes do sistema de design ao renderizar.

```javascript
import { MDXProvider } from "@mdx-js/react"
import * as DesignSystem from "your-design-system"

export default function Layout({ children }) {
  return (
    <MDXProvider
      components={{
        // Map HTML element tag to React component
        h1: DesignSystem.H1,
        h2: DesignSystem.H2,
        h3: DesignSystem.H3,
        // Or define component inline
        p: props => <p {...props} style={{ color: "rebeccapurple" }} />,
      }}
    >
      {children}
    </MDXProvider>
  )
}
```

Os seguintes componentes podem ser customizados com o MDXProvider:

|Tag|Name|Syntax|
|---|-----|------|
| p | [Parágrafo](https://github.com/syntax-tree/mdast#paragraph) |	
| h1 | [Título 1](https://github.com/syntax-tree/mdast#heading) | # |
| h2 | [Título 2](https://github.com/syntax-tree/mdast#heading) | ## |
| h3 | [Título 3](https://github.com/syntax-tree/mdast#heading) | ### |
| h4 | [Título 4](https://github.com/syntax-tree/mdast#heading) | #### |
| h5 | [Título 5](https://github.com/syntax-tree/mdast#heading) | ##### |
| h6 | [Título 6](https://github.com/syntax-tree/mdast#heading) | ###### |
| thematicBreak | [Quebra de tema](https://github.com/syntax-tree/mdast#thematicbreak) | *** |
| blockquote | [Citação](https://github.com/syntax-tree/mdast#blockquote) |	> |
| ul | [Lista](https://github.com/syntax-tree/mdast#list) | - |
| ol | [Lista Ordenada](https://github.com/syntax-tree/mdast#list) | 1. |
| li | [Lista](https://github.com/syntax-tree/mdast#listitem) | item |
| table | [Tabela](https://github.com/syntax-tree/mdast#table) | --- \| --- \| --- \| ---|
| tr | [Linha de tabela](https://github.com/syntax-tree/mdast#tablerow) | Linha | Isso \| é \| uma \| Linha de tabela |
| td/th | [Célula de tabela](https://github.com/syntax-tree/mdast#tablecell) |
| pre | [Pre](https://github.com/syntax-tree/mdast#code) |	```js console.log()``` |
| code| [Código](https://github.com/syntax-tree/mdast#code) | `console.log()` |
| em | [Itálico](https://github.com/syntax-tree/mdast#emphasis) | _Itálico_ |
| strong | [Negrito](https://github.com/syntax-tree/mdast#strong) | **Negrito** |
| delete | [Corte horizontal](https://github.com/syntax-tree/mdast#delete) |	~~strikethrough~~ |
| code | [Código em linha](https://github.com/syntax-tree/mdast#inlinecode) | `console.log()` |
| hr | [Quebra / Pausa](https://github.com/syntax-tree/mdast#break) | --- |
| a | [Link](https://github.com/syntax-tree/mdast#link) | <https://mdxjs.com> or [MDX](https://mdxjs.com) |
| img| [Imagem](https://github.com/syntax-tree/mdast#image) | ![alt](https://mdx-logo.now.sh) |

### Como isso funciona?
Componentes passados para o MDXProvider são usados para renderizar o elemento HTML que o Markdown cria. Isso usa [React's Context API](https://reactjs.org/docs/context.html)

### Relacionado
- [MDX components](https://mdxjs.com/getting-started)
