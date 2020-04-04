---
title: Como Gatsby Trabalha com GitHub Pages
---

GitHub Pages é um serviço oferecido pelo GitHub que permite a hospedagem de sites configurados diretamente do repositório. Um site feito em Gatsby pode ser hospedado no GitHub Pages com apenas algumas configurações na base de código e nas configurações do repositório.

Você pode publicar seu site no GitHub Pages de várias maneiras diferentes:

- para um caminho como `username.github.io/reponame/` ou `/docs`
- para um subdomínio com base no seu nome de usuário ou nome de organização: `username.github.io` ou `orgname.github.io`
- para o subdomínio raiz em `username.github.io`, e então configurar para usar um domínio personalizado

## Configurando a branch de origem do GitHub Pages

Você deve selecionar nas configurações do seu repositório qual branch será publicada no GitHub para que o GitHub Pages funcione. No GitHub:

1. Navegue até o repositório do seu site.

2. Abaixo do nome do repositório, clique em Configurações.

3. Na seção GitHub Pages, use o drop-down de Origem para selecionar master (para publicar no subdomínio raiz) ou gh-pages (para publicar em um caminho como `/docs`) como sua origem de publicação para o GitHub Pages.

4. Clique Salvar.

## Instalando o pacote `gh-pages`

A maneira mais fácil de publicar um site Gatsby para o GitHub Pages é usando um pacote chamado [gh-pages](https://github.com/tschaub/gh-pages).

```shell
npm install gh-pages --save-dev
```

## Usando um script de deploy

Um script personalizado em seu `package.json` torna mais fácil fazer o build do seu site e mover o conteúdo dos arquivos gerados para a branch apropriada para o GitHub Pages, isso ajuda a automatizar esse processo.

### Fazer deploy para um caminho no GitHub Pages

Para sites publicados em um caminho como `username.github.io/reponame`, uma flag `--prefix-paths` é usada porque seu site vai estar dentro de um diretório como `username.github.io/reponame/`. Você vai precisar adicionar seu `/reponame` [path prefix](/docs/path-prefix/) como uma opção no `gatsby-config.js`:


```js:title=gatsby-config.js
module.exports = {
  pathPrefix: "/reponame",
}
```

Então adicione um script `deploy` no `package.json` no código base do seu repositório:

```json:title=package.json
{
  "scripts": {
    "deploy": "gatsby build --prefix-paths && gh-pages -d public"
  }
}
```

Quando você executar `npm run deploy` todo conteúdo do diretório `public` será movido para a branch `gh-pages` do seu repositório. Certifique-se de que as configurações do seu repositório tenham a branch `gh-pages` configurada como origem de publicação.

**Nota**: para selecionar master ou gh-pages como sua origem de publicação, você precisa ter essa branch presente em seu repositório. Se você não tem uma branch master ou gh-pages, você pode criar elas e então retornar à configuração de Origem para alterar sua origem de publicação.

### Fazer deploy para um subdomínio GitHub Pages em github.io

Para um repositório com nome `username.github.io`, você não precisa especificar o `pathPrefix` e seu site precisa ser enviado para a branch `master`.

```json:title=package.json
{
  "scripts": {
    "deploy": "gatsby build && gh-pages -d public -b master"
  }
}
```

Depois de executar `npm run deploy` você deve ver seu site em `username.github.io`

### Fazer deploy para o subdomínio raiz e utilizar um domínio personalizado

Se você usa um [domínio personalizado](https://help.github.com/articles/using-a-custom-domain-with-github-pages/), não adicione o `pathPrefix` pois isso vai quebrar a navegação do seu site. Prefixo de caminho somente é necessário quando o site _não_ está na raiz do domínio, como nos sites de repositórios.

**Nota**: Não esqueça de adicionar seu arquivo [CNAME](https://help.github.com/articles/troubleshooting-custom-domains/#github-repository-setup-errors) ao diretório `static`.

### Fazer deploy para o GitHub Pages a partir de um servidor CI

Também é possível publicar seu site para `gh-pages` através de um servidor CI. Este exemplo usa Travis CI, um serviço hospedado de Integração Contínua, mas outros sistemas CI também podem funcionar.

Você pode usar o [módulo npm gh-pages](https://www.npmjs.com/package/gh-pages) para publicar. Mas primeiro, você precisa configurá-lo com as credenciais apropriadas para que `gh-pages` possa enviar uma nova branch.

#### Obter um token GitHub para autenticação no CI

Para fazer o push de mudanças a partir do sistema CI para o GitHub, você precisará autenticar. É recomendado usar [tokens do GitHub para desenvolvedores](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line).

No GitHub vá para as configurações de sua conta -> configurações de desenvolvedor -> tokens de acesso pessoal, e crie um novo token que forneça permissões de acesso ao `repo`.

Na [configuração do Travis para o repositório](https://docs.travis-ci.com/user/environment-variables/#defining-variables-in-repository-settings), adicione uma nova variável secreta de ambiente de nome `GH_TOKEN` com o valor do token copiado do GitHub. Certifique-se de **NÃO alterar a configuração "exibir nos logs de build" para ativada** pois o token deve permanecer secreto. Caso contrário, estranhos poderão fazer push para o seu repositório (um grande problema de segurança).

#### Adicionar um script de deploy ao GitHub Pages via CI

Atualizar o `package.json` do projeto Gatsby para incluir um script de execução `deploy` que chama `gh-pages` com dois argumentos importantes na linha de comando:

1. `-d public` - especifica o diretório no qual os arquivos gerados estão e que serão enviados como origem para o GitHub Pages
2. `-r URL` - a URL do repositório GitHub, incluindo o uso do token secreto do GitHub (como uma variável secreta de ambiente) para ser capaz de enviar mudanças para a branch `gh-pages`, na forma de `https://$GH_TOKEN@github.com/<github username>/<github repository name>.git`

Aqui está um exemplo (não esqueça de atualizar o nome de usuário e repositório):

```json
  "scripts": {
    "deploy": "gatsby build --prefix-paths && gh-pages -d public -r https://$GH_TOKEN@github.com/lirantal/dockly.git"
  }
```

#### Atualizar a configuração do .travis.yml

A seguinte configuração `.travis.yml` fornece uma referência:

```yaml
language: node_js
before_script:
  - npm install -g gatsby-cli
node_js:
  - "10"
deploy:
  provider: script
  # Nota: altere "docs" para o diretório onde está seu site Gatsby, se necessário`
  script: cd docs/ && yarn install && yarn run deploy
  skip_cleanup: true
  on:
  
    branch: master
```

Explicando aqui as partes importantes para publicação do site Gatsby a partir do Travis para o GitHub Pages:

1. `before_script` é usado para instalar o Gatsby CLI para que esse possa ser usado na execução do script do projeto para o build do site Gatsby
2. `deploy` somente será disparado quando o build for executado na branch master, neste caso vai disparar o script de deploy. No exemplo acima, o site Gatsby está localizado no diretório `/docs`. O script muda para esse diretório, instala todas as dependências do site, e executa o script de deploy como foi definido no passo anterior.

Fazer commit e push de ambos arquivos `.travis.yml` e `package.json` para sua branch base vai ser o passo final do processo.
