---
title: O arquivo da API gatsby-config.js
---

O arquivo `gatsby-config.js` define os metadados do seu website, _plugins_, e outras configurações gerais. Este arquivo deve estar na raiz do seu website Gastby.

Se você criou um website Gatsby com o comando `gatsby new`, já deve existir um arquivo de configuração de exemplo na pasta do seu website.

## Construindo o arquivo de configuração

O arquivo de configuração deve exportar um objeto JavaScript. Dentro deste objeto, você pode definir várias opções de configuração diferentes.

```javascript:title=gatsby-config.js
module.exports = {
  // objeto de configuração
}
```

Um exemplo de arquivo `gatsby-config.js` poderia ser algo do tipo:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Gatsby`,
  },
  plugins: [
    `gatsby-transform-plugin`,
    {
      resolve: `gatsby-plugin-name`,
      options: {
        optionA: true,
        optionB: `Outra opção`,
      },
    },
  ],
}
```

## Opções de configuração

Existem [muitas opções de configuração](/docs/gatsby-config) disponíveis, mas as mais comuns configuram metadados do website e habilitam _plugins_.

### Metadados do website

O objeto `siteMetadata` pode conter qualquer dado que você queira compartilhar em seu website. Um exemplo útil é o título do website. Se você guardar o título em `siteMetadata`, você pode alterá-lo apenas em um único lugar, e ele será atualizado por todo seu website. Para adicionar metadados inclua o objeto `siteMetadata` no seu arquivo de configuração:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Gatsby`,
  },
}
```

Você pode então [acessar o título do website usando GraphQL](/tutorial/part-four/#your-first-graphql-query) de qualquer lugar no seu website.

### _Plugins_

_Plugins_ adicionam novas funcionalidades no seu website Gatsby. Por exemplo, alguns _plugins_ buscam dados de um serviço hospedado, transformam a formatação dos dados, ou redimensionam imagens. A [biblioteca de _plugins_ do Gatsby](/plugins) ajuda você a encontrar o _plugin_ correto para suas necessidades.

Instalar um _plugin_ utilizando um gerenciador de pacotes como o `npm` **não** habilita ele no seu website Gatsby. Para finalizar a adição de um _plugin_ tenha certeza que seu arquivo `gatsby-config.js` contenha o array `plugins`, permitindo então que você possa incluir os _plugins_ necessários para construir o seu website dentro dele:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    // plugins são colocados aqui
  ],
}
```

Quando for adicionar múltiplos _plugins_, eles devem estar separados por vírgulas no array `_plugins_` para ser uma sintaxe válida de JavaScript.

#### _Plugins_ sem opções

Se um _plugin_ não requer quaisquer opções, você pode adicionar o nome dele como uma string no array `_plugins_`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-name`],
}
```

#### _Plugins_ com opções

Vários _plugins_ possuem opções facultativas ou obrigatórias a serem configuradas. Ao invés de adicionar a string do nome no array `_plugins_`, adicione um objeto com o nome do _plugin_ e suas opções. A maior parte dos _plugins_ apresentam exemplos em seu arquivo `README` ou na página da [biblioteca de _plugins_ do Gatsby](/plugins).

Aqui está um exemplo mostrando como escrever um objeto com uma chave `_resolve_` para definir o nome do _plugin_ e uma chave `_options_` para definir um objeto com qualquer configuração aplicável:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-name`,
      options: {
        optionA: true,
        optionB: `Outra opção`,
      },
    },
  ],
}
```

### _Plugins_ mistos

Você pode adicionar _plugins_ com ou sem opções no mesmo array. O arquivo de configuração do seu website poderia ficar assim:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-transform-plugin`,
    {
      resolve: `gatsby-plugin-name`,
      options: {
        optionA: true,
        optionB: `Outra opção`,
      },
    },
  ],
}
```

## Opções de configuração adicionais

Existem várias outras opções de configurações disponíveis para o arquivo `gatsby-config.js`. Você pode encontrar uma lista de cada opção na página [Configuração da API do Gatsby](/docs/gatsby-config/).
