---
title: Início Rápido
---

Esse guia de início rápido é direcionado para desenvolvedores com conhecimento intermediário ou avançado. Para uma introdução mais amigável ao Gatsby, [visite nosso tutorial](/tutorial/)!

## Usando o Gatsby CLI

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-quick-start-with-gatsby-create-develop-and-build-gatsby-sites-from-the-command-line"
  lessonTitle="Quick Start with Gatsby: Create, Develop, and Build Gatsby Sites From the Command Line"
/>

**Nota**: este vídeo usa o `npx`, que é uma ferramenta para executar um pacote npm sem primeiro instalá-lo. Executar o comando `npx gatsby new` é o mesmo que executar `gatsby new` após instalar o gatsby-cli no seu computador.

<<<<<<< HEAD
### Instalando o Gatsby CLI.
=======
### Install the Gatsby CLI
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
npm install -g gatsby-cli
```

<<<<<<< HEAD
### Criando um novo site.
=======
> The above command installs Gatsby CLI globally on your machine.

### Create a new site
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
gatsby new gatsby-site
```

<<<<<<< HEAD
### Mudando o diretório para a pasta do site.
=======
### Change directories into site folder
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
cd gatsby-site
```

<<<<<<< HEAD
### Iniciando o servidor de desenvolvimento.
=======
### Start development server
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
gatsby develop
```

<<<<<<< HEAD
O Gatsby iniciará um ambiente de desenvolvimento com _hot-reloading_, que pode ser acessado por padrão em `localhost:8000`.
=======
Gatsby will start a hot-reloading development environment accessible by default at `http://localhost:8000`.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Tente editar as páginas JavaScript em `src/pages`. As alterações salvas serão atualizadas automaticamente no navegador.

<<<<<<< HEAD
### Criando um pacote de produção.
=======
### Create a production build
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
gatsby build
```

O Gatsby criará um pacote de produção otimizado para seu site, gerando HTML estático e pacotes JavaScript para cada rota.

<<<<<<< HEAD
### Servindo o pacote de produção localmente.
=======
### Serve the production build locally
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```shell
gatsby serve
```

O Gatsby iniciará um servidor HTML local para testar seu site. Lembre-se de construir seu site usando `gatsby build` antes de usar este comando.

### Acessando a documentação para comandos do CLI

Para ver a documentação detalhada de comandos do CLI, execute `gatsby --help` no terminal.

Para comandos específicos, execute `gatsby COMMAND_NAME --help`, como por exemplo `gatsby new --help`.

Para mais informações sobre o Gatsby CLI, visite a [seção sobre o CLI](/docs/gatsby-cli/) na documentação.
