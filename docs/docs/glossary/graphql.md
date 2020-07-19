---
title: GraphQL
disableTableOfContents: true
---

## O que é GraphQL?

GraphQL é uma linguagem de consulta para requisitar informações de uma [API](/docs/glossary#api), e um protocolo para servidores que a suportam. GraphQL é um dos caminhos que você pode importar dados dentro de seus componentes no Gatsby.

O Facebook criou o GraphQL em 2012 quando percebeu que precisava de uma API capaz de suportar aplicativos Web e móveis nativos. A empresa liberou o GraphQL com uma licença de código aberto em 2015.

As APIs mais tradicionais usam um endpoint separado para cada parte ou tipo de dados que você queira requisitar. Por exemplo, uma API de jornal pode conter:

- `/articles/<id>` endpoint que retorna uma nova notícia específica;
- `/reporters/<id>` endpoint que retorna informações sobre um reporter em particular.

Uma única página de artigo de notícias pode exigir duas requisições separadas: uma para requisitar os dados da matéria e outro para os detalhes de contato do repórter. Além do mais o endpoint `/reporters` pode retornar mais dados do que você deseja mostrar. Pode retornar sua biografia e redes sociais, quando o que você apenas deseja mostrar é seu o nome, email e foto.

Uma API GraphQL, por outro lado, possui um único endpoint. Para requisitar dados, você envia um texto como requisição que utiliza a sintaxe específica do GraphQL. O GraphQL executa as funções necessárias para trazer os dados que você requisitou e retorna um simples JSON.

A requisição de um artigo e seu repórter se parece com o exemplo a seguir.

```graphql
{
  article(id: '7fdc2787469b') {
    title
    body
    reporter(id: '64669b3f') {
      name
      email
      photo
    }
  }
}
```

E nesse retorno contém apenas o que você requisitou.

```json
{
  "data": {
    "article": {
      "title": "Gatsby promove adoção do GraphQL",
      "body": "...",
      "reporter": {
        "name": "Jane Gatsby",
        "email": "janereports@example.com",
        "photo": "images/reporters/janegatsby.jpg"
      }
    }
  }
}
```

Você não precisa usar o GraphQL junto ao Gatsby, portanto o GraphQL oferece algumas vantagens a mais do que outras formas de importação de dados.

- Você pode requisitar apenas os dados que deseja ver.
- Você pode adicionar novos tipos de dados e recursos sem precisar criar um novo endpoint.
- Você pode armazenar conteúdo da forma que faz sentido em teu site, se estiver em um banco de dados, CMS de terceiros ou arquivos de texto em Markdown.

## Aprenda mais

- [GraphQL & Gatsby](/docs/graphql/)

- [Por que Gatsby usa GraphQL](/docs/why-gatsby-uses-graphql/)

- [GraphQL](https://graphql.org) site oficial

- [How to GraphQL](https://www.howtographql.com/)
