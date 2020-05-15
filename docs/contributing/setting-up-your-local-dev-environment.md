---
title: Configurando o seu ambiente local de desenvolvimento
---

Esta página descreve como se preparar para contribuir com o núcleo do Gatsby e o seu ecossistema. Para instruções de como trabalhar com documentação, visite a página de [contribuições para as documentações](/contributing/docs-contributions/). Para instruções de configuração do blog e site, visite a página de [contribuições ao blog & site](/contributing/blog-and-website-contributions/).

> O Gatsby usa um padrão chamado "monorepo" para gerenciar suas muitas dependências e depende do
> [Lerna](https://lerna.js.org/) e [Yarn](https://yarnpkg.com/en/) para configurar o repositório tanto para atividades de desenvolvimento quanto para alterações da infraestrutura de documentação

## Usando o Yarn

Yarn é um gerenciador de pacotes para o seu código, parecido com o [NPM](https://www.npmjs.com/). Enquanto o NPM é usado para desenvolver sites Gatsby com a CLI, para contribuir com o repositório do Gatsby o Yarn é necessário pelo seguinte motivo: nós usamos uma função do Yarn chamada [workspaces](https://classic.yarnpkg.com/pt-BR/docs/workspaces) que é bem útil com monorepos. Ela permite que instalemos dependências de múltiplos arquivos `package.json` em sub-diretórios, tornando o processo de instalação mais rápido e leve.

```json:title=package.json
{
  "workspaces": ["workspace-a", "workspace-b"]
}
```

## Instruções de instalação do repositório do Gatsby

### Instale o Node e Yarn  

- Garanta que possui a última versão estável do Node instalada **LTS** (>= 10.16.0). `node --version`
- [Instale](https://yarnpkg.com/en/docs/install) o gerenciador de pacotes Yarn.
- Garanta que possui a última versão do Yarn instalada (>= 1.0.2). `yarn --version`

### Faça o fork, clone, e crie uma branch no seu repositório

- [Fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) o [repositório oficial `gatsbyjs/gatsby` repository](https://github.com/gatsbyjs/gatsby).
- Clone seu fork: `git clone --depth=1 https://github.com/<seu-username>/gatsby.git`
- Configure o repositório e instale as dependências: `yarn run bootstrap`
- Garanta que os testes estão pasasndo: `yarn test`
- Crie uma nova branch de tópico: `git checkout -b topics/new-feature-name`

### Alterações somente em documentação

- Veja [as instruções de configuração de docs](/contributing/docs-contributions#docs-site-setup-instructions) para alterações apenas em documentações.
- Execute `yarn run watch` na raiz do repositório para observar alterações no código do pacote e compilar em tempo real.

  - O comando watch pode usar recursos da máquina intensamente. Para limitar em quais pacotes está trabalhando, adicione o escopo como parâmetro, assim: `yarn run watch --scope={gatsby,gatsby-cli}`.
  - Para observar apenas um pacote, execute `yarn run watch --scope=gatsby`.

### Alterações de funcionalidades do Gatsby

- Instale [gatsby-cli](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli):
  - Garanta que você tem a Gatsby CLI instalada com `gatsby -v`,
  - senão, instale globalmente: `yarn global add gatsby-cli`
- Instale [gatsby-dev-cli](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-dev-cli):
  - Garante que você tem a Gatsby Dev CLI instalada com `gatsby-dev -v`
  - senão, instale globalmente: `yarn global add gatsby-dev-cli`
- Execute `yarn install` em cada site que você está testando.
- Para cada um dos seus sites de teste Gatsby, execute o comando `gatsby-dev` dentro do diretório do site para copiar os arquivos gerados do seu repositório Gatsby que foi clonado. Ele irá observar as alterações nos pacotes Gatsby e copiá-las para o site. Para informações mais detalhadas veja [o README do gatsby-dev-cli](https://www.npmjs.com/package/gatsby-dev-cli) e confira o [vídeo demo do gatsby-dev-cli](https://www.youtube.com/watch?v=D0SwX1MSuas).

  - Nota: se você pretende modificar pacotes que são exportados diretamente do `gatsby`, você precisa adicioná-los manualmente ao seu site de teste para que eles estejam listados no `package.json` (exemplo: `yarn add gatsby-link`), ou especificá-los explicitamente com `gatsby-dev --packages gatsby-link`).

### Adicione testes

- Adicione os testes e o código para suas alterações.
- Uma vez que tenha terminado, garanta que os testes continuam passando: `yarn test`.

  - Para rodar testes para um pacote específico: `yarn jest <package-name>`.
  - Para rodar um arquivo específico de teste: `yarn jest <file-path>`.

### Commits e pull requests

- Faça commit e suba as alterações para o seu fork.
- Crie um pull request da sua branch.

### Sincronizando seu fork

- Página de ajuda do GitHub [Sincronizando um fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
- Página de ajuda do GitHub [Fazendo merge de um repositório upstream para o seu fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/merging-an-upstream-repository-into-your-fork)
