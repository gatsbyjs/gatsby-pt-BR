---
title: Interface Node
---

O "`node`" é o centro do sistema de dados do Gatsby. Todos os dados que são adicionados ao Gatsby são modelados usando `nodes`.

## Estrutura de dados de um `node`

A estrutura básica de dados de um `node` é a seguinte:

```flow
id: String,
children: Array[String],
parent: String,
fields: Object,
internal: {
  contentDigest: String,
  mediaType: String,
  type: String,
  owner: String,
  fieldOwners: Object,
  content: String,
}
...outros campos específicos para este tipo de node
```

### `parent`

Uma chave reservada para plugins que desejam estender outros `nodes`.

### `contentDigest`

Campo onde é armazenado um Hash (breve resumo digital) referente ao conteúdo deste `node`, pode ser por exemplo um `md5sum`.

Esse campo deve ser único de acordo com o conteúdo deste `node` pois é usado no armazenamento em cache. O Hash mudará conforme o conteúdo desse `node` for alterado. Há um função auxiliar chamada [createContentDigest](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-core-utils/src/create-content-digest.js) para criar um Hash `md5`.

### `mediaType`

[Tipo de mídia](https://pt.wikipedia.org/wiki/Tipo_de_m%C3%ADdia_da_Internet) opcional que indica aos plugins transformadores que este `node` contém dados que podem ser processados posteriormente.

### `type`

Um tipo de `node` único e global escolhido pelo proprietário do plugin.

### `owner`

O plugin que criou este `node`. Este campo é adicionado pelo próprio gatsby (e não pelo plugin).

### `fieldOwners`

Atributo que armazena a correspondência entre plugins e seus campos criados. Este campo também é adicionado pelo próprio gatsby (e não pelo plugin).

### `content`

Campo opcional que expõe o conteúdo puro desse `node` para plugins transformadores que podem obter e processar posteriormente.

## Plugins de origem (Source plugins)

Novos `nodes` são adicionados ao Gatsby por plugins de origem. Comumente muitos sites do Gatsby usam o [plugin de origem do sistema de arquivos](/packages/gatsby-source-filesystem/) que transforma arquivos do disco em arquivos de `nodes`.

Outros plugins de origem extraem dados para APIs externas, como a da
[Drupal](/packages/gatsby-source-drupal/) e da
[Hacker News](/packages/gatsby-source-hacker-news/).

## Plugins transformadores (Transformer plugins)

Plugins transformadores podem também criar `nodes` transformando `nodes` de origem em novos tipos de `nodes`. Esse comportamento é muito comum quando construímos sites usando o Gatsby para instalar ambos os plugins de origem e os plugins transformados.

`Nodes` criados pelos plugins transformadores são atribuídos como "`children`" de seus `nodes` pais.

- O 
[plugin transformador Remark (da biblioteca Markdown)](/packages/gatsby-transformer-remark/)
procura por novos `nodes` que foram criados com `mediaType` do tipo `text/markdown`
e depois transforma-os em `nodes` `MarkdownRemark` com um campo `html`.

- O [plugin transformador YAML](/packages/gatsby-transformer-yaml/) procura por novos nodes com o tipo de media `text/yaml` (por exemplo. um arquivo `.yaml`) e cria um novo `node` filho YAML analisando a fonte YAML em objetos JavaScript.

## GraphQL

Gatsby automaticamente infere a estrutura dos `nodes` do seu site e cria um esquema GraphQL que você pode consultar a partir dos componentes do seu site.

## Criação de `node`

Para aprender mais sobre como os `nodes` são criados e vinculados, consulte a documentação de [Criação de nós](/docs/node-creation/) na seção "Por trás das cenas".
