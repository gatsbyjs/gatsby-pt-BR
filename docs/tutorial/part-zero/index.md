---
title: Configurando seu Ambiente de Desenvolvimento
typora-copy-images-to: ./
disableTableOfContents: true
---

Antes de começar a construir seu primeiro site Gatsby, você precisará se familiarizar com algumas das principais tecnologias web e verificar se instalou todas as ferramentas de software necessárias.

## Familiarize-se com a linha de comando

A linha de comando é uma interface baseada em texto usada para executar comandos no seu computador. Às vezes, você encontrará artigos se referindo a ela como _terminal_. Neste tutorial, usaremos os dois termos de forma intercambiável. É como usar o Finder em um Mac ou o Explorer no Windows. Finder e Explorer são exemplos de interfaces gráficas de usuário (GUI). A linha de comando permite uma interação poderosa com os recursos que o seu computador oferece.

Reserve um momento para localizar e abrir a interface de linha de comando (CLI) do seu computador. De acordo com o sistema operacional que você está utilizando veja, [**instruções para Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instruções para Windows**](https://www.lifewire.com/how-to-open-command-prompt-2618089) ou [**instruções para Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

_Nota: Se você é novo com linha de comando, "executar" um comando, significa "escrever um conjunto de instruções em seu prompt de comando, e apertar a tecla Enter". Comandos serão mostrados em uma caixa destacada, algo como `node --version`, mas nem toda caixa destacada é um comando! Se algo for um comando será mencionado que é algo que você deve rodar/executar._

## Instale o Node.js apropriado para o seu sistema operacional
Node.js é um ambiente que pode executar código JavaScript fora de um navegador web. Gatsby é construído com Node.js. Para começar a usar o Gatsby, você precisa ter uma versão recente do Node.js instalada em seu computador. O _npm_ vem atrelado ao Node.js então caso você não o tenha, há grandes chances de você não ter o Node.js também.

### Instruções para Mac

Para instalar o Gatsby e o Node.js em um Mac é recomendada a utilização do [Homebrew](https://brew.sh/). Uma pequena configuração no começo irá livrar você de algumas dores de cabeça mais tarde.

#### Como instalar ou verificar o Homebrew em seu computador:

1. Abra seu Terminal.
2. Veja se o Homebrew está instalado executando `brew -v`. Você deve ver "Homebrew" e um número de versão.
3. Caso não, baixe e instale o [Homebrew com essas instruções](https://docs.brew.sh/Installation).
4. Depois de instalar o Homebrew, repita o passo 2 para verificar.

#### Instalando a ferramenta de linha de comando (CLI) do Xcode
1. Abra seu Terminal.
2. Instale o Xcode CLI executando o comando `xcode-select --install`.
   - Caso isso falhe, baixe [direto do site da Apple](https://developer.apple.com/download/more/), depois de fazer login com uma conta de desenvolvedor Apple
3. Depois do inicio da instalação, será solicitado novamente para aceitar uma licença de software para o download das ferramentas.

#### Instalando o Node

1. Abra seu Terminal
2. Execute o comando `brew install node`
   - Se você não quiser instalar através do Homebrew, baixe a versão mais recente do Node.js no [site oficial](https://nodejs.org/pt-br/), clique duas vezes no arquivo baixado e siga o processo de instalação.

### Instruções para Windows

- Baixe e instale a versão mais recente do Node.js no [site oficial](https://nodejs.org/pt-br/)

### Instruções para Linux

Instale o nvm (Node Version Manager) e as dependências necessárias. O nvm é usado para gerenciar o Node.js e todas as suas versões associadas.

_💡 Se quando estiver instalando um pacote, for solicitado uma confirmação, digite `y` e pressione enter._

#### Ubuntu, Debian, e outras distros baseadas no `apt`:

1. Execute `sudo apt update` e depois `sudo apt -y upgrade` para garantir que sua distribuição Linux está pronta para ser usada.
2. Execute `sudo apt-get install curl` para instalar o curl, que permite transferir dados e baixar dependências adicionais.
3. Após terminar a instalação, execute `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash` para baixar a última versão do nvm.
4. Para garantir que está funcionando, use o seguinte comando. `nvm --version`. A saída deve ser um número de versão.
5. [Defina uma versão padrão do Node.js](#set-default-nodejs-version)

#### Arch, Manjaro e outras distros baseadas no `pacman`:

1. Execute `sudo pacman -Sy` para garantir que sua distribuição está preparada.
2. Essas distros vêm instaladas com curl, então você pode executar o seguinte comando para baixar o nvm. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
3. Antes de usar o nvm você precisa instalar as dependências adicionais executando o comando: `sudo pacman -S grep awk tar`.
4. Para garantir que está funcionando, use o seguinte comando. `nvm --version`. A saída deve ser um número de versão.
5. [Defina uma versão padrão do Node.js](#set-default-nodejs-version)

#### Fedora, RedHat, e outras distros baseadas no `dnf`:

1. Essas distros vêm instaladas com curl, então você pode executar o seguinte comando para baixar o nvm. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
2. Para garantir que está funcionando, use o seguinte comando. `nvm --version`. A saída deve ser um número de versão.
3. [Defina uma versão padrão do Node.js](#set-default-nodejs-version)

Se a distribuição Linux que você está utilizando não está listada aqui, por favor encontre instruções na internet.

#### Definindo uma versão padrão do Node.js

Quando o nvm é instalado, ele não é padronizado para uma versão específica do Node. Você precisará instalar a versão desejada e fornecer instruções do nvm para usá-la. Este exemplo usa a versão mais recente da versão 10, mas números de versão mais recentes podem ser usados.

```shell
nvm install 10
nvm use 10
```

Para garantir que está funcionando, execute o comando `npm --version` e `node --version`. A saída deve ser algo similar à captura de tela abaixo, mostrando os números da versão de acordo com os comandos.

![Verifique as versões do node e npm no terminal](01-node-npm-versions.png)

## Instale o Git

O Git é um sistema de controle de versão distribuído de código aberto e gratuito, projetado para lidar com tudo, desde projetos pequenos a grandes, com rapidez e eficiência. Quando você instala um site _starter_ do Gatsby, o Gatsby usa o Git nos bastidores para baixar e instalar os arquivos necessários para seu _starter_. Você precisará ter o Git instalado para configurar seu primeiro site Gatsby.

As etapas para baixar e instalar o Git dependem do seu sistema operacional. Siga o guia para o seu sistema:

- [Instale o Git no macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
- [Instale o Git no Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
- [Instale o Git no Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Usando a CLI do Gatsby

A ferramenta CLI do Gatsby permite que você execute os comandos necessários para desenvolver com rapidez os seus sites utilizando a tecnologia do Gatsby. Ela está disponível como um pacote publicado no _npm_.

A CLI do Gatsby está disponível via npm e deve ser instalada globalmente executando `npm install -g gatsby-cli`.

_**Nota**: ao instalar o Gatsby e executá-lo pela primeira vez, você verá uma pequena mensagem notificando sobre dados de uso anônimo que estão sendo coletados para comandos do Gatsby, você pode ler mais sobre como esses dados são extraídos e utilizados na [documentação de telemetria](/docs/telemetry)._

Para listar os comandos disponíveis, execute `gatsby --help`.

![Confira os comandos do Gatsby no terminal](04-gatsby-help.png)

> 💡 Caso você não consiga executar a CLI do Gatsby devido a problemas de permissão, consulte os [documentos do npm sobre como corrigir permissões](https://docs.npmjs.com/getting-started/fixing-npm-permissions), ou [este guia](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Crie um site do Gatsby

Agora você está pronto para usar a ferramenta CLI para criar seu primeiro site do Gatsby. Usando a CLI, você pode fazer o download de _starters_ (sites parcialmente construídos e que trazem algumas configurações por padrão) para ajudá-lo a acelerar a criação de um determinado tipo de projeto. O _starter_ do "Hello World" que você usará aqui é um _starter_ que contém os recursos básicos de um site Gatsby.

1. Abra seu terminal.
2. Execute `gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world`. (_Nota: Dependendo da sua velocidade de download, a quantidade de tempo necessária pode variar. Por uma questão de brevidade, o gif abaixo foi pausado durante parte da instalação_).
3. Execute `cd hello-world`.
4. Execute `gatsby develop`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./02-create-site.mp4" />
  <p>Desculpe! Seu navegador não suporta este vídeo.</p>
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

Abra uma nova guia no seu navegador e navegue até `http://localhost:8000/`

![Verifique a página inicial](03-home-page.png)

Parabéns! Este é o começo de seu primeiro site Gatsby! 🎉

Você poderá visitar o site localmente em `http://localhost:8000/` enquanto seu servidor de desenvolvimento estiver em execução. Esse é o processo que você iniciou executando o comando `gatsby develop`. Para parar de executar esse processo (ou “parar de executar o servidor de desenvolvimento”), volte para a janela do terminal, mantenha pressionada a tecla “control” e pressione “c” (ctrl-c). Para iniciá-lo novamente, execute o `gatsby develop` novamente!

**Nota:** Se você estiver usando uma configuração da VM como `vagrant` e/ou gostaria de escutar no seu endereço IP local, execute `gatsby develop - --host = 0.0.0.0`. Agora, o servidor de desenvolvimento escuta `http://localhost` e seu IP local.

## Configure um editor de código

Um editor de código é um programa desenvolvido especialmente para editar códigos de computador. Existem ótimos editores por aí.

### Baixe o VS Code

A documentação do Gatsby às vezes inclui capturas de tela que foram tiradas no VS Code, portanto, se você ainda não possui um editor de código preferido, o uso do VS Code garantirá que sua tela se pareça com as capturas de tela no tutorial e nos documentos. Se você optar por usar o VS Code, visite o [site do VS Code](https://code.visualstudio.com/#alt-downloads) e baixe a versão apropriada para sua plataforma.

### Instale o plugin Prettier

Também recomendamos o uso do [Prettier](https://github.com/prettier/prettier), uma ferramenta que ajuda a formatar seu código para evitar erros.

Você pode usar o Prettier diretamente no seu editor usando o [plugin Prettier do VS Code](https://github.com/prettier/prettier-vscode):

1. Abra a visualização de extensões no VS Code (View => Extensions).
2. Procure "Prettier - Code formatter".
3. Clique em "Install". (Após a instalação, você será solicitado a reiniciar o VS Code para habilitar a extensão. As versões mais recentes do VS Code habilitarão a extensão automaticamente após o download.)

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

Para uma introdução abrangente sobre o que é um site, incluindo uma introdução ao HTML e CSS, confira “[**Construindo sua primeira página da web**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. É um ótimo lugar para começar a aprender sobre a web. Para uma introdução mais prática à [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css), e [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), confira os tutoriais da Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) e [**GraphQL**](http://graphql.org/graphql-js/) também têm seus próprios tutoriais introdutórios.

### Saiba mais sobre a interface de linha de comando

Para uma ótima introdução ao uso da linha de comando, consulte [**Tutorial da interface linha de comando da Codecademy**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) para usuários de Mac e Linux e [**este tutorial**](https://www.computerhope.com/issues/chusedos.htm) para usuários de Windows. Mesmo se você for usuário do Windows, a primeira página do tutorial do Codecademy é uma leitura valiosa. Explica o que é a linha de comando, não apenas como interagir com ela.

### Saiba mais sobre o npm

O **npm** é um gerenciador de pacotes JavaScript. Um pacote é um módulo de código que você pode optar por incluir em seus projetos. Se você acabou de baixar e instalar o Node.js, o npm foi instalado com ele!

O npm possui três componentes distintos: o site npm, o _npm registry_ e a interface da linha de comandos (CLI) do npm.

- No site npm, você pode procurar quais pacotes JavaScript estão disponíveis no _npm registry_.
- O _npm registry_ é um grande banco de dados com informações sobre pacotes JavaScript disponíveis no npm.
- Depois de identificar o pacote desejado, você pode usar a CLI do npm para instalá-lo em seu projeto ou globalmente (como outras ferramentas da CLI). A CLI do npm é o que fala com o _registry_ - geralmente você interage apenas com o site npm ou a CLI do npm.

> 💡 Confira a introdução do npm em “[**O que é npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Saiba mais sobre o Git

Você não precisará conhecer o Git para concluir este tutorial, mas é uma ferramenta muito útil. Se você estiver interessado em aprender mais sobre controle de versão, Git e GitHub, consulte as instruções do GitHub. [Manual do Git](https://guides.github.com/introduction/git-handbook/).
