---
title: Node.js
disableTableOfContents: true
---

Aprenda mais sobre Node.js, um dos pacotes de software que torna Gatsby possível.

## O que é Node.js?

Node.js é um interpretador (_runtime_) JavaScript que usa o mesmo motor (_engine_) do Google Chrome. Com Node.js, você pode executar aplicações JavaScript no seu computador, sem a necessidade de um navegador web.

No início dos anos 2000s, serviços como Gmail e Flickr nos mostraram que JavaScript poderia ser usado para construir aplicações robustas, disponíveis para qualquer um com navegador web e conexão com a internet.

No entanto, essas aplicações JavaScript possuiam uma grande limitação: elas só conseguiam executar tão bem quanto o interpretador permitisse. Antes de 2009, o interpretador era quase que sempre um navegador web. Então a Google iniciou o projeto Chromium, em parte para criar um navegador mais rápido. O resultado foi o Google Chrome, lançado em 2008, e seu novo motor JavaScript: [V8](https://v8.dev/).

Um ano depois, Node.js fez sua estréia como um interpretador JavaScript independente utilizando o motor V8.

Depois de instalar o Node.js, você pode usá-lo para executar JavaScript pela [linha de comando](/docs/glossary#command-line). Digite `node` em um _prompt_ para abrir o _shell_ interativo do Node.js. Inclua o caminho de um arquivo JavaScript para executar aquele _script_, exemplo: `node /Users/gatsbyfan/hello-world.js`

Você vai precisar [instalar o Node.js](/tutorial/part-zero/#install-nodejs-for-your-appropriate-operating-system) antes de usar Gatsby. Gatsby é construído usando JavaScript e requer um interpretador Node.js.

Ao instalar o Node.js, também é instalado o [npm](/docs/glossary#npm), o gerenciador de pacote do Node.js. Um gerenciador de pacote é um software especializado que permite você instalar e atualizar módulos e pacotes utilizados em seu projeto.

Você utilizará npm para instalar Gatsby e suas dependências. Digite `npm install -g gatsby-cli` no _prompt_ da linha de comando para instalar a interface de linha de comando do Gatsby ou CLI. A opção (_flag_) `-g` instala Gatsby globalmente, o que significa que você pode usá-lo digitando `gatsby` em um _prompt_. Por exemplo, você pode usar o comando `gatsby new` para criar um novo site Gatsby.

## Aprenda mais sobre Node.js

- [Site oficial](https://nodejs.org/en/) do Node.js

- [Introdução ao Node.js](https://nodejs.dev)

- [NodeSchool](https://nodeschool.io/) oferece oficinas _online_ e presenciais sobre Node.js

- [V8](https://v8.dev/) blog do desenvolvedor
