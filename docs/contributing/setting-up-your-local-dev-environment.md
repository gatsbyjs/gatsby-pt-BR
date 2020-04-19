---
title: Configurando o seu ambiente local de desenvolvimento
---

Esta página descreve como se preparar para contribuir com o núcleo do Gatsby e o seu ecossistema. Para instruções de como trabalhar com documentação, visite a página de [contribuições para as documentações](/contributing/docs-contributions/). Para instruções de configuração do blog e site, visite a página de [contribuições ao blog & site](/contributing/blog-and-website-contributions/).

> O Gatsby usa um padrão chamado "monorepo" para gerenciar suas muitas dependências e depende do
> [Lerna](https://lerna.js.org/) e [Yarn](https://yarnpkg.com/en/) para configurar o repositório tanto para atividades de desenvolvimento quanto para alterações da infraestrutura de documentação

## Usando o Yarn

Yarn é um gerenciador de pacotes para o seu código, parecido com o [NPM](https://www.npmjs.com/). Enquanto o NPM é usado para desenvolver sites Gatsby com a ILC, para contribuir com o repositório do Gatsby o Yarn é necessário pelo seguinte motivo: nós usamos uma função do Yarn chamada [workspaces](https://yarnpkg.com/lang/en/docs/workspaces/) que é bem útil com monorepos. Ela permite que instalemos dependências de múltiplos arquivos `package.json` em sub-diretórios, tornando o processo de instalação mais rápido e leve.

```json:title=package.json
{
  "workspaces": ["workspace-a", "workspace-b"]
}
```

## Instruções de instalação do repositório do Gatsby
<!-- 
### Install Node and Yarn

- Ensure you have the latest **LTS** version of Node installed (>= 10.16.0). `node --version`
- [Install](https://yarnpkg.com/en/docs/install) the Yarn package manager.
- Ensure you have the latest version of Yarn installed (>= 1.0.2). `yarn --version`

### Fork, clone, and branch the repository

- [Fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) the [official `gatsbyjs/gatsby` repository](https://github.com/gatsbyjs/gatsby).
- Clone your fork: `git clone --depth=1 https://github.com/<your-username>/gatsby.git`
- Set up repo and install dependencies: `yarn run bootstrap`
- Make sure tests are passing for you: `yarn test`
- Create a topic branch: `git checkout -b topics/new-feature-name`

### Docs only changes

- See [docs setup instructions](/contributing/docs-contributions#docs-site-setup-instructions) for docs-only changes.
- Run `yarn run watch` from the root of the repo to watch for changes to packages' source code and compile these changes on-the-fly as you work.

  - Note that the watch command can be resource intensive. To limit it to the packages you're working on, add a scope flag, like `yarn run watch --scope={gatsby,gatsby-cli}`.
  - To watch just one package, run `yarn run watch --scope=gatsby`.

### Gatsby functional changes

- Install [gatsby-cli](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli):
  - Make sure you have the Gatsby CLI installed with `gatsby -v`,
  - if not, install globally: `yarn global add gatsby-cli`
- Install [gatsby-dev-cli](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-dev-cli):
  - Make sure you have the Gatsby Dev CLI installed with `gatsby-dev -v`
  - if not, install globally: `yarn global add gatsby-dev-cli`
- Run `yarn install` in each of the sites you're testing.
- For each of your Gatsby test sites, run the `gatsby-dev` command inside the test site's directory to copy
  the built files from your cloned copy of Gatsby. It'll watch for your changes
  to Gatsby packages and copy them into the site. For more detailed instructions
  see the [gatsby-dev-cli README](https://www.npmjs.com/package/gatsby-dev-cli) and check out the [gatsby-dev-cli demo video](https://www.youtube.com/watch?v=D0SwX1MSuas).

  - Note: if you plan to modify packages that are exported from `gatsby` directly, you need to either add those manually to your test sites so that they are listed in `package.json` (e.g. `yarn add gatsby-link`), or specify them explicitly with `gatsby-dev --packages gatsby-link`).

### Add tests

- Add tests and code for your changes.
- Once you're done, make sure all tests still pass: `yarn test`.

  - To run tests for a single package you can run: `yarn jest <package-name>`.
  - To run a single test file you can run: `yarn jest <file-path>`.

### Commits and pull requests

- Commit and push to your fork.
- Create a pull request from your branch.

### Sync your fork

- GitHub Help Page [Syncing a fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
- GitHub Help Page [Merging an upstream repository into your fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/merging-an-upstream-repository-into-your-fork) -->
