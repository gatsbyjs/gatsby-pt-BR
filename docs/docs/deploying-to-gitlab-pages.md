---
title: Publicando no GitLab Pages
---

GitLab Pages é muito semelhante ao Github Pages. GitLab Pages dá suporte a domínios customizados, certificados SSL, como também inclui uma plataforma de integração contínua.

Crie um novo repositório no GitLab, [crie um novo site Gatsby](/docs/) se ainda não fez e adicione o GitLab como seu remoto.

```shell
git init
git remote add origin git@gitlab.com:examplerepository
git add .
git push -u origin master
```

Você pode publicar sites no GitLab Pages com ou sem um domínio customizado. Se você escolher a configuração padrão (sem um domínio customizado), ou se você criar um site para um projeto, você precisará configurar um prefixo para a rota do seu site. Se você adicionar um domínio customizado, você pode pular o passo de adicionar o prefixo na rota, e remover `--prefix-paths` do arquivo `gitlab-ci.yml`

## Adicione Prefixo a Rota no Gatsby

Como seu site irá ser hospedado em seunome.gitlab.io/repositorioexemplo/, você irá precisar configurar para o Gatsby para que use o plugin Path Prefix.

Em `gatsby-config.js`, coloque o `pathPrefix` para ser o prefixo que será adicionado aos links das rotas do seu site. O `pathPrefix` deve ser o nome do projeto em seu repositório. (ex. `https://gitlab.com/seunome/repositorioexemplo/`) - seu `pathPrefix` deve ser `/repositorioexemplo`. Veja a [documentação de prefixação de rota para mais detalhes](/docs/path-prefix/).

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/repositorioexemplo`,
}
```

## Faça o build e publique com GitLab CI

Para usar a ferramenta de integração contínua (CI) do GitLab, você precisa adicionar o arquivo de configuração `.gitlab-ci.yml`. Este é o arquivo que o GitLab usa para gerenciar as tarefas do CI.

O editor online no site do [GitLab](https://gitlab.com) contém um exemplo pré-built com um template pronto para ser usado no Gatsby.

Para usar o template, abra seu repositório no site do GitLab, selecione a opção 'Setup CI/CD' no menu, após isso será criado um arquivo `.gitlab-ci.yml` vazio automaticamente. Agora selecione o 'Apply a template' e digite 'Gatsby' no filtro. Selecione o Gatsby como opção, clique para 'Commit Change' e está feito!

Caso você opte por adicionar manualmente o template no seu projeto, o arquivo `.gitlab-ci.yml` precisa conter alguns campos obrigatórios:

```yaml:title=.gitlab-ci.yml
image: node:latest

# Essa pasta é armazenada em cache entre as builds
# http://docs.gitlab.com/ce/ci/yaml/README.html#cache
cache:
  paths:
    - node_modules/

pages:
  script:
    - npm install
    - ./node_modules/.bin/gatsby build --prefix-paths
  artifacts:
    paths:
      - public
  only:
    - master
```

A plataforma de CI usa Docker images/containers, então `image node:latest` informa ao CI que deve usar a última imagem do node. `cache:` irá fazer o cache do `node_modules` antigo entre as builds, assim as próximas builds devem ser muito mais rápidas já que não precisam reinstalar todas as dependências. `pages:` é o nome do estágio do CI. Você pode ter múltiplos estágios, e.g. 'Test', 'Build', 'Deploy' etc. `script:` começa a próxima parte do estágio da CI, informando que deve começar a rodar os scripts descritos abaixo dele dentro da imagem que foi selecionada. `npm install` e `./node_modules/.bin/gatsby build --prefix-paths` irão instalar todas as dependências e iniciar o build do site estático, respectivamente.

Como `./node_modules/.bin/gatsby build --prefix-paths` foi usado, você não precisa instalar gatsby-cli para fazer o build da imagem, pois já foi incluído e instalado com `npm install`. `--prefix-paths` foi usando porque _sem_ essa flag, Gatsby ignora seu pathPrefix. `artifacts:` and `paths:` são usados para informar ao GitLab Pages onde os arquivos estáticos estão localizados. `only:` and `master` diz ao CI para apenas rodar estas instruções quando a branch master é publicada.

Adicione essa configução e no próximo push para a sua branch master, seu site terá feito o build corretamente. Isto pode ser checado no seu repositório do GitLab, selecionando em CI/CD na barra lateral. Será mostrado um log de todas as atividades que tiveram sucesso ou falharam. Você pode clicar no status de falha e selecionar a atividade para obter mais informações do porquê sua build falhou.

Se tudo ocorreu bem, você agora poderá acessar seu site. Ele será hospedado em gitlab.io - por exemplo se o seu repositório está associado a sua conta, a url será seunome.gitlab.io/repositorioexemplo.

Visite o [GitLab Pages](https://gitlab.com/help/user/project/pages/getting_started_part_one.md) para aprender como configurar domínios customizados e descobrir configurações avançadas.
