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

### Instalando o Gatsby CLI.

```shell
npm install -g gatsby-cli
```

### Criando um novo site.

```shell
gatsby new gatsby-site
```

### Mudando o diretório para a pasta do site.

```shell
cd gatsby-site
```

### Iniciando o servidor de desenvolvimento.

```shell
gatsby develop
```

O Gatsby iniciará um ambiente de desenvolvimento com _hot-reloading_, que pode ser acessado por padrão em `localhost:8000`.

Tente editar as páginas JavaScript em `src/pages`. As alterações salvas serão atualizadas automaticamente no navegador.

### Criando um pacote de produção.

```shell
gatsby build
```

O Gatsby criará um pacote de produção otimizado para seu site, gerando HTML estático e pacotes JavaScript para cada rota.

### Servindo o pacote de produção localmente.

```shell
gatsby serve
```

O Gatsby iniciará um servidor HTML local para testar seu site. Lembre-se de construir seu site usando `gatsby build` antes de usar este comando.

### Acessando a documentação para comandos do CLI

Para ver a documentação detalhada de comandos do CLI, execute `gatsby --help` no terminal.

Para comandos específicos, execute `gatsby COMMAND_NAME --help`, como por exemplo `gatsby new --help`.

Para mais informações sobre o Gatsby CLI, visite a [seção sobre o CLI](/docs/gatsby-cli/) na documentação.
