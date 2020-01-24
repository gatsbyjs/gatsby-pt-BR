---
title: Utilizando o GraphQL Playground
---

## Introdução

Nessa página nós queremos lhe apresentar uma alternativa ao IDE atual para as suas consultas com GraphQL: [GraphQL Playground](https://github.com/prisma/graphql-playground).

## O que é GraphQL Playground?

O GraphQL Playground é uma maneira de você interagir com os dados que as suas fontes e plugins adicionam como esquemas. Você irá interagir muito com esses dados e o Playground o ajudará muito na exploração deles.

## Acessando o playground

Para acessar essa funcionalidade experimental utilizando o GraphQL Playground com Gatsby, adicione `GATSBY_GRAPHQL_IDE` no script `develop`  em seu `package.json`, desta forma:

```
"develop": "GATSBY_GRAPHQL_IDE=playground gatsby develop",
```

Use `npm run develop` ao invés de `gatsby develop` e acesse-o quando o servidor de desenvolvimento estiver rodando em `https://localhost:8000/___graphql`

Para ainda conseguir usar o `gatsby develop` você precisaria do pacote dotenv no seu arquivo gatsby-config.js e adicionar um [arquivo de variáveis](/docs/environment-variables/), normalmente chamado de `.env.development`. E por fim, adicionar `GATSBY_GRAPHQL_IDE=playground` ao arquivo `.env.development`.

![Uma imagem que indica onde encontrar o esquema GraphQl](images/playground-schema.png)
