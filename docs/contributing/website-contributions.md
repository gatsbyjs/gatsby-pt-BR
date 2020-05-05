---
title: Contribuições para o site
---

Se você quer fazer mudanças, melhorias ou adicionar alguma funcionalidade no site, não é preciso configurar o repositório completo do Gatsby para contribuir. Você pode subir sua própria instância do site do Gatsby seguindo esses passos:

- Clone [o repositório do Gatsby](https://github.com/gatsbyjs/gatsby/) e navegue até a pasta `/www`
- Execute o comando `yarn` para instalar todas as dependências do site.
- Execute o comando `npm run develop` para visualizar o site no endereço `http://localhost:8000/`.

> Nota: Se você tiver problemas para executar o site em uma máquina Linux, execute o comando `sudo apt install libvips-dev`, para instalar uma dependência nativa. Você também pode consultar [o guia do Gatsby no Linux](/docs/gatsby-on-linux/), para ver outros requisitos específicos desta plataforma.

Agora você pode fazer e visualizar suas mudanças antes de mandar um pull request!

Para instruções sobre a configuração completa do repositório, veja a página [contribuições de código](/contributing/code-contributions/)

## Estilizando componentes no Gatsbyjs.org com Theme-UI

A estilização do site é feita usando [Theme-UI](https://theme-ui.com/), que nos permite aplicar temas baseados em design tokens (variáveis).

### Design tokens

Design tokens são usados para consolidar o número de cores e atributos de estilos, que são aplicados nos componentes através do site. Limitando os estilos que podem ser aplicados, o site se mantém consistente com as diretrizes de cores, tipografia, espaçamento, etc.

Tabelas com a lista de design tokens usados no site podem ser encontradas nas [diretrizes de design](/guidelines/design-tokens/).

### A propriedade `sx`

A [propriedade `sx`](https://theme-ui.com/sx-prop) do Theme-UI te permite acessar os valores do tema para estilizar elementos e componentes, ela deve ser usada sempre que possível. A propriedade é "habilitada" ao adicionar a [diretiva de compilação JSX](https://theme-ui.com/jsx-pragma) no topo de um arquivo `js`.

Você pode importar os tokens diretamente do arquivo [`www/src/gatsby-plugin-theme-ui`](https://github.com/gatsbyjs/gatsby/blob/master/www/src/gatsby-plugin-theme-ui/index.js), como `mediaQueries` ou `colors`, se isso ajudar em um cenário específico - por exemplo ao precisar de uma varíavel CSS global, ao precisar passar os valores do tema para outras bibliotecas ou plugins, ao criar estilos responsivos complexos, etc.