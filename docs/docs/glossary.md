---
title: Glossário
disableTableOfContents: true
---

<<<<<<< HEAD
import HorizontalNavList from "../../www/src/components/horizontal-nav-list.js"

Quando você é novo no Gatsby, pode haver muitas palavras para aprender. Este glossário tem como objetivo fornecer uma visão geral de termos comuns e o que eles significam para sites Gatsby.
=======
When you're new to Gatsby there can be a lot of words to learn. This glossary aims to give you a 10,000-foot overview of common terms and what they mean for Gatsby sites.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

<HorizontalNavList
items={"ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("")}
slug={props.slug}
/>

## A

### AST

Árvore Sintática Abstrata: Uma representação em árvore do código fonte encontrado durante uma etapa de [compilação](#compilador) entre duas linguagens. Por exemplo, [gatsby-transformer-remark](/packages/gatsby-transformer-remark/) criará um AST do [Markdown](#markdown) para descrever um documento Markdown em uma estrutura de árvore usando o analisador [Remark](#remark).

### API

Interface de Programação de Aplicações: Um método para um aplicativo se comunicar com outro. Por exemplo, um [plugin nativo](#plugin-nativo) geralmente usa uma API para obter seus dados.

### Acessibilidade

A prática inclusiva de remover barreiras que impedem a interação ou acesso a sites por pessoas com deficiência. Quando os sites são projetados corretamente, desenvolvidos e editados para acessibilidade, geralmente todos os usuários têm acesso igual às informações e funcionalidades. Leia sobre o [Compromisso do Gatsby com a Acessibilidade](/blog/2019-04-18-gatsby-commitment-to-accessibility/).

### Ambiente

Ambiente no qual o seu projeto Gatsby está sendo executado. Por exemplo, quando você está desenvolvendo o site, você provavelmente deseja o máximo de informações de _debugging_ possível, no entanto esse recurso não é indicado para quando o site está _no ar_ ou quando o aplicativo está sendo utilizado no celular do usuário final. Através do conceito de _ambiente_, o Gatsby consegue se adaptar ao contexto no no qual ele está sendo utilizado.

O Gatsby suporta dois ambientes por padrão: [ambiente de desenvolvimento](#ambiente-de-desenvolvimento) e [ambiente de produção](#ambiente-de-produção).

### Ambiente de Desenvolvimento

[Ambiente](#ambiente) que você utiliza quando está programando. Esse ambiente é disponibilizado pela [CLI](#cli) ao executar o comando `gatsby develop` e exibe relatórios de erro, entre outros recursos que ajudam na solução de problemas antes de publicar o site em um [ambiente de produção](#ambiente-de-produção).

### Ambiente de Produção

[Ambiente](#ambiente) para [build](#build) do site ou aplicação que será utilizada pelos usuários quando for [publicada](#publicação). Pode ser acessado através da [CLI](#cli) usando `gatsby build` ou `gatsby serve`.

## B

### Babel

Uma ferramenta que permite escrever o [JavaScript](#javascript) mais moderno e durante o [build](#build) é [compilado](#compilador) para código que a maioria dos navegadores da web pode entender.

### Backend

<<<<<<< HEAD
Os bastidores que o [público](#público) não vê. Isso geralmente se refere ao painel de controle do seu [CMS](#cms). Geralmente, eles são desenvolvidos com linguagens de programação _server-side_ (aquelas que rodam no servidor), como Node.js, PHP, Go, ASP.net, Ruby, ou Java.

### Banco de dados

Um banco de dados é uma coleção estruturada de dados ou conteúdo. Geralmente, um [CMS](#cms) é salvo em um banco de dados usando [tecnologias backend](#backend). Eles são frequentemente acessados no Gatsby por meio de um [plugin nativo](#plugin-nativo).
=======
The behind the scenes that the [public](#public) does not see. This often refers to the control panel of your [CMS](#cms). These are often powered by server-side programming languages such as Node.js, PHP, Go, ASP.net, Ruby, or Java.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

### Build

No Gatsby, esse é o processo de pegar seu código e conteúdo e empacotá-lo em um site que pode ser hospedado e acessado. Geralmente chamado de _tempo de compilação_. Consulte também: [backend](#backend) e [server-side](#server-side).

## C

### Cache

Um armazenamento local de informações que podem ser usadas novamente, para que cálculos e pesquisas possam ser recuperados mais rapidamente em um único local. O Gatsby usa um cache para armazenar informações, para que ele possa construir seu site mais rapidamente quando você estiver desenvolvendo sem precisar fazer o mesmo trabalho duas vezes.

### CLI

Interface de Linha de Comando: um aplicativo que é executado no seu computador através da [linha de comando](#linha-de-comando) e interage com seu teclado.

Gatsby tem duas interfaces de linha de comando. Um, [`gatsby`](/docs/gatsby-cli/), para o desenvolvimento diário com Gatsby e outro, [`gatsby-dev`](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions), para aqueles que contribuem para o projeto Gatsby.

### Client-side

Client-side refere-se às operações executadas pelo navegador do usuário em um [relacionamento cliente–servidor](https://pt.wikipedia.org/wiki/Modelo_cliente%E2%80%93servidor) em uma rede de computadores. No Gatsby, isso é importante ao [trabalhar com pacotes](/docs/using-client-side-only-packages/) que dependem de objetos do [DOM do navegador](#dom), como `window` or `navigator`. Consulte também: [server-side](#server-side), [frontend](#frontend), e [backend](#backend).

### CMS

Sistema de Gerenciamento de Conteúdo: um aplicativo em que você pode gerenciar seu conteúdo e salvá-lo em um banco de dados ou arquivo para acesso posterior. Exemplos de Sistemas de Gerenciamento de Conteúdo incluem WordPress, Drupal, Contentful, e Netlify CMS.

### Código Fonte

O código-fonte é o código que fica na pasta `/src/` e compõe os aspectos exclusivos do seu site ou aplicativo. É composto de [JavaScript](#javascript) e, às vezes, [CSS](#css) e outros arquivos.

O código fonte é [incorporado](#build) ao site que o [público](#público) verá.

### Compilador

Um compilador é um programa que converte código escrito em um linguagem para outra linguagem. Por exemplo, o [Gatsby](#gatsby) pode compilar aplicativos [React](#react) em arquivos [HTML](#html) estáticos.

### Componente

Os componentes são blocos de código independentes e reutilizáveis do [React](#react) que, quando combinados, compõem seu site ou aplicativo.

Um componente pode incluir componentes dentro dele. De fato, [páginas](#página) e [templates](#template) são exemplos de componentes.

### Configuração

O arquivo de configuração, `gatsby-config.js` informa ao Gatsby informações sobre o seu site. Uma opção comum definida na configuração são os metadados do seu site que podem potencializar suas meta tags de SEO.

### [Continuous Deployment](/docs/glossary/continuous-deployment)

Continuous deployment (CD) automates the process of releasing changes to your project. A continuous deployment workflow automatically builds and tests your project, and publishes your changes only when they pass the required tests.

### CSS

<<<<<<< HEAD
[CSS](https://developer.mozilla.org/pt-BR/docs/Web/CSS) significa Folhas de Estilo em Cascata, e é uma parte importante da Plataforma Web com [HTML](#html) e [JavaScript](#javascript). CSS é uma linguagem para estilizar páginas da web projetadas para serem altamente compatíveis com versões anteriores. À medida que novos recursos são lançados para os usuários finais, os [analisadores de CSS](https://www.html5rocks.com/pt/tutorials/internals/howbrowserswork/#CSS_parsing) podem ignorar com segurança os recursos não suportados e aprimorar as propriedades que eles suportam. O CSS realiza isso com seu design em _cascata_, fundamental para criar estilos com novas técnicas, como [CSS Grid](https://developer.mozilla.org/pt-BR/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_and_Progressive_Enhancement) ao mesmo tempo em que fornece alternativas para navegadores mais antigos. O Gatsby suporta várias [abordagens de estilo](/docs/styling/), incluindo arquivos CSS regulares, módulos CSS e CSS-in-JS.
=======
[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) stands for Cascading Style Sheets, and it's a major part of the Web Platform with [HTML](#html) and [JavaScript](#javascript). CSS is a language for styling webpages designed to be highly backwards-compatible. As new features are rolled out to end users, [CSS parsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#CSS_parsing) can safely ignore unsupported features and enhance with the properties they do support. CSS accomplishes this with its _cascading_ design, fundamental to styling with new techniques like [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_and_Progressive_Enhancement) while providing fallbacks for older browsers. Gatsby supports multiple [approaches to styling](/docs/styling/), including regular CSS files, CSS modules, and CSS-in-JS.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

## D

### Decoupled

<<<<<<< HEAD
A dissociação descreve a separação de diferentes preocupações. Com o [Gatsby](#gatsby) , isso geralmente significa dissociar o [frontend](#frontend) do [backend](#backend), como no [Decoupled Drupal](https://dri.es/how-to-decouple-drupal-in-2019) ou [Headless WordPress](https://www.smashingmagazine.com/2018/10/headless-wordpress-decoupled/).
=======
Decoupling describes the separation of different concerns. With [Gatsby](#gatsby) this most commonly means decoupling the [frontend](#frontend) from the [backend](#backend), like with [Decoupled Drupal](https://dri.es/how-to-decouple-drupal-in-2019) or [Headless WordPress](https://www.smashingmagazine.com/2018/10/headless-wordpress-decoupled/).

### [Decoupled Drupal](/docs/glossary/decoupled-drupal)

Decoupling refers to the practice of using Drupal as a [headless CMS](#headless-cms). A decoupled Drupal instance functions as a content API that returns JSON for your [frontend](#frontend) to consume.

### Deploy

The process of [building](#build) your website or app and uploading onto a [hosting provider](#hosting).

### Development Environment

The [environment](#environment) when you're developing your code. It's accessed through the [CLI](#cli) using `gatsby develop`, and provides extra error reporting and things to help you debug before building for [production](#production-environment).
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

### DOM

O Modelo de Objeto do Documento, conhecido como "o DOM", é uma API de navegador padrão que conecta páginas da web a scripts ou linguagens de programação, representando a estrutura de um documento HTML na memória. Os desenvolvedores geralmente interagem com o DOM por meio da marcação [HTML](#html) (escrita em [JSX](#jsx) no Gatsby), além do código [React](https://pt-br.reactjs.org/docs/react-dom.html) e [vanilla JavaScript](https://developer.mozilla.org/pt-BR/docs/DOM/Referencia_do_DOM/Introdu%C3%A7%C3%A3o#DOM_and_JavaScript). Outro aspecto importante da utilização do DOM em todo o seu potencial é escrever uma marcação HTML [acessível](#acessibilidade) para expor a estrutura de uma página à tecnologia assistida.

## E

### ECMAScript

ECMAScript (geralmente chamado de ES) é uma especificação para linguagens de script. [JavaScript](#javascript) é uma implementação do ECMAScript. Frequentemente, os desenvolvedores usam o [Babel](#babel) para [compilar](#compilador) o código ECMAScript mais recente em JavaScript mais amplamente suportado.

### Esquema

Uma representação exata de como os dados são armazenados em um sistema, como tabelas e campos em um banco de dados ou em uma estrutura de arquivos JSON. No Gatsby, o esquema do GraphQL expressa todos os dados consultáveis - ou dados sobre os quais os componentes podem perguntar como parte da camada de dados do Gatsby.

## F

### Fonte de Dados

Ponto de origem do conteúdo e dos dados, normalmente integrado ao Gatsby com [plugins nativo](#plugin-nativo). Uma fonte de dados geralmente é um [Headless CMS](#headless-cms), mas também pode incluir arquivos Markdown, JSON, ou arquivos YAML.

### Frontend

A interface [voltada para o público](#público) do seu site ou aplicativo, fornecida usando tecnologias da web: HTML, CSS e JavaScript. Para obter mais informações sobre como a Plataforma Web reúne essas tecnologias, consulte este artigo em [Como Funcionam os Navegadores](https://www.html5rocks.com/pt/tutorials/internals/howbrowserswork/).

## G

### Gatsby

O Gatsby é uma estrutura de site moderna que aprimora o desempenho de todos os sites ou aplicativos, aproveitando as mais recentes tecnologias da web, como [React](#react), [GraphQL](#graphql), e [JavaScript](#javascript) moderno. O Gatsby facilita a criação de experiências na web incrivelmente rápidas e atraentes, sem a necessidade de se tornar um especialista em desempenho.

### [GraphQL](/docs/glossary/graphql)

Uma linguagem de [consulta](#query) que permite extrair dados para o seu site ou aplicativo. É a [interface que Gatsby usa](/docs/graphql/) para gerenciar dados do site.

## H

### HTML

Uma linguagem de marcação que todo navegador da web é capaz de entender. Significa Linguagem de Marcação de Hipertexto. O [HTML](https://developer.mozilla.org/pt-BR/docs/Web/HTML) fornece ao seu conteúdo da web uma estrutura informacional universal, definindo itens como cabeçalhos, parágrafos e muito mais. Também é fundamental para fornecer um site acessível.

### [Headless CMS](/docs/glossary/headless-cms)

Um [CMS](#cms) que lida apenas com o gerenciamento de conteúdo do [backend](#backend) em vez de lidar com o backend e o [frontend](#frontend). Esse tipo de configuração também é conhecido como [Desacoplado](#decoupled).

<<<<<<< HEAD
### Hospedagem
=======
### [Headless WordPress](/docs/glossary/headless-wordpress)

The practice of using JSON returned from the WordPress REST API as a [headless CMS](#headless-cms). It allows you to use WordPress to write and edit content that can be consumed by any client capable of parsing JSON.

### Hosting
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Um provedor de hospedagem mantém uma cópia do seu site ou aplicativo e o torna acessível [ao público](#público). Os [provedores de hospedagem comuns para projetos Gatsby](/docs/deploying-and-hosting/) incluem Netlify, AWS, S3, Surge, Heroku e mais.

### Hot module replacement

Um recurso em uso quando você executa o `gatsby develop` que atualiza ao vivo seu site ao salvar código em um editor de texto, substituindo automaticamente módulos ou blocos de código em uma janela aberta do navegador.

### Hydration

Depois que um site é [construído](#build) pelo Gatsby e carregado em um navegador web, os recursos JavaScript do [client-side](#client-side) baixam e transformam o site em um aplicativo React completo que pode manipular o [DOM](#dom). Esse processo geralmente é chamado de reidratação, pois executa o mesmo código JavaScript usado para gerar páginas do Gatsby, mas desta vez com APIs DOM disponíveis no navegador, como `window`.

## I

### Inference

As part of its data layer and [build](#build) process, Gatsby will automatically **infer** a [schema](#schema), or type-based structure, based on available data sources (e.g. Markdown file nodes, WordPress posts, etc.). More control can be gained over this structure by using Gatsby's [Schema Customization API](/docs/schema-customization/).

## J

### [JAMStack](/docs/glossary/jamstack)

O JAMStack se refere a uma arquitetura moderna da web usando [JavaScript](#javascript), [APIs](#api) e marcação ([HTML](#html)). Do [JAMStack.org](https://jamstack.org): "É uma nova maneira de criar sites e aplicativos que oferece melhor desempenho, maior segurança, menor custo de dimensionamento e melhor experiência do desenvolvedor".

### JavaScript

Uma linguagem de programação que nos ajuda a tornar a web dinâmica e interativa. [JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/Javascript) é uma tecnologia da Web amplamente implantada em navegadores. Também é usado no _server-side_ com [Node.js](#nodejs). É uma implementação da especificação [ECMAScript](#ECMAScript).

### JSX

JSX é uma extensão do JavaScript que permite que os desenvolvedores escrevam HTML e componentes personalizados no mesmo trecho de código. A [equipe do React recomenda](https://pt-br.reactjs.org/docs/introducing-jsx.html) usá-lo para descrever a aparência de uma [UI](#UI).  O JSX pode lembrá-lo de uma linguagem de template, mas vem com todo o poder do JavaScript. Alguns detalhes importantes a serem observados são que, como o JSX usa JavaScript, alguns atributos HTML da sua marcação precisam ser trocados para evitar palavras reservadas no JavaScript (coisas como `htmlFor` e `className`).

## K

## L

### Linha de Comando

Uma interface baseada em texto para executar comandos no seu computador. Os aplicativos de linha de comando padrão para Mac e Windows são `Terminal` e `Prompt de Comando` respectivamente.

### Linting

Linting é o processo de execução de um programa que analisará o código quanto a possíveis erros. O projeto Gatsby usa [prettier](https://prettier.io/) para identificar e corrigir problemas comuns de estilo. Outro exemplo de um linter comumente usado em projetos React é o [eslint-jsx-plugin-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y), que verifica problemas comuns de [acessibilidade](#acessibilidade) no desenvolvimento.

## M

### MDX

Estende o [Markdown](#markdown) para dar suporte aos [componentes](#componente) do [React](#react) dentro do seu conteúdo.

### Markdown

Uma maneira de escrever conteúdo HTML com texto sem formatação, usando caracteres especiais para indicar tipos de conteúdo, como símbolos de hash para [títulos](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/Heading_Elements), e sublinhados e asteriscos para enfatizar o texto.

### Melhoramento progressivo

Melhoramento progressivo (_progressive enhancement_) é uma estratégia de desenvolvimento que prioriza o carregamento do conteúdo essencial de uma página _web_ frente a outras operações, incluíndo o carregamento do código [JavaScript](#javascript). Após essa etapa de carregamento do conteúdo inicial, mais recursos e camadas de apresentação são servidas ao úsuario de acordo com os recursos do navegador e da qualidade/velocidade de conexão do usuário. A estratégia de [construção](#build) de sites que o Gatsby utiliza por padrão prepara o conteúdo do site com antecedêcia em tempo de compilação, o que significa que o conteúdo do site é carregado primeiro e outros elementos são ativados quando os _scripts_ são carregados e executados.

## N

### NPM

Gerenciador de [Pacotes](#pacote) [Node](#nodejs). Permite instalar e atualizar outros pacotes dos quais seu projeto depende. [Gatsby](#gatsby) e [React](#react) são exemplos das dependências do seu projeto. Consulte também: [Yarn](#yarn).

### Node

Gatsby usa [nós de dados](/docs/node-interface/) para representar um único pedaço de dados. Uma [fonte de dados](#fonte-de-dados) criará vários nós.

### [Node.js](/docs/glossary/node)

Um programa que permite executar o [JavaScript](#javascript) no seu computador. Gatsby é feito em Node.

## O

## P

### Pacote

Um pacote geralmente descreve um programa [JavaScript](#javascript) ue possui informações adicionais sobre como ele deve ser distribuído e usado, como o número da versão. O [NPM](#npm) e o [Yarn](#yarn) gerenciam e instalam os pacotes que seu projeto usa. O próprio [Gatsby](#gatsby) é um pacote.

### Página

Uma página [HTML](#html).

Isso também se refere frequentemente aos [componentes](#componente) que ficam em `/src/pages/` e são convertidos em páginas pelo [Gatsby](#gatsby), além de [páginas criadas dinamicamente](/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) no seu arquivo `gatsby-node.js`.

### Plugin

Código adicional que acrescenta funcionalidades a um projeto Gatsby que não estejam incluídas por padrão.
Alguns [plugins](/plugins/) populares incluem os plugins [nativos](#plugin-nativo) e [transformer](#transformer) que são utilizados para carregar e manipular dados, respectivamente.

### Plugin Nativo

Um [plugin](#plugin) que adiciona [fontes de dados](#fonte-de-dados) adicionais ao Gatsby que podem ser [consultadas](#query) por suas [páginas](#página) e [componentes](#componente).

### Publicação

O processo de [construção](#build) do seu site ou aplicativo e envio para um [provedor de hospedagem](#hospedagem).

### Programaticamente

<<<<<<< HEAD
Algo que acontece automaticamente com base no seu código e configuração. Por exemplo, você pode [configurar](#configuração) seu projeto para criar uma [página](#página) para cada postagem de blog escrita ou ler e exibir o ano atual como parte de um _copyright_ no rodapé do site.
=======
Progressive enhancement is a strategy for the web that emphasizes core page content is loaded from a server before anything else, without [JavaScript](#javascript) as a requirement to load. This strategy then progressively adds more complex layers of presentation and features on top of the content as the end user's browser/network connection allow. Gatsby's default approach to [building](#build) pages ahead-of-time means content will load first and enhance as scripts download and execute.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

### Público

Geralmente, isso se refere a um membro do público (em oposição à sua equipe) ou à pasta `/public` em que o site ou aplicativo [construído](#build) é salvo.

## Q

### Query

O processo de solicitar dados específicos de algum lugar. Com o Gatsby, você normalmente consulta com o [GraphQL](#graphql).

## R

### [React](/docs/glossary/react)

Uma biblioteca de códigos (escrita com [JavaScript](#javascript)) para construção de interfaces de usuário. É a estrutura que o [Gatsby](#gatsby) usa para construir páginas e estruturar o conteúdo.

### Remark

Um analisador para traduzir o [Markdown](#markdown) para outros formatos, como [HTML](#html) ou código [React](#react).

### Runtime

Tempo de execução é quando um programa está sendo executado (ou sendo executável); pode se referir a algumas coisas. O [Node.js](#nodejs) executa o código JavaScript em tempo de execução no [server-side](#server-side). O [JavaScript client-side](#client-side), por outro lado, refere-se ao tempo de execução do navegador em que o código JavaScript tradicional é executado. O Gatsby compila seu site em [tempo de construção](#build) e [reidrata com o React runtime](#hydration) para fornecer uma experiência rápida, interativa e dinâmica ao usuário.

### Roteamento

O roteamento é o mecanismo para carregar o conteúdo correto em um site ou aplicativo com base em uma solicitação de rede - geralmente uma URL. Por exemplo, ele permite rotear URLs como `/about-us` para a [página](#página), [template](#template), ou [componente](#componente) apropriado.

## S

### Server-side

A parte do server-side do [relacionamento cliente-servidor](https://pt.wikipedia.org/wiki/Modelo_cliente%E2%80%93servidor) refere-se às operações executadas por um programa de computador que gerencia o acesso a um recurso ou serviço centralizado em uma rede de computadores. O Gatsby usa a tecnologia [Node.js](#nodejs) do _server-side_ para compilar páginas em tempo de compilação, em vez de servi-las no [tempo de execução do navegador](#runtime) com JavaScript do [client-side](#client-side). Consulte também: [frontend](#frontend) e [backend](#backend).

### Sistema de arquivo

A maneira como os arquivos são organizados. Com o Gatsby, significa ter arquivos no mesmo local que o código do seu site ou aplicativo, ao invés de extrair dados de uma [fonte](#fonte-de-dados) externa. O uso comum do sistema de arquivos no Gatsby inclui conteúdo Markdown, imagens, arquivos de dados e outros _assets_.

### Starter

Um projeto Gatsby pré-configurado que pode ser usado como ponto de partida para o seu projeto. Eles podem ser descobertos usando a [Biblioteca do Gatsby Starter](/starters/) e instalados usando a [CLI do Gatsby](/docs/starters/).

### Static

Gatsby [constrói](#build) versões estáticas da sua página que podem ser facilmente [hospedadas](#hospedagem). Isso contrasta com os sistemas dinâmicos nos quais cada página é gerada rapidamente. Ser estático proporciona grandes ganhos de desempenho porque o trabalho precisa ser feito apenas uma vez por alteração de conteúdo ou código.

Também se refere à pasta `/static` que é automaticamente copiada para `/public` em cada [construção](#build) para arquivos que não precisam ser processados pelo Gatsby, mas que existem em [public](#público).

### [Static Site Generator](/docs/glossary/static-site-generator)

A software application that creates HTML pages from templates or [components](#component) and a given content source.

## T

### Template

Um [componente](#componente) que é [programaticamente](#programaticamente) transformado em uma página pelo Gatsby.

### Tema

Um tema do Gatsby é como um tema do WordPress que pode ser composto (com outros temas), extensível (com mais lógica) e substituível ([sombreamento](/blog/2019-04-29-component-shadowing/)). Os temas do Gatsby podem ter qualquer aspecto de um aplicativo do Gatsby empacotado dentro deles e também podem oferecer qualquer número de botões para ativar ou desativar os recursos.

### Transformer

Um [plugin](#plugin) que transforma um tipo de dados em outro. Por exemplo, você pode transformar uma planilha em um array [JavaScript](#javascript).

## U

### UI

Uma UI se refere a uma Interface do Usuário. No campo da interação humano-computador, uma UI é um espaço em que ocorrem interações entre humanos e máquinas. O objetivo dessa interação é permitir a operação e o controle efetivo da máquina a partir do lado humano, enquanto a máquina fornece informações simultaneamente que auxiliam no processo de tomada de decisão do usuário (como mensagens de erro ou notificações).

## V

### Variáveis de Ambiente

[Variáveis de ambiente](/docs/environment-variables/) permitem que você personalize o comportamento do seu site ou aplicativo de acordo com o [ambiente](#ambiente) em que ele está sendo utilizado.
Por exemplo, você pode desejar carregar o conteúdo a partir de um CMS de validação (_staging_) durante a etapa de desenvolvimento e conectar com o CMS de produção apenas quando estiver [_buildando_](#build) o seu site.
Utilizando _variáveis de ambiente_ você pode configurar um URL de conexão distinto para cada ambiente.

## W

### [webpack](/docs/glossary/webpack)

Um aplicativo [JavaScript](#javascript) usado pelo Gatsby para agrupar o código do seu site. Isso acontece automaticamente na [construção](#build).

## X

## Y

### Yarn

Um gerenciador de [pacotes](#pacote) que alguns preferem ao [NPM](#npm). Também é necessário para o [desenvolvimento Gatsby](/contributing/setting-up-your-local-dev-environment/#using-yarn).

## Z
