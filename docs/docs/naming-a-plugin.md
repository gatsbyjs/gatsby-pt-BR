---
Titulo: Nomeando um Plugin
---

## Padrões de nomes para plugins

No Gatsby existem quatro padrões de nomes para plugins:

- **`gatsby-source-*`** — um plugin do tipo origem, carrga dados de uma determinada fonte (por exemplo, WordPress, MongoDB, o sistema de arquivos). Utilize este tipo de plugin se estiver conectando uma nova fonte de dados ao Gatsby.
  - Exemplo: [`gatsby-source-contentful`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-source-contentful)
  - Documentação: [criando um plugin de oringem](/docs/creating-a-source-plugin/)
- **`gatsby-transformer-*`** — um plugin transformador é capaz de converter dados de um dos formatos (por exemplo, CSV, YAML) em um objeto JavaScript. Utilize este padrão de nome se seu plugin converte dados de um formato para outro.
  - Exemplo: [`gatsby-transformer-yaml`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-yaml)
  - Documentação: [criando um plugin transformador](/docs/creating-a-transformer-plugin/)
- **`gatsby-[plugin-name]-*`** — se o plugin for um plugin para outro plugin 😅, ele deve ser prefixado com o nome do plugin o qual ele estende (por exemplo, se o plugin adiciona emojis para a saida do `gatsby-transformer-remark`, chame-o de `gatsby-remark-add-emoji`).   Utilize este padrão de nome quando seu plugin for incluido nos objetos `options` de outro plugin.
  - Exemplo: [`gatsby-remark-images`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-remark-images)
- **`gatsby-theme-*`** — este padrão de nome deve ser usado para [Gatsby themes](/docs/themes/), os quais são um tipo de plugin.
- **`gatsby-plugin-*`** — este é o tipo de plugin mais geral. Utilize este padrão de nome se o seu plugin não se encaixa em nenhum dos requerimentos dos plugins anteriomente citados.
  - Exemplo: [`gatsby-plugin-sharp`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-sharp)
