---
title: API de configuração do Gatsby
---

As opções de configurações para um site Gatsby são colocadas em um arquivo na raiz do projeto chamado `gatsby-config.js`.

_Anotações: Existem muitas amostras de configurações que podem ser úteis para referenciar em diferentes [Exemplos de Websites Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/examples)._

## Opções de Configurações

Opções disponíveis para configurar dentro do `gatsby-config.js` incluem:

1.  [siteMetadata](#sitemetadata) (object)
2.  [plugins](#plugins) (array)
3.  [pathPrefix](#pathprefix) (string)
4.  [polyfill](#polyfill) (boolean)
5.  [mapping](#mapping-node-types) (object)
6.  [proxy](#proxy) (object)
7.  [developMiddleware](#advanced-proxying-with-developmiddleware) (function)

## siteMetadata

Quando você quer reutilizar alguns pedaços comuns através do site (por exemplo, o título do site), você pode armazenar estes dados em `siteMetadata`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Gatsby`,
    siteUrl: `https://www.gatsbyjs.org`,
    description: `Gerador de site moderno e veloz para React`,
  },
}
```

Desta forma, você pode armazenar em um único local e puxar isto sempre que precisar. Se você sempre precisar atualizar as informações, você somente tem que mudar aqui.

Veja a descrição completa e exemplo de uso em [Tutorial Gatsby.js Parte Quatro](/tutorial/part-four/#data-in-gatsby).

## Plugins

Plugins são pacotes Node.js que implementam APIs do Gatsby. O arquivo de configurações aceita um array de plugins. Alguns plugins podem ser listados somente pelo nome, enquanto outros podem precisar de opções (veja a documentação para plugins individuais).

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-react-helmet`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `docs`,
        path: `${__dirname}/../docs/`,
      },
    },
  ],
}
```

Veja mais sobre [Plugins](/docs/plugins/) para saber mais como utilizá-los, além de conferir os plugins oficiais e os feitos pela comunidade.

## pathPrefix

É comum sites serem hospedados em algum outro local que não seja domínio raiz. Quando dizemos que temos um site Gatsby em `example.com/blog/`. Nesse caso, precisamos de um prefixo (`/blog`) adicionado para todos os caminhos no site.

```javascript:title=gatsby-config.js
module.exports = {
  pathPrefix: `/blog`,
}
```

Veja mais sobre [Adicionar um Prefixo de Caminho](/docs/path-prefix/).

## Polyfill

Gatsby usa a API do ES6 Promise. Pelo fato de alguns navegadores não suportarem isso, o Gatsby inclui uma _Promise_ polyfill por padrão.

Se você desejar fornecer sua própria _Promise_ polyfill, você pode configurar o `polyfill` como _false_.

```javascript:title=gatsby-config.js
module.exports = {
  polyfill: false,
}
```

Veja mais sobre [Suporte de Navegadores](/docs/browser-support/#polyfills) em Gatsby.

## Mapeando tipos de nó

O Gatsby inclui um recurso avançado que permite criar "mappings" entre os tipos de nós.

> Anotações: Gatsby v2.2 introduziu uma nova maneira de criar relações de chave estrangeira entre os tipos de nós com [o `@link` Extensão de campo GraphQL](/docs/schema-customization/#foreign-key-fields).

Por exemplo, imagine que você tem um blog em markdown com vários autores no qual deseja "vincular" cada postagem do blog às informações do autor armazenadas em um arquivo yaml chamado `author.yaml`:

```markdown
---
title: Uma publicação no blog
author: Kyle Mathews
---

Um tratado sobre a eficácia do bezoar no tratamento de envenenamento por pesticidas agrícolas.
```

```yaml:title=author.yaml
- id: Kyle Mathews
  bio: Fundador @ GatsbyJS. Gosta de tecnologia, leitura/escrita, fundando coisas. Blogs em bricolage.io.
  twitter: "@kylemathews"
```
Você pode mapear entre o campo do `author` em `frontmatter` para o id nos objetos `author.yaml` adicionando ao seu `gatsby-config.js`:

```javascript
module.exports = {
  plugins: [...],
  mapping: {
    "MarkdownRemark.frontmatter.author": `AuthorYaml`,
  },
}
```

Pode ser necessário instalar o transformador de arquivo apropriado (neste caso [YAML](/packages/gatsby-transformer-yaml/)) e configurar o [gatsby-source-filesystem](/packages/gatsby-source-filesystem/) adequadamente para que o Gatsby pegue os arquivos de mapeamento. Isso se aplica a outros tipos de arquivos mencionados posteriormente neste segmento também.

Gatsby usa esse mapeamento ao criar um schema GraphQL para permitir a consulta de dados de ambas as fontes. 

```graphql
query($slug: String!) {
  markdownRemark(fields: { slug: { eq: $slug } }) {
    html
    fields {
      slug
    }
    frontmatter {
      title
      author {
        # Este é um link para o objeto autor
        id
        bio
        twitter
      }
    }
  }
}
```

O mapeamento também pode ser usado para mapear um array de ids para qualquer outra coleção de dados. Por exemplo, se você tiver dois arquivos JSON `experience.json` e `tech.json` da seguinte maneira:

```json:title=experience.json
[
  {
    "id": "companyA",
    "company": "Company A",
    "position": "Unicorn Developer",
    "from": "Dec 2016",
    "to": "Present",
    "items": [
      {
        "label": "Responsibility",
        "description": "Being an unicorn"
      },
      {
        "label": "Hands on",
        "tech": ["REACT", "NODE"]
      }
    ]
  }
]
```

```json:title=tech.json
[
  {
    "id": "REACT",
    "icon": "facebook",
    "color": "teal",
    "label": "React"
  },
  {
    "id": "NODE",
    "icon": "server",
    "color": "green",
    "label": "NodeJS"
  }
]
```

E você adiciona a seguinte regra ao seu `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [...],
  mapping: {
    'ExperienceJson.items.tech': `TechJson`
  },
}
```

Você pode consultar o objeto `tech` por meio dos ids mencionados na `experience`:

```graphql
query {
  experience: allExperienceJson {
    edges {
      node {
        company
        position
        from
        to
        items {
          label
          description
          link
          tech {
            label
            color
            icon
          }
        }
      }
    }
  }
}
```

O mapeamento também funciona entre arquivos Markdown. Por exemplo, em vez de ter todos os autores em um arquivo YAML, você pode ter informações sobre cada autor em um arquivo Markdown separado:

```markdown
---
author_id: Kyle Mathews
twitter: "@kylemathews"
---

Fundador @ GatsbyJS. Gosta de tecnologia, leitura/escrita, fundando coisas. Blogs em bricolage.io.
```

E adicione a seguinte regra ao seu `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [...],
  mapping: {
    'MarkdownRemark.frontmatter.author': `MarkdownRemark.frontmatter.author_id`
  },
}
```

De maneira semelhante aos arquivos YAML e JSON, o mapeamento entre arquivos Markdown também pode ser usado para mapear um array de ids.

## Proxy

Definir a opção de configuração do proxy informará o servidor de desenvolvimento para realizar proxy de qualquer solicitação desconhecida endereçada a um servidor especificado. Por exemplo:

```javascript:title=gatsby-config.js
module.exports = {
  proxy: {
    prefix: "/api",
    url: "http://examplesite.com/api/"
  }
}
```

Veja mais sobre [Proxying API Requests em desenvolvimento](/docs/api-proxy/).

## Proxy avançado com `developMiddleware`

Veja mais sobre [como adicionar middleware desenvolvido](/docs/api-proxy/#advanced-proxying).
