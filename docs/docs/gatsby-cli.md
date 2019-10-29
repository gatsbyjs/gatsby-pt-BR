---

title: Commands (Gatsby CLI)

tableOfContentsDepth: 2

---

  

A interface de linha de comandos (ILC) do Gatsby é o primeiro passo para iniciar sua aplicação Gatsby e executar ações como rodar um servidor de desenvolvimento e fazer o build da aplicação antes de publicá-la.

  

_Documentação sobre esse tema também está disponível no [README](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli/README.md),  do gatsby-cliand e a [folha de consulta rápida](/docs/cheat-sheet/) contém os principais comandos da ILC em formato para impressão._

  

## Como utilizar o `gatsby-cli`

  

A ILC do Gatsby (`gatsby-cli`) é distribuída em forma de um pacote executável disponibilizado via [npm](https://www.npmjs.com/) que deve ser instalado globalmente utilizando o comando `npm install -g gatsby-cli`.

  

Utilize o comando `gatsby --help` se precisar de instruções de uso.

  

Outra opção para utilizar o `gatsby-cli` é através de _scripts_ disponívels no arquivo `package.json` que são disponibilizados na maioria dos [starters](/docs/starters/). Por exemplo: para disponibilizar o comando [`gatsby develop`](#develop) em sua aplicação, abra o arquivo `package.json` e adicione o script abaixo:

  

```json:title=package.json

{

"scripts": {

"develop": "gatsby develop"

}

}

```

  

## API 

  

### `new`

  

```

gatsby new [<site-name> [<starter-url>]]

```

  

#### Parâmetros

  

| Parâmetro | Descrição |

| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| site-name | O nome do seu site Gatsby, que será utilizado para nomear o diretório do projeto criado pelo _gatsby-cli_.

| starter-url | URL de um starter do Gatsby. URL. O valor default desse parâmetro é  [gatsby-starter-default](https://github.com/gatsbyjs/gatsby-starter-default); consulte a documentação disponível na página [Starters do Gatsby](/docs/gatsby-starters/) para mais informações. |

  

> Importante: O valor do parâmetro `site-name`  só deve conter letras e números. Se você incluir caracteres como `.`, `./` ou `<space>`, o comando `gatsby new` retornará um erro.

  

#### Exemplos de uso

  

- Criar um site Gatsby de nome `my-awesome-site` utilizando o starter default:

  

```shell

gatsby new my-awesome-site

```

  

- Criar um site de nome `my-awesome-blog-site`, utilizando o starter [gatsby-starter-blog](https://www.gatsbyjs.org/starters/gatsbyjs/gatsby-starter-blog/):

  

```shell

gatsby new my-awesome-blog-site https://github.com/gatsbyjs/gatsby-starter-blog

```

  

- Caso você não especifique ambos os parâmetros, a ILC executará em modo interativo, solicitando as informações necessárias:
  

```shell

gatsby new

? What is your project called? › my-gatsby-project

? What starter would you like to use? › - Use arrow-keys. Return to submit.

❯ gatsby-starter-default

gatsby-starter-hello-world

gatsby-starter-blog

(Use a different starter)

```

  

Consulte a documentação dos [starters do Gatsby](https://www.gatsbyjs.org/docs/gatsby-starters/) para mais detalhes.

  

### Comando `develop`

  
Após a instalação do site Gatsby, acesse o diretório raiz do seu projeto e utilize o comando abaixo para executar o servidor de desenvolvimento:

  

`gatsby develop`

  

#### Opções

  

| Opção | Descrição |

| :-------------: | ----------------------------------------------- |

| `-H`, `--host` | Especifica o host. Default: localhost |

| `-p`, `--port` | Especifica a porta. Default: 8000 |

| `-o`, `--open` | Abre o site no navegador padrão do computador |

| `-S`, `--https` | Executa o servidor em modo HTTPS |

  

Consulte o [guia para HTTPS local](/docs/local-https/) para instruções de como executar um servidor local HTTPS no seu projeto Gatsby.

  

#### Visualizando as alterações que você fez em outros dispositivos

  
Utilize o argumento _host_ do comando _develop_ para acessar o seu ambiente de desenvolvimento em outros dispositivos que esteja conectados na mesma rede: 

```shell

gatsby develop -H 0.0.0.0

```

  
O terminal exibirá o log de informações normalmente mas incluirá também uma URL que você poderá acessar em outro dispositivo conectado à mesma rede para avaliar a renderização do site.

  

```

You can now view gatsbyjs.org in the browser.

⠀

Local: http://0.0.0.0:8000/

On Your Network: http://192.168.0.212:8000/ // highlight-line

```

  

**Note**: O  endereço 0.0.0.0:8000 não pode ser acessado se você está utilizando  Windows (mas você poderá acessar digitando localhost:8000 ou através do atalho "Minha Rede Local" no Windows)

  

### Comando `build`

  
Executado na raiz do site, compile sua aplicação Gatsby e a prepara para distribuição.

  

`gatsby build`

  

#### Opções

  

| Opção | Descrição |

| :--------------------------: | --------------------------------------------------------------------------------------------------------- |

| `--prefix-paths` | Incluir um prefixo no _path_ dos links do site (configure a opção _pathPrefix_ no arquivo _config_ do seu projeto) |

| `--no-uglify` | Faz o _build_ do seu _bundle_ Javascript sem executar etapa de _uglify_ . (útil para modo de debug) |

| `--open-tracing-config-file` | arquivo de configuração para _tracer_(compatível com OpenTracing).  Consulte [Rastreamento de Performance](/docs/performance-tracing/) |

| `--no-color`, `--no-colors` | Desabilita o uso de cores no _output_ do terminal|

  

Além das opções de _build_ acima listadas, exitem [variáveis de ambiente de build](/docs/environment-variables/#build-variables) opcionais disponíveis para uma configuração mais avançada da execução do processo de _build_. Por exemplo, especificando `CI=true` como variável de ambiente permite adaptar o output para [terminais burros](https://en.wikipedia.org/wiki/Computer_terminal#Dumb_terminals).

  

### `serve`

  

Executado na raiz do site, serve a versão de produção do seu site para efeito de teste:

  

`gatsby serve`

  

#### Opcões

  

| Opção | Descrição |

| :--------------: | ---------------------------------------------------------------------------------------- |

| `-H`, `--host` | Especifica o host. Default: localhost |

| `-p`, `--port` | Especifica a porta. Default: 9000 |

| `-o`, `--open` | Abre o site no navegador padrão do computador |

| `--prefix-paths` | Caso seu gatsby-config especifique um atributo `pathPrefix`, o site será servido com esse prefixo aplicado aos links. |

  

### `info`

  
Executado na raiz de um site Gatsby, esse comando disponibiliza informações importantes necessárias quando se está reportando um bug:

  

`gatsby info`

  

#### Opções

  

| Opção | Descrição |

| :-----------------: | ------------------------------------------------------- |

| `-C`, `--clipboard` | Copia informações do ambiente para a área de transferência (clipboard)  |

  

### `clean`

  

Executado na raiz do site, limpa os diretórios _cache_ e _public_:

  

`gatsby clean`

  
Esse comando é útil como um último recurso quando seu projeto local apresenta problemas que levam a crer que o conteúdo do site não está sendo regenerado. Alguns problemas que podem ser resolvidos com essa solução:

This is useful as a last resort when your local project seems to have issues or content does not seem to be refreshing. Issues this may fix commonly include:

  

- Conteúdo desatualizado (por exemplo, arquivos e recursos que não são exibidos ou encontrados)

- Erro de GraphQL. ( por exemplo, esse recurso GraphQL deveria está disponível mas não existe)

- Problemas de dependência como versões inválidas, erros enigmáticos no console, etc.

- Problemas com `plugins`, por exemplo, alterações não aparecem quando se está desenvolvendo um plugin local.

  

### `plugin`

  

Executa comandos referentes a plugins do Gatsby.

  

#### `docs`

  

`gatsby plugin docs`

  

Direciona o usuário à documentação referente a como utilizar e criar _plugins_.
  

### Repl

  

Disponibiliza um REPL (console interativo) do Node.js que contém o contexto da sua aplicação Gatsby. Digite:

  

`gatsby repl`

  

O  REPL do Gatsby solicitará que você insira comandos para explorar os recursos da ferramenta. Quando o seguinte _prompt_ de comando for exibido: `gatsby >`

  

Você poderá inserir comandos como:

  

`babelrc`

  

`components`

  

`dataPaths`

  

`getNodes()`

  

`nodes`

  

`pages`

  

`schema`

  

`siteConfig`

  

`staticQueries`

  

Combinado com o [GraphQL explorer](/docs/introducing-graphiql/), os comandos REPL podem ser muito úteis para ter dar uma visão dos dados de uma aplicação Gatsby.

  

Para mais informações, consulte a [documentação do REPL Gatsby](/docs/gatsby-repl/).

  

### Desabilitando o uso de cores no _output_

  

Além da opção `--no-color` , a ILC  reconhece também a variável de ambiente  `NO_COLOR`  (mais informações em [no-color.org](https://no-color.org/)).