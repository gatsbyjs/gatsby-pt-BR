---
title: Criando um Plugin de Transformação
---

Existem dois tipos de _plugins_ que funcionam com o sistema de dados do Gatsby, os _plugins_ de fonte de dados ("_source_") e os _plugins_ de transformação ("_transformer_").

- **Source** _plugins_, ou _plugins_ de fonte de dados, proveem informação de uma fonte remota ou local para o que o Gatsby chama de [nós](/docs/node-interface/).
- **Transformer** _plugins_, ou _plugins_ de transformação, "transformam" informação provida por _source plugins_ para novos nós e/ou para campos dos nós.

O objetivo deste documento é:

1. Definir o que é um _plugin_ de transformação do Gatbsy, e
2. Acompanhar uma reimplementação simplificada de um _plugin_ existente para demonstrar como criar um _plugin_ de transformação.

## O que _plugins_ de transformação fazem?

_Plugins_ de transformação "transformam" dados de um tipo para outro tipo. Você frequentemente usará ambos os plugins de fonte de dados e os plugins de transformação no seu website feito com Gatsby.

Esse acoplamento flexível entre os _plugins_ de fonte de dados e de transformação permitem que os desenvolvedores que usam Gatsby montem rapidamente _pipelines_ de transformação de dados complexos com pouco trabalho.

## Como criar um _plugin_ de transformação?

Assim como o _plugin_ de fonte dados, o _plugin_ de transformação é um pacote NPM normal. Ele possui um arquivo `package.json` com dependências opcionais assim como um arquivo `gatsby-node.js` onde você implementa as APIs Node.js do Gatsby.

`gatsby-transformer-yaml` é um _plugin_ de transformação que procura por novos nós com o _media type_ igual a _text/yaml_ (e.g. um arquivo .yaml) e cria novo(s) nó(s) filho(s) do tipo YAML através da análise do arquivo fonte YAML em objetos JavaScript.

Confira este exemplo de reconstrução simplificada de um `gatsby-transformer-yaml` diretamente em um website. Digamos que você tenha um site inicial padrão do Gatsby que inclua um arquivo `src/data/example.yml`:

```yaml:title=src/data/example.yml
- name: Jane Doe
  bio: Desenvolvedor residente de  Somewhere, USA
- name: John Smith
  bio: Desenvolvedor residente de  Maintown, USA
```

### Verifique que os dados estão sendo providos

Primeiro, no `gatsby-config.js`, use o _plugin_ `gatsby-source-filesystem` para criar nós de arquivo.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `./src/data/`,
      },
    },
  ],
}
```

Eles estão expostos no seu esquema graphql, que você pode consultar:

```graphql
query {
  allFile {
    edges {
      node {
        internal {
          type
          mediaType
          description
          owner
        }
      }
    }
  }
}
```

Agora você tem um nó de arquivo para trabalhar:

```json
{
  "data": {
    "allFile": {
      "edges": [
        {
          "node": {
            "internal": {
              "contentDigest": "c1644b03f380bc5508456ce91faf0c08",
              "type": "File",
              "mediaType": "text/yaml",
              "description": "File \"src/data/example.yml\"",
              "owner": "gatsby-source-filesystem"
            }
          }
        }
      ]
    }
  }
}
```

### Transformando nós do tipo `text/yaml`

Agora, transforme os nós de arquivo recém-criados, conectando-os à API `onCreateNode` em `gatsby-node.js`.

Se você estiver acompanhando a partir de um projeto exemplo, instale os seguintes pacotes:

```shell
npm install --save js-yaml lodash
```

Agora, no `gatsby-node.js`:

```javascript:title=gatsby-node.js
const jsYaml = require(`js-yaml`)

async function onCreateNode({ node, loadNodeContent }) {
  // somente faça log para nós de mediaType igual a `text/yaml`
  if (node.internal.mediaType !== `text/yaml`) {
    return
  }

  const content = await loadNodeContent(node)
  const parsedContent = jsYaml.load(content)
}

exports.onCreateNode = onCreateNode
```

Conteúdo do arquivo:

```text
- id: Jane Doe
  bio: Desenvolvedor residente de  Somewhere, USA
- id: John Smith
  bio: Desenvolvedor residente de  Maintown, USA
```

Conteúdo YAML analisado:

```javascript
;[
  {
    id: "Jane Doe",
    bio: "Desenvolvedor residente de   Somewhere, USA",
  },
  {
    id: "John Smith",
    bio: "Desenvolvedor residente de   Maintown, USA",
  },
]
```

Agora você escreverá uma função auxiliar para transformar o conteúdo YAML analisado em novos nós do Gatsby:

```javascript
function transformObject(obj, id, type) {
  const yamlNode = {
    ...obj,
    id,
    children: [],
    parent: node.id,
    internal: {
      contentDigest: createContentDigest(obj),
      type,
    },
  }
  createNode(yamlNode)
  createParentChildLink({ parent: node, child: yamlNode })
}
```

Acima, você cria um objeto `yamlNode` com o formato esperada pelo [`createNode`] (/docs/actions/#createNode).

Então você cria um link entre o nó pai (arquivo) e o nó filho (conteúdo do yaml).

No seu `gatsby-node.js` atualizado, você irá percorrer o conteúdo do YAML analisado, usando a função auxiliar para transformar cada parte num novo nó:

```javascript:title=gatsby-node.js
const jsYaml = require(`js-yaml`)
const _ = require(`lodash`)

async function onCreateNode({
  node,
  actions, // highlight-line
  loadNodeContent,
  createNodeId, // highlight-line
  createContentDigest, // highlight-line
}) {
  // highlight-start
  function transformObject(obj, id, type) {
    const yamlNode = {
      ...obj,
      id,
      children: [],
      parent: node.id,
      internal: {
        contentDigest: createContentDigest(obj),
        type,
      },
    }

    createNode(yamlNode)
    createParentChildLink({ parent: node, child: yamlNode })
  }
  // highlight-end

  const { createNode, createParentChildLink } = actions

  if (node.internal.mediaType !== `text/yaml`) {
    return
  }

  const content = await loadNodeContent(node)
  const parsedContent = jsYaml.load(content)

  // highlight-start
  parsedContent.forEach((obj, i) => {
    transformObject(
      obj,
      obj.id ? obj.id : createNodeId(`${node.id} [${i}] >>> YAML`),
      _.upperFirst(_.camelCase(`${node.name} Yaml`))
    )
  })
  // highlight-end
}

exports.onCreateNode = onCreateNode
```

Agora você pode consultar seus novos nós que contêm nossos dados do YAML transformados:

```graphql
query {
  allExampleYaml {
    edges {
      node {
        id
        name
        bio
      }
    }
  }
}
```

```json
{
  "data": {
    "allExampleYaml": {
      "edges": [
        {
          "node": {
            "id": "3baa5e64-ac2a-5234-ba35-7af86746713f",
            "name": "Jane Doe",
            "bio": "Desenvolvedor residente de   Somewhere, USA"
          }
        },
        {
          "node": {
            "id": "2c733815-c342-5d85-aa3f-6795d0f25909",
            "name": "John Smith",
            "bio": "Desenvolvedor residente de   Maintown, USA"
          }
        }
      ]
    }
  }
}
```

Confira o [código fonte completo](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-transformer-yaml/src/gatsby-node.js) do `gatsby-transformer-yaml`.

## Usando a cache

Às vezes transformar propriedades custa tempo e recursos. Para evitar recriar essas propriedades a cada execução, você pode aproveitar o mecanismo de _cache_ global fornecido por Gatsby.

As chaves de cache devem conter pelo menos o contentDigest do nó em questão. Por exemplo, o `gatsby-transformer-remark` usa a seguinte chave de _cache_ para o nó html:

```javascript:title=extend-node-type.js
const htmlCacheKey = node =>
  `transformer-remark-markdown-html-${node.internal.contentDigest}-${pluginsCacheStr}-${pathPrefixCacheStr}`
```

Acessar e configurar o conteúdo na _cache_ é tão simples quanto:

```javascript:title=extend-node-type.js
const cachedHTML = await cache.get(htmlCacheKey(markdownNode))

cache.set(htmlCacheKey(markdownNode), html)
```
