---
title: Sintaxe Markdown
---

A sintaxe Markdown é muito comum na hora de escrever conteúdo em posts e páginas no Gatsby. Este guia contém dicas de escrita e formatações úteis em Markdown.

## Titulação

```markdown
# Título 1

## Título 2

### Título 3

#### Título 4

##### Título 5

###### Título 6
```

As tags acima irão renderizar desta forma no HTML:

# Título 1

## Título 2

### Título 3

#### Título 4

##### Título 5

###### Título 6

- Cada título é convertido à sua tag HTML correspondente
  - i.e. `# Título 1` é `<h1>Título 1</h1>`
- O uso correto de cada título deve seguir os
  [guias de acessibilidade](https://www.w3.org/WAI/tutorials/page-structure/headings/) criado pelo World Wide Web Consortium (W3C)
  _Nota: nas [Documentações do Gatsby](/contributing/docs-contributions#headings), h1s já estão inclusos nas entradas de `título` nos metadados do frontmatter, e contribuições em Markdown devem começar com h2._

## Ênfase textual

- Itálico
  - um asterisco ou um underline
    - `*itálico*` ou `_itálico_`
    - _itálico!_
- Negrito
  - dois asteriscos ou dois underlines
    - `**negrito**` ou `__negrito__`
    - **negrito!**
- Itálico e negrito
  - três asteriscos ou três underlines
    - `***itálico e negrito***` or `___itálico e negrito___`
    - **_itálico e negrito!!_**

## Listas

### Não ordenadas

- Pode-se utilizar `*`, `-`, ou `+` para cada item da lista

<!-- prettier-ignore-start -->
```markdown
* Gatsby
  * docs
- Gatsby
  - docs
+ Gatsby
  + docs
```
<!-- prettier-ignore-end -->

Como listas não ordenadas são renderizadas no HTML:

- Gatsby
  - docs

* Gatsby
  - docs

- Gatsby
  - docs

### Ordenadas

- número e período para cada item da lista
- usando `1.` para cada item pode automaticamente ser incrementado dependendo do conteúdo

```markdown
1. Um
1. Dois
1. Três
```

1. Um
1. Dois
1. Três

## Links e imagens

### Link

Os Links em Markdown utilizam este formato. URLs podem ser relativas ou remotas:

```markdown
[Texto](url)
```

Exemplo de um Link renderizado no HTML:

[Site do Gatsby](https://www.gatsbyjs.org/)

### Imagem com texto alternativo

```markdown
![texto alternativo](caminho-da-imagem)
```

### Imagem sem texto alternativo

Este padrão é apropriado para [imagens decorativas ou repetitivas](https://www.w3.org/WAI/tutorials/images/decision-tree/):

```markdown
![](caminho-da-imagem)
```

## Bloco de citação

- Use `>` para declarar um bloco de citação
- Adicione múltiplos `>` para criar blocos de citações aninhados
- É recomendado colocar `>` antes de cada linha
- Você pode usar outra sintaxe Markdown dentro de um bloco de citação

```markdown
> bloco de citação
>
> > bloco de citação aninhado
>
> > **Sou negrito!**
>
> mais citações
```

> bloco de citação
>
> > bloco de citação aninhado
>
> > **Sou negrito!**
>
> mais citações

## Comentários de código

### Em linha

- Coloque o texto entre barras invertidas \`code\`
- `código` em linha se parece com esta frase

### Blocos de código

- Idente o bloco com quatro espaços

## MD vs MDX

- MDX é um superconjunto do Markdown. Ele permite você escrever JSX dentro de um arquivo markdown. Com isso é possível importar e renderizar componentes React!

## Processando Markdown e MDX no Gatsby:

- Para processar e usar Markdown ou MDX no Gatsby, você pode usar o plugin [gatsby-source-filesystem](/docs/sourcing-from-the-filesystem)
- Você pode obter maiores informações e como funciona o plugin no [README](/packages/gatsby-source-filesystem)


## Frontmatter

- Metadados para seu Markdown
- Variáveis que podem ser injetadas mais tarde nos seus componentes
- Deve ser:
  - No topo do arquivo
  - YAML válido
  - Entre linhas tracejadas triplas
  ```
  ---
  titulo: Meu título do Frontmatter
  exemplo_de_um_booleano: true
  ---
  ```

## Exemplo de Frontmatter + MDX

```mdx
---
descricao: Um simples exemplo de descrição no Frontmatter
---

import { Chart } from "../components/chart"

# Aqui está um gráfico

O gráfico é renderizado no seu documento MDX.

<Chart descricao={descricao} />
```

## Links úteis

- https://daringfireball.net/projects/markdown/syntax
- https://www.markdownguide.org/basic-syntax
