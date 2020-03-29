---
title: Gatsby Starters
---

A CLI do Gatsby permite instalar **starters**, que são bases para sites Gatsby mantidos pela comunidade e projetados para partir ao desenvolvimento rapidamente.

## Instalando starters

Execute o comando `gatsby new` para clonar a base de um starter, instalar suas dependências, e limpar o histórico Git.

### Usando URLs de repositório Git

Ao criar um novo site Gatsby, você pode opcionalmente especificar um starter para basear seu novo site; eles podem vir de qualquer repositório Git disponível publicamente, como GitHub, GitLab ou Bitbucket. Você pode fornecer a `[URL_DO_REPOSITORIO_GIT_DO_STARTER]` diretamente:

```shell
gatsby new [DIRETORIO_DO_SITE] [URL_DO_REPOSITORIO_GIT_DO_STARTER]
```

Por exemplo, para criar um site em uma pasta `blog` com o Gatsby Starter Blog da sua URL do GitHub:

```shell
gatsby new blog https://github.com/gatsbyjs/gatsby-starter-blog
```

Isso baixa os arquivos e inicializa o site executando `npm install`. 

### Usando nomes de usuário e repositórios GitHub em vez de URLs

Como alternativa, você pode também pode fornecer um nome de usuário e repositório GitHub:

```shell
gatsby new [DIRETORIO_DO_SITE] [NOME_DE_USUARIO_NO_GITHUB/REPOSITORIO]
```

Aqui temos um exemplo utilizando esse formato `[NOME_DE_USUARIO_NO_GITHUB/REPOSITORIO]`:

```shell
gatsby new blog gatsbyjs/gatsby-starter-blog
```

Isso também baixa os arquivos e inicializa o site executando `npm install`.

Se você não especificar um starter, seu site será criado a partir do [starter padrão](https://github.com/gatsbyjs/gatsby-starter-default).


> **Observação:** Se você trabalha para um empresa de nível corporativo onde não tem permissão para fazer pull de repositórios públicos, você ainda pode configurar o Gatsby. Confira a [documentação para saber mais](/docs/setting-up-gatsby-without-gatsby-new/).

### Usando um starter local

Outra opção é fornecer um caminho (relativo ou absoluto) para uma pasta local que contém um starter:

```shell
gatsby new [DIRETORIO_DO_SITE] [CAMINHO_LOCAL_PARA_O_STARTER]
```

Aqui está um exemplo, assumindo que existe um starter no caminho `./Code/my-local-starter`:

```shell
gatsby new blog ./Code/my-local-starter
```

## Starters oficiais

Starters oficiais são mantidos pelo Gatsby.

| Starter                                                                              | Demo                                                         | Caso de uso                                | Contém                           |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ | -------------------------------- |
| [gatsby-starter-default](https://github.com/gatsbyjs/gatsby-starter-default)         | [Demo](https://gatsby-starter-default-demo.netlify.com/)     | Apropriado para a maioria dos casos de uso | Site padrão em Gatsby            |
| [gatsby-starter-blog](https://github.com/gatsbyjs/gatsby-starter-blog)               | [Demo](https://gatsby-starter-blog-demo.netlify.com/)        | Criar um blog simples                      | Postagens e listagens de um blog |
| [gatsby-starter-hello-world](https://github.com/gatsbyjs/gatsby-starter-hello-world) | [Demo](https://gatsby-starter-hello-world-demo.netlify.com/) | Aprender Gatsby                            | O essencial e básico do Gatsby   |

## Criando starters

Aprenda [como fazer um starter](/docs/creating-a-starter/) na documentação do Gatsby. Starters podem ser criados apenas para seu time ou distribuídos para a comunidade em geral. Só depende de você!

## Starters da comunidade

Starters da comunidade são criados e mantidos por membros da comunidade Gatsby.

- Buscando por um starter para um caso de uso específico? Procure nos starters que foram enviados a [Biblioteca Starter](/starters/).
- Criou um starter que gostaria de compartilhar? Siga [estes passos para enviar seu starter](/contributing/submit-to-starter-library/) a Biblioteca Starter.
