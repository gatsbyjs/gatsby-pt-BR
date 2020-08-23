---
title: "Receitas: Trabalhando com temas"
tableOfContentsDepth: 1
---

Um [tema Gatsby](/docs/themes/what-are-gatsby-themes) junta as configurações Gastby (funcionalidade compartilhadas, design, fontes de dados) em um pacote instalável. Isso significa que configurações e funcionalidades não são criadas diretamente no seu projeto, mas sim versionada, gerenciada de forma centralizada e instalada como uma dependência. De forma parecida você pode atualizar um tema, juntar temas e até mesmo trocar um tema por outro caso estes sejam compatíveis.

## Criando um site novo usando um tema

Encontrou um tema que você gostaria de usar no seu projeto? Maravilha! Você pode configura-lo para o uso a partir dos seguintes passos:

> Caso você queira dar uma olhada nas opções de temas, dê uma olhada nessa [lista de temas](https://www.npmjs.com/search?q=gatsby-theme).

## Pré-requisitos

- Tenha certeza de que você tem o [Gatsby CLI](/docs/gatsby-cli) instalado na sua máquina.

### Direcionamentos

1. Crie um site Gatsby

```shell
gatsby new {nome-do-seu-projeto}
```

2. Entre no diretório do projeto e instale um tema

No exemplo a seguir, o tema utilizado é o `gatsby-theme-blog`. Você pode substituir essa referênca pelo nome do seu tema.

```shell
cd {nome-do-seu-projeto}
npm install gatsby-theme-blog
```

3. Adicione o tema no arquivo `gatsby.config.js`

Siga as instruções encontradas no README do tema que você estiver utilizando e defina as configurações que são requisitadas.


```shell
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        /*
        - basePath defaults to `/`
        - contentPath defaults to `content/posts`
        - assetPath defaults to `content/assets`
        - mdx defaults to `true`
        */
        basePath: `/blog`,
      },
    },
  ],
}
```

4. Execute o comando `gatsby develop`, o tema deve estar disponível em `http://localhost:8000/{caminhoBase}`

> Para aprender como customizar um tema ainda mais, dê uma olhada nos caminhos disponíveis em [documentação do Gatsby-theme-blog](https://www.npmjs.com/package/gatsby-theme-blog).

### Recursos adicionais

- Para aprender a costumizar um tema ainda mais, dê uma olhada no docs ["shadowing" temas Gatsby.](https://www.gatsbyjs.org/docs/themes/shadowing/)]

- Além disso você pode [usar vários temas](https://www.gatsbyjs.org/docs/themes/using-multiple-gatsby-themes/) no seu projeto.

## Criando um site novo usando um starter de temas

Criar um site com um starter que configura temas segue a mesma processo de criar um site com um starter que **não** configura um tema. Nesse exemplo você pode usar o [starter para a criação de um novo site que usa o tema oficial da Gatsby para blogs](https://github.com/gatsbyjs/gatsby-starter-blog-theme).

### Pré-requisitos

- Confira se você tem o [Gatsby CLI](/docs/gatsby-cli) instalado na sua máquina.

### Direcionamentos

1. Cria um novo site com o starter para tema de blogs:

```shell
gatsby new {nome-do-seu-projeto} https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

2. Execute o seu novo site:

```shell
cd {nome-do-seu-projeto}
gatsby develop
```

### Recursos adicionais

- Aprenda a usar um tema Gatsby já existente nesse [pequeno guia conceitual](/docs/themes/using-a-gatsby-theme) ou para mais detalhes confira o [tutorial passo-a-passo](/tutorial/using-a-theme).

## Construindo novos temas

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-the-gatsby-theme-workspace-starter-to-begin-building-a-new-theme"
  lessonTitle="Use o starter de temas de áreas de trabalhos para começar a construir novos temas"
/>

### Pré-requisitos

- Ter o [Gatsby CLI](/docs/gatsby-cli) instalado.

- Ter o [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) instalado.

### Direcionamentos

1. Crie uma área de trabalho para o seu tema usando o [starter da Gatsby de áreas de trabalhos para temas](https://github.com/gatsbyjs/gatsby-starter-theme-workspace):

```shell
gatsby new {nome-do-seu-projeto} https://github.com/gatsbyjs/gatsby-starter-theme-workspace
```

2. Execute o site de exemplo na área de trabalho:

```shell
yarn workspace example develop
```

### Recursos adicionais

- Siga esse [guia mais detalhado](/docs/themes/building-themes/) para a utilização de um starter Gatsby de áreas de trabalho para temas.

- Aprenda como construir seu próprio tema no [curso em vídeo da EggHead sobre Temas Gatsby Autorais](https://egghead.io/courses/gatsby-theme-authoring), ou no [curso em vídeo complementar desse tutorial](/tutorial/building-a-theme).