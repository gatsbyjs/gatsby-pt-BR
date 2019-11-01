---
title: Como Abrir uma Pull Request
---

Uma boa parte de contribuição para _open source_ consiste em enviar alterações para um projeto: melhorias no código-fonte ou nos testes, atualizações no conteúdo da documentação, ou até mesmo erros de digitação ou links quebrados. Este documento abordará o que você precisa saber para **abrir uma pull request** no Gatsby.

## O que é uma Pull Request (PR)?

Caso você não esteja familiarizado, veja como o pessoal do GitHub [define uma pull request](https://help.github.com/pt/articles/about-pull-requests):

> As pull requests permitem que você informe outras pessoas sobre as alterações das quais você fez push para um branch em um repositório no GitHub. Depois que uma pull request é aberta, você pode discutir e revisar as possíveis alterações com colaboradores e adicionar commits de acompanhamento antes que as alterações sofram merge no branch base.

Gatsby usa o processo de PR para revisar e testar as alterações antes de serem adicionadas ao repositório do Gatsby no GitHub. Qualquer pessoa pode abrir uma pull request. O mesmo processo é usado para todos os contribuidores, seja esta a sua primeira contribuição open source ou seja você um membro da equipe core do Gatsby.

Quando alguém desejar contribuir com o Gatsby, essa pessoa abre uma solicitação para inserir (_pull_) seu código no repositório. Dependendo do tipo de alteração, os PRs são categorizados em:

- [Documentação](#documentation)
- [Código](#code-changes)
- [Starters or Site Showcase](#starters-or-site-showcase)
- [Blog posts](#blog-posts)

Recomendações para diferentes tipos de contribuições seguirão neste guia e ao longo das documentações de contribuição.

## O que você deve saber antes de abrir uma PR

Normalmente recomendamos [abrir uma issue](/contributing/how-to-file-an-issue/) antes de uma pull request, se ainda não houver uma issue para o problema que você deseja resolver. Isso ajuda a facilitar uma discussão antes de decidir sobre uma implementação.

Para algumas alterações, como correções de erros de digitação ou links quebrados, pode ser apropriado abrir um pequeno PR por si só. Isso é um pouco subjetivo, portanto, se você tiver alguma dúvida, [não hesite em perguntar-nos](/contributing/how-to-contribute/#not-sure-how-to-start-contributing).

A equipe core do Gatsby usa um processo de triagem descrito em [Gerenciando Pull Requests](/contributing/managing-pull-requests/), se você estiver interessado em aprender mais sobre como isso funciona.

## Abrindo PRs no Gatsby

Para qualquer tipo de alteração nos arquivos no repositório do Gatsby, você pode seguir as etapas abaixo. Certifique-se de verificar as dicas adicionais para contribuir para várias partes do repo mais adiante neste documento, como mudanças nas docs, blog posts, starters, ou melhorias de código e testes.

Alguns PRs podem ser feitos completamente a partir do [GitHub UI](https://help.github.com/pt/articles/creating-a-pull-request), como edições em arquivos README ou documentações.

Para testar alterações localmente no [site e arquivos do projeto](https://github.com/gatsbyjs/gatsby) do Gatsby, você pode fazer um fork do repositório e instalar partes dele para executar na sua máquina local.

- [Crie um fork e clone o repositório Gatsby](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions).
- Instale o [yarn](https://yarnpkg.com/pt-BR/) para obter dependências e criar o projeto.
- Siga as instruções para a parte do projeto que você deseja alterar. (Veja seções específicas abaixo.)
- [Crie uma branch no Git](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) para isolar suas alterações:

  ```shell
  git checkout -b some-change
  ```

* Assim que tiver alterações no Git que você deseje enviar, [adicione-os e crie um commit](https://help.github.com/pt/articles/adding-a-file-to-a-repository-using-the-command-line). Para obter informações sobre como estruturar seus commits, consulte a documentação [Gerenciando PRs](/contributing/managing-pull-requests/#commit-and-pr-title).
  - Usando um caractere de ponto `.` adicionará todos os arquivos não rastreados no diretório e subdiretórios atuais.
  ```shell
  git add .
  ```
  - Usando uma ferramenta visual como [GitHub Desktop](https://desktop.github.com/) ou [GitX](https://rowanj.github.io/gitx/) pode ajudar a escolher quais arquivos e linhas commitar.
* Commitando código executará o linter automatizado usando o [Prettier](https://prettier.io). Para executar o linter manualmente, execute um script npm no diretório base do projeto:
  ```shell
  npm run format
  ```
* Crie um commit com as alterações de linting antes de enviar por push, [alterando o commit anterior](https://help.github.com/pt/articles/changing-a-commit-message) ou adicionando um novo commit. Para mais informações sobre linting e testes, visite a documentação [Gerenciando PRs](/contributing/managing-pull-requests/#automated-checks).
  ```shell
  git commit --amend
  ```
- Envie suas alterações para seu fork, assumindo que ele esteja configurado como [`origin`](https://www.git-tower.com/learn/git/glossary/origin):
  ```shell
  git push origin head
  ```
- Para abrir uma PR com suas alterações no repositório Gatsby, você pode usar o [GitHub Pull Request UI](https://help.github.com/pt/articles/creating-a-pull-request). Como alternativa, você pode usar a linha de comando: recomendamos [hub](https://github.com/github/hub) para isso.

### Documentação de PRs

O site da documentação do Gatsby.js está principalmente nos diretórios [www](https://github.com/gatsbyjs/gatsby/tree/master/www) e [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs) no GitHub, incluindo documentações e conteúdos de tutoriais. Também existem alguns [exemplos no repositório Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/examples) mencionado na documentação.

Passos adicionais para documentar PR:

- Para alteraçÕes docs-only, considere usar `git checkout -b docs/some-change` ou `git checkout -b docs-some-change`, pois isso irá encurtar o circuito do processo de CI e executar apenas as tarefas de linting.

Mais instruções podem ser encontradas na página de [contribuições de documentações](/contributing/docs-contributions/).

### Alterações de código

Instruções para fazer alterações no código-fonte do Gatsby, testes, componentes internos, APIs, pacotes e muito mais podem ser encontradas nas documentações de contribuições sobre [configurando seu ambiente de desenvolvimento local](/contributing/setting-up-your-local-dev-environment/). Também há detalhes adicionais na página [Contribuições de código](/contributing/code-contributions/).

### Starters ou Site Showcase

Existem páginas específicas sobre como contribuir para várias partes do ecossistema de Gatsby:

- [Submissões ao Showcase](/contributing/site-showcase-submissions/)
- [Biblioteca Starter](/contributing/submit-to-starter-library/)

### Blog posts

Para o blog do Gatsby, é necessário executar sua ideia de conteúdo pela equipe do Gatsby antes de enviá-la. Para obter mais informações, consulte a página de [contribuições de blog e site](/contributing/blog-and-website-contributions/), incluindo como propor uma idéia e configurar o blog para ser executado localmente.

## Atualize seu fork com as alterações mais recentes do Gatsby

O repositório do Gatsby GitHub é muito ativo, portanto, é provável que você precise atualizar seu fork com as alterações mais recentes para poder mergir no seu código. Isso requer adicionar o Gatsby como um [upstream remote](https://help.github.com/pt/articles/configuring-a-remote-for-a-fork):

- Defina a URL do repositório do Gatsby como uma fonte remota. O nome do remoto é arbitrário; este exemplo usa `upstream`.
  ```shell
  git remote add upstream git@github.com:gatsbyjs/gatsby.git
  ```
  - _Nota: esta sintaxe [usa SSH e chaves: você também pode usar `https`](https://help.github.com/pt/articles/which-remote-url-should-i-use) e seu usuário/senha._
- Você pode verificar o nome e a URL remotos a qualquer momento:
  ```shell
  git remote -v
  ```
- Obtenha as alterações mais recentes do Gatsby:
  ```shell
  git fetch upstream master
  ```
- [Na branch](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) que você deseja atualizar, faça merge de todas as alterações do Gatsby no seu fork:
  ```shell
  git merge upstream/master
  ```
  - Se houver alguns [conflitos de mesclagem](https://help.github.com/pt/articles/resolving-a-merge-conflict-on-github), você vai querer resolver-los para obter um merge limpo.
- Quando sua branch estiver funcionando em boas condições, faça push das alterações para o seu fork:
  ```shell
  git push origin head
  ```

Para mais informações sobre como trabalhar com repositórios upstream, [visite a documentação do GitHub](https://help.github.com/pt/articles/configuring-a-remote-for-a-fork).

_**Nota:** como membro do repositório Gatsby, você também pode cloná-lo diretamente (em vez de fazer um fork e usar um fluxo de trabalho remoto upstream). Você pode então enviar via push as alterações para [feature branches](https://git-scm.com/book/en/v1/Git-Branching-Branching-Workflows) para abrir PRs._

## Recursos adicionais

- CSS Tricks: [How to Contribute to an Open Source Project](https://css-tricks.com/how-to-contribute-to-an-open-source-project/)
- [Criar uma pull request](https://help.github.com/pt/articles/creating-a-pull-request) do GitHub
- [Configurar remote para bifurcação](https://help.github.com/pt/articles/configuring-a-remote-for-a-fork)
- [Qual URL remote eu devo usar?](https://help.github.com/pt/articles/which-remote-url-should-i-use)
- [Git Branching and Merging](https://git-scm.com/book/pt-br/v2/Git-Branching-Basic-Branching-and-Merging)
- [Feature Branching and Workflows](https://git-scm.com/book/en/v1/Git-Branching-Branching-Workflows)
- [Resolver um conflito de merge no GitHub](https://help.github.com/pt/articles/resolving-a-merge-conflict-on-github)
- [Gerenciando Pull Requests](/contributing/managing-pull-requests/) na equipe core do Gatsby
- [Guia sobre sintaxe de Markdown](/docs/mdx/markdown-syntax/)
