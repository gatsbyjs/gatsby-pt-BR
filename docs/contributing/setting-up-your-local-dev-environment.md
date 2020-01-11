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

- Certifique-se de ter a última versão **LTS** do Node instalada (>= 10.16.0). `node --version`
- [Instale](https://yarnpkg.com/en/docs/install) o gerenciador de pacotes Yarn.
- Certifique-se de ter a última versão do Yarn instalada (>= 1.0.2). `yarn --version`
- Faça um fork do [repositório oficial do Gastby](https://github.com/gatsbyjs/gatsby).
- Clone o seu fork: `git clone --depth=1 https://github.com/<seu-username>/gatsby.git`
- Configure o repositório e instale as dependências: `yarn run bootstrap`
- Certifique-se de que os testes estão passando para você: `yarn test`
- Crie um branch com um nome bem descritivo: `git checkout -b topics/new-feature-name`
- Veja as [instruções para configurar a documentação do Gatsby](/contributing/docs-contributions#instruções-para-configurar-a-documentação-do-Gatsby) para alterações apenas na documentação.
- Execute `yarn run watch` a partir da raiz do seu repositório para observar mudanças no código fonte dos pacotes e compilar estas mudanças automaticamente conforme você trabalha.
  - Note que o comando watch pode consumir bastante recursos. Para limitá-lo aos pacotes que você está trabalhando, adicione um argumento scope, como `yarn run watch --scope={gatsby,gatsby-cli}`.
  - Para observar apenas um pacote, execute `yarn run watch --scope=gatsby`.
- Instale o [gatsby-dev-cli](https://www.npmjs.com/package/gatsby-dev-cli) globalmente: `yarn global add gatsby-dev-cli`
- Execute `yarn install` em cada um dos sites que você estiver testando.
- Para cada um dos seus sites Gatsby, execute o comando `gatsby-dev` dentro do diretório do site de teste para copiar
  os arquivos compilados da sua cópia clonada do Gatsby. Ele irá observar suas mudanças
  nos pacotes do Gatsby e copiá-los para seu site. Para instruções mais detalhadas,
  veja o [README do gatsby-dev-cli](https://www.npmjs.com/package/gatsby-dev-cli) e confira o [vídeo de demonstração do gatsby-dev-cli](https://www.youtube.com/watch?v=D0SwX1MSuas).
  - Nota: se você planeja modificar os pacotes que são exportados do `gatsby` diretamente, você precisa ou adicioná-los manualmente aos seus sites de teste para que eles sejam listados no `package.json` (ex. `yarn add gatsby-link`), ou especificá-los explicitamente com `gatsby-dev --packages gatsby-link`).
- Adicione testes e código para as suas alterações.
- Assim que você terminar, certifique-se de que todos os testes continuam passando: `yarn test`.
  - Para rodar os testes de um único pacote, você pode executar: `yarn jest <nome-do-pacote>`.
  - Para rodar um único arquivo de teste, você pode executar: `yarn jest <caminho-do-arquivo>`.
- Faça o commit e push do seu código para o seu fork.
- Crie um pull request do seu branch.
