---
Titulo: Nomeando um Plugin
---

## Padrões de nomes para plugins

<<<<<<< HEAD
No Gatsby existem quatro padrões de nomes para plugins:

- **`gatsby-source-*`** — um plugin do tipo origem, carrega dados de uma determinada fonte (por exemplo, WordPress, MongoDB, o sistema de arquivos). Utilize este tipo de plugin se estiver conectando uma nova fonte de dados ao Gatsby.
  - Exemplo: [`gatsby-source-contentful`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-source-contentful)
  - Documentação: [criando um plugin de origem](/docs/creating-a-source-plugin/)
- **`gatsby-transformer-*`** — um plugin transformador converte dados de um dos formatos (por exemplo, CSV, YAML) em um objeto JavaScript. Utilize este padrão de nome se seu plugin converte dados de um formato para outro.
  - Exemplo: [`gatsby-transformer-yaml`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-yaml)
  - Documentação: [criando um plugin transformador](/docs/creating-a-transformer-plugin/)
- **`gatsby-[plugin-name]-*`** — se o plugin for um plugin para outro plugin 😅, ele deve ser prefixado com o nome do plugin o qual ele estende (por exemplo, se o plugin adiciona emojis para a saida do `gatsby-transformer-remark`, chame-o de `gatsby-remark-add-emoji`).   Utilize este padrão de nome sempre que seu plugin for incluído nos objetos `options` de outro plugin.
  - Exemplo: [`gatsby-remark-images`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-remark-images)
- **`gatsby-theme-*`** — este padrão de nome deve ser usado para [temas Gatsby](/docs/themes/), os quais são um tipo de plugin.
- **`gatsby-plugin-*`** — este é o tipo mais geral de plugin. Utilize este padrão de nome se o seu plugin não se encaixa em nenhum dos requerimentos dos plugins anteriormente citados.
  - Exemplo: [`gatsby-plugin-sharp`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-sharp)
=======
There are five standard plugin naming conventions for Gatsby:

- **`gatsby-source-*`** — a source plugin loads data from a given source (e.g. WordPress, MongoDB, the file system). Use this plugin type if you are connecting a new source of data to Gatsby.
  - Example: [`gatsby-source-contentful`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-source-contentful)
  - Docs: [creating a source plugin](/docs/creating-a-source-plugin/)
- **`gatsby-transformer-*`** — a transformer plugin converts data from one format (e.g. CSV, YAML) to a JavaScript object. Use this naming convention if your plugin will be transforming data from one format to another.
  - Example: [`gatsby-transformer-yaml`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-yaml)
  - Docs: [creating a transformer plugin](/docs/creating-a-transformer-plugin/)
- **`gatsby-[plugin-name]-*`** — if a plugin is a plugin for another plugin 😅, it should be prefixed with the name of the plugin it extends (e.g. if it adds emoji to the output of `gatsby-transformer-remark`, call it `gatsby-remark-add-emoji`). Use this naming convention whenever your plugin will be included as a plugin in the `options` object of another plugin.
  - Example: [`gatsby-remark-images`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-remark-images)
  - Docs: [creating a remark plugin](/docs/remark-plugin-tutorial/)
- **`gatsby-theme-*`** — this naming convention **must** be used for [Gatsby themes](/docs/themes/), which are a type of plugin. Without following this naming convention, the plugin will not be recognized as a theme and it will not be able to utilize the powerful [shadowing](/docs/themes/shadowing/) feature of themes.
  - Example: [`gatsby-theme-blog`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-theme-blog)
  - Docs: [creating a theme](/tutorial/building-a-theme/)
- **`gatsby-plugin-*`** — this is the most general plugin type. Use this naming convention if your plugin doesn’t meet the requirements of any other plugin types.
  - Example: [`gatsby-plugin-sharp`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-sharp)
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f
