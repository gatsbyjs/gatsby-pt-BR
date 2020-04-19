---
Titulo: Nomeando um Plugin
---

## Padrões de nomes para plugins

No Gatsby existem cinco padrões de nomes para plugins:

- **`gatsby-source-*`** — um plugin do tipo origem, carrega dados de uma determinada fonte (por exemplo, WordPress, MongoDB, o sistema de arquivos). Utilize este tipo de plugin se estiver conectando uma nova fonte de dados ao Gatsby.
  - Exemplo: [`gatsby-source-contentful`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-source-contentful)
  - Documentação: [criando um plugin de origem](/docs/creating-a-source-plugin/)
- **`gatsby-transformer-*`** — um plugin transformador converte dados de um dos formatos (por exemplo, CSV, YAML) em um objeto JavaScript. Utilize este padrão de nome se seu plugin converte dados de um formato para outro.
  - Exemplo: [`gatsby-transformer-yaml`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-yaml)
  - Documentação: [criando um plugin transformador](/docs/creating-a-transformer-plugin/)
- **`gatsby-[plugin-name]-*`** — se o plugin for um plugin para outro plugin 😅, ele deve ser prefixado com o nome do plugin o qual ele estende (por exemplo, se o plugin adiciona emojis para a saida do `gatsby-transformer-remark`, chame-o de `gatsby-remark-add-emoji`).   Utilize este padrão de nome sempre que seu plugin for incluído nos objetos `options` de outro plugin.
  - Exemplo: [`gatsby-remark-images`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-remark-images)
- **`gatsby-theme-*`** — Esse padrão de nome é usado para [temas Gatsby](/docs/themes/), que são um tipo de plugin. Esse padrão é usado para plugins que possuem uma seção, uma página, ou parte de uma página de um site ou que expôem arquivos ou componentes para [shadowing](/docs/themes/shadowing/).
  - Example: [`gatsby-theme-blog`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-theme-blog)
  - Docs: [creating a theme](/tutorial/building-a-theme/)
- **`gatsby-plugin-*`** — este é o tipo mais geral de plugin. Utilize este padrão de nome se o seu plugin não se encaixa em nenhum dos requerimentos dos plugins anteriormente citados.
  - Exemplo: [`gatsby-plugin-sharp`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-sharp)
