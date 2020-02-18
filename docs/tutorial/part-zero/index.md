---
title: Set Up Your Development Environment
typora-copy-images-to: ./
disableTableOfContents: true
---

Antes de começar a construir seu primeiro site Gatsby, você precisará se familiarizar com algumas das principais tecnologias web e verificar se instalou todas as ferramentas de software necessárias.

## Familiarize-se com a linha de comando

A linha de comando é uma interface baseada em texto usada para executar comandos no seu computador. Às vezes, você encontrará artigos se referindo a ela como _terminal_. Neste tutorial, usaremos os dois termos de forma intercambiável. É como usar o Finder em um Mac ou o Explorer no Windows. Finder e Explorer são exemplos de interfaces gráficas de usuário (GUI). A linha de comando permite uma interação poderosa com os recursos que o seu computador oferece.

<<<<<<< HEAD
Reserve um momento para localizar e acessar a interface da linha de comandos (Command Line Interface - CLI) do seu computador. Dependendo do sistema operacional que você estiver usando, consulte as [**instruções para Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instruções para Windows**](ttps://www.quora.com/How-do-I-open-terminal-in-windows) ou [**instruções para Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

## Instale o Homebrew para Node.js

Para instalar o Gatsby e o Node.js, é recomendável usar o [Homebrew](https://brew.sh/). Investir em uma configuração mínima nesse momento inicial pode te poupar algumas dores de cabeça mais tarde!

Como instalar ou verificar o Homebrew no seu computador:

1. Abra seu Terminal.
1. Veja se o Homebrew está instalado executando `brew -v`. Você deverá ver a palavra "Homebrew" e um número de versão.
1. Caso contrário, faça o download e instale o [Homebrew com as instruções](https://docs.brew.sh/Installation) para o seu sistema operacional (Mac, Linux ou Windows).
1. Depois de instalar o Homebrew, repita a etapa 2 para confirmar o sucesso da instalação.

### Usuário de Mac: instale as ferramentas de linha de comando do Xcode

1. Abra seu Terminal.
1. Em um Mac, instale as ferramentas de linha de comando do Xcode executando o comando `xcode-select --install`.
   1. Se isso falhar, faça o download [diretamente do site da Apple](https://developer.apple.com/download/more/), após fazer login na conta de desenvolvedor da Apple.
1. Ao iniciar a instalação, você será solicitado novamente a aceitar uma licença de software para o download das ferramentas.

## ⌚ Instale o Node.js e o npm

O Node.js é um ambiente que pode executar código JavaScript fora de um navegador da _web_. Gatsby é construído com Node.js. Para começar a trabalhar com o Gatsby, é necessário ter uma versão recente do Node.js instalada no seu computador.

_Nota: a versão mínima do Node.js suportada pelo Gatsby é a 8.0, mas fique à vontade para usar uma versão mais recente._

1. Abra seu terminal.
1. Execute `brew update` para garantir que você estará usando a versão mais recente do Homebrew.
1. Execute este comando para instalar o Node e o npm de uma só vez: `brew install node`

Depois de seguir as etapas de instalação, verifique se tudo foi instalado corretamente:

### Verifique sua instalação do Node.js

1. Abra seu terminal.
2. Execute `node --version`. (Se o terminal é algo novo para você, "Execute `node --version`" significa que você deve escrever o comando no terminal - nesse caso o comando é `node --version` - e em seguida pressionar a tecla _Enter_.  "Executar `comando`" terá esse significado daqui em diante).
3. Execute `npm --version`.

A saída de cada um desses comandos deve ser um número de versão. Suas versões podem não ser as mesmas mostradas abaixo! Se ao executar esses comandos não for exibido um número de versão, refaça a operação para confirmar que instalou o Node.js corretamente.
=======
Take a moment to locate and open up the command line interface (CLI) for your computer. Depending on which operating system you are using, see [**instructions for Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instructions for Windows**](https://www.lifewire.com/how-to-open-command-prompt-2618089) or [**instructions for Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

_Note: If you’re new to the command line, "running" a command, means "writing a given set of instructions in your command prompt, and hitting the Enter key". Commands will be shown in a highlighted box, something like `node --version`, but not every highlighted box is a command! If something is a command it will be mentioned as something you have to run/execute._

## Install Node.js for your appropriate operating system

Node.js is an environment that can run JavaScript code outside of a web browser. Gatsby is built with Node.js. To get up and running with Gatsby, you’ll need to have a recent version installed on your computer. npm comes bundled with Node.js so if you don't have npm, chances are that you don't have Node.js either.

### Mac instructions

To install Gatsby and Node.js on a Mac, it is recommended to use [Homebrew](https://brew.sh/). A little set-up in the beginning can save you from some headaches later on!

#### How to install or verify Homebrew on your computer:

1. Open your Terminal.
2. See if Homebrew is installed by running `brew -v`. You should see "Homebrew" and a version number.
3. If not, download and install [Homebrew with the instructions](https://docs.brew.sh/Installation).
4. Once you've installed Homebrew, repeat step 2 to verify.

#### Install Xcode Command Line Tools:

1. Open your Terminal.
2. Install Xcode Command line tools by running `xcode-select --install`.
   - If that fails, download it [directly from Apple's site](https://developer.apple.com/download/more/), after signing-in with an Apple developer account
3. After being prompted to start the installation, you'll be prompted again to accept a software license for the tools to download.

#### Install Node

1. Open your Terminal
2. Run `brew install node`
   - If you don't want to install it through Homebrew, download the latest Node.js version from [the official Node.js website](https://nodejs.org/en/), double click on the downloaded file and go through the installation process.

### Windows Instructions

- Download and install the latest Node.js version from [the official Node.js website](https://nodejs.org/en/)

### Linux Instructions

Install nvm (Node Version Manager) and needed dependencies. nvm is used to manage Node.js and all its associated versions.

_💡 If when installing a package, it asks for confirmation, type `y` and press enter._

#### Ubuntu, Debian, and other `apt` based distros:

1. Run `sudo apt update` and then `sudo apt -y upgrade` to make sure your Linux distribution is ready to go.
2. Run `sudo apt-get install curl` to install curl which allows you to transfer data and download additional dependencies.
3. After it finishes installing, run `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash` to download the latest nvm version.
4. To confirm this has worked, use the following command. `nvm --version`. The output should be a version number.
5. [Set default Node.js version](#set-default-nodejs-version)

#### Arch, Manjaro and other `pacman` based distros:

1. Run `sudo pacman -Sy` to make sure your distribution is ready to go.
2. These distros come installed with curl, so you can use that to download nvm.
   `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
3. Before using nvm, you need to install additional dependencies by running `sudo pacman -S grep awk tar`.
4. To confirm this has worked, use the following command. `nvm --version`. The output should be a version number.
5. [Set default Node.js version](#set-default-nodejs-version)

#### Fedora, RedHat, and other `dnf` based distros:

1. These distros come installed with curl, so you can use that to download nvm.
   `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
2. To confirm this has worked, use the following command. `nvm --version`. The output should be a version number.
3. [Set default Node.js version](#set-default-nodejs-version)

If the Linux distribution you are using is not listed here, please find instructions on the web.

#### Set default Node.js version

When nvm is installed, it does not default to a particular node version. You’ll need to install the version you want and give nvm instructions to use it. This example uses the latest release of version 10, but more recent version numbers can be used instead.

```shell
nvm install 10
nvm use 10
```

To confirm that this worked, you can run `npm --version` and `node --version`. The output should look similar to the screenshot below, showing version numbers in response to the commands.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

![Verifique as versões do node e npm no terminal](01-node-npm-versions.png)

<<<<<<< HEAD
## Instale o Git
=======
Once you have followed the installation steps and you have checked everything is installed properly, you can continue to the next step.

## Install Git
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

O Git é um sistema de controle de versão distribuído de código aberto e gratuito, projetado para lidar com tudo, desde projetos pequenos a grandes, com rapidez e eficiência. Quando você instala um site _starter_ do Gatsby, o Gatsby usa o Git nos bastidores para baixar e instalar os arquivos necessários para seu starter. Você precisará ter o Git instalado para configurar seu primeiro site Gatsby.

As etapas para baixar e instalar o Git dependem do seu sistema operacional. Siga o guia para o seu sistema:

- [Instale o Git no macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
- [Instale o Git no Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
- [Instale o Git no Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Usando a CLI do Gatsby

A ferramenta CLI do Gatsby permite que você execute os comandos necessários para desenvolver com rapidez os seus sites utilizando a tecnologia do Gatsby. Ela está disponível como um pacote publicado no _npm_.

A CLI do Gatsby está disponível via npm e deve ser instalada globalmente executando `npm install -g gatsby-cli`.

_**Nota**: ao instalar o Gatsby e executá-lo pela primeira vez, você verá uma pequena mensagem notificando sobre dados de uso anônimo que estão sendo coletados para comandos do Gatsby, você pode ler mais sobre como esses dados são extraídos e utilizados no [doc de telemetria](/docs/telemetry)._

Para listar os comandos disponíveis, execute `gatsby --help`.

![Confira os comandos do Gatsby no terminal](05-gatsby-help.png)

> 💡 Caso você não consiga executar a CLI do Gatsby devido a problemas de permissão, consulte os [documentos do npm sobre como corrigir permissões](https://docs.npmjs.com/getting-started/fixing-npm-permissions), ou [este guia](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Crie um site do Gatsby

Agora você está pronto para usar a ferramenta CLI para criar seu primeiro site do Gatsby. Usando a CLI, você pode fazer o download de _starters_ (sites parcialmente construídos e que trazem algumas configurações por padrão) para ajudá-lo a acelerar a criação de um determinado tipo de projeto. O _starter_ do "Hello World" que você usará aqui é um _starter_ que contém os recursos básicos de um site Gatsby.

1. Abra seu terminal.
2. Execute `gatsby new hello-world https: // github.com / gatsbyjs / gatsby-starter-hello-world`. (_Nota: Dependendo da sua velocidade de download, a quantidade de tempo necessária pode variar. Por uma questão de brevidade, o gif abaixo foi pausado durante parte da instalação_).
3. Execute `cd hello-world`.
4. Execute `gatsby develop`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
<<<<<<< HEAD
  <p>Desculpe! Seu navegador não suporta este vídeo.</p>
=======
  <p>Sorry! Your browser doesn't support this video.</p>
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1
</video>

O que acabou de acontecer?

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

- `new` é um comando gatsby para criar um novo projeto Gatsby.
- Aqui, `hello-world` é um título arbitrário - você pode escolher qualquer coisa. A ferramenta CLI colocará o código do seu novo site em uma nova pasta chamada “hello-world”.
- Por fim, o URL do GitHub especificado aponta para um repositório que contém o código inicial que você deseja usar.

```shell
cd hello-world
```

- Esse comando significa "Eu quero mudar de diretório para a subpasta 'hello world'". Sempre que você quiser executar algum comando para o seu site, você precisa estar no contexto desse site (ou seja, seu terminal precisa ser apontado para o diretório que contém o código do site).

```shell
gatsby develop
```

- Este comando inicia um servidor de desenvolvimento. Você poderá ver e interagir com seu novo site em um ambiente de desenvolvimento local (ou seja, rodando no seu computador, não hospedado na Internet).

### Visualize seu site localmente

<<<<<<< HEAD
Abra uma nova guia no seu navegador e navegue até [**http://localhost:8000**](http://localhost:8000/).
=======
Open up a new tab in your browser and navigate to `http://localhost:8000/`
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

![Verifique a página inicial](04-home-page.png)

Parabéns! Este é o começo de seu primeiro site Gatsby! 🎉

<<<<<<< HEAD
Você poderá visitar o site localmente em [**_http://localhost:8000_**](http://localhost:8000/) enquanto seu servidor de desenvolvimento estiver em execução. Esse é o processo que você iniciou executando o comando `gatsby develop`. Para parar de executar esse processo (ou “parar de executar o servidor de desenvolvimento”), volte para a janela do terminal, mantenha pressionada a tecla “control” e pressione “c” (ctrl-c). Para iniciá-lo novamente, execute o `gatsby develop` novamente!

**Nota:** Se você estiver usando uma configuração da VM como `vagrant` e/ou gostaria de escutar no seu endereço IP local, execute `gatsby develop - --host = 0.0.0.0`. Agora, o servidor de desenvolvimento escuta 'localhost' e seu IP local.
=======
You’ll be able to visit the site locally at `http://localhost:8000/` for as long as your development server is running. That’s the process you started by running the `gatsby develop` command. To stop running that process (or to “stop running the development server”), go back to your terminal window, hold down the “control” key, and then hit “c” (ctrl-c). To start it again, run `gatsby develop` again!

**Note:** If you are using VM setup like `vagrant` and/or would like to listen on your local IP address, run `gatsby develop --host=0.0.0.0`. Now, the development server listens on both `http://localhost` and your local IP.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

## Configure um editor de código

Um editor de código é um programa desenvolvido especialmente para editar códigos de computador. Existem ótimos editores por aí.

### Baixe o VS Code

A documentação do Gatsby às vezes inclui capturas de tela que foram tiradas no VS Code, portanto, se você ainda não possui um editor de código preferido, o uso do VS Code garantirá que sua tela se pareça com as capturas de tela no tutorial e nos documentos. Se você optar por usar o Código VS, visite o [site do VS Code](https://code.visualstudio.com/#alt-downloads) e baixe a versão apropriada para sua plataforma.

### Instale o plugin Prettier

Também recomendamos o uso do [Prettier](https://github.com/prettier/prettier), uma ferramenta que ajuda a formatar seu código para evitar erros.

Você pode usar o Prettier diretamente no seu editor usando o [plugin Prettier do VS Code](https://github.com/prettier/prettier-vscode):

<<<<<<< HEAD
1. Abra a visualização de extensões no VS Code (View => Extensions).
2. Procure "Prettier - Code formatter".
3. Clique em "Install". (Após a instalação, você será solicitado a reiniciar o VS Code para habilitar a extensão. As versões mais recentes do VS Code habilitarão a extensão automaticamente após o download.)
=======
1.  Open the extensions view on VS Code (View => Extensions).
2.  Search for "Prettier - Code formatter".
3.  Click "Install". (After installation, you'll be prompted to restart VS Code to enable the extension. Newer versions of VS Code will automatically enable the extension after download.)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

> 💡 Se você não estiver usando o VS Code, consulte a documentação do Prettier para [instruções de instalação](https://prettier.io/docs/en/install.html) ou [integrações para outros editores](https://prettier.io/docs/en/editors.html).

## ➡️ O que vem a seguir?

Para resumir, nesta seção você:

- Aprendeu sobre a linha de comando e como usá-la
- Instalou e aprendeu sobre o Node.js e a ferramenta CLI do npm, o sistema de controle de versão Git e a ferramenta CLI do Gatsby
- Gerou um novo site Gatsby usando a ferramenta CLI Gatsby
- Executou o servidor de desenvolvimento Gatsby e visitou seu site localmente
- Baixou um editor de código
- Instalou um formatador de código chamado Prettier

Agora, vá para [**conhecendo os blocos de construção de Gatsby**](/tutorial/part-one/).

## Referências

### Visão geral das principais tecnologias

Não é necessário ser um especialista nisso - se não for, não se preocupe! Você aprenderá muito ao longo desta série de tutoriais. Estas são algumas das principais tecnologias da web que você usará ao criar um site do Gatsby:

- **HTML**: Uma linguagem de marcação que todo navegador da Web é capaz de entender. Significa HyperText Markup Language. O HTML fornece ao seu conteúdo da web uma estrutura informacional universal, definindo itens como cabeçalhos, parágrafos e muito mais.
- **CSS**: Uma linguagem de apresentação usada para estilizar a aparência do seu conteúdo da web (fontes, cores, layout etc.). Significa Folhas de Estilo em Cascata (do inglês **C**ascading **S**tyle **S**heets).
- **JavaScript**: Uma linguagem de programação que nos ajuda a tornar a web dinâmica e interativa.
- **React**: Uma biblioteca de códigos (criada com JavaScript) para criar interfaces de usuário. É o framework que o Gatsby usa para criar páginas e estruturar o conteúdo.
- **GraphQL**: Uma linguagem de consulta que permite extrair dados para o seu site. É a interface que o Gatsby usa para gerenciar dados do site.

### O que é um site?

Para uma introdução abrangente sobre o que é um site, incluindo uma introdução ao HTML e CSS, confira “[**Construindo sua primeira página da web**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. É um ótimo lugar para começar a aprender sobre a web. Para uma introdução mais prática à [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css), e [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), cconfira os tutoriais da Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) e [**GraphQL**](http://graphql.org/graphql-js/) também têm seus próprios tutoriais introdutórios.

### Saiba mais sobre a interface de linha de comando

Para uma ótima introdução ao uso da linha de comando, consulte [**Tutorial da interface linha de comando da Codecademy**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) para usuários de Mac e Linux e [**este tutorial**](https://www.computerhope.com/issues/chusedos.htm) para usuários de Windows. Mesmo se você for usuário do Windows, a primeira página do tutorial do Codecademy é uma leitura valiosa. Explica o que é a linha de comando, não apenas como interagir com ela.

### Saiba mais sobre o npm

O npm é um gerenciador de pacotes JavaScript. Um pacote é um módulo de código que você pode optar por incluir em seus projetos. Se você acabou de baixar e instalar o Node.js, o npm foi instalado com ele!

O npm possui três componentes distintos: o site npm, o _npm registry_ e a interface da linha de comandos (CLI) do npm.

- No site npm, você pode procurar quais pacotes JavaScript estão disponíveis no _npm registry_.
- O _npm registry_ é um grande banco de dados com informações sobre pacotes JavaScript disponíveis no npm.
- Depois de identificar o pacote desejado, você pode usar a CLI do npm para instalá-lo em seu projeto ou globalmente (como outras ferramentas da CLI). A CLI do npm é o que fala com o _registry_ - geralmente você interage apenas com o site npm ou a CLI do npm.

> 💡 Confira a introdução do npm, “[**O que é npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Saiba mais sobre o Git

Você não precisará conhecer o Git para concluir este tutorial, mas é uma ferramenta muito útil. Se você estiver interessado em aprender mais sobre controle de versão, Git e GitHub, consulte as instruções do GitHub. [Manual do Git](https://guides.github.com/introduction/git-handbook/).
