---
title: API de configuração do Gatsby
---

As opções de configuração para um site Gatsby são colocados em um arquivo na raiz do projeto chamado `gatsby-config.js`.
Anotações: Existe muitos exemplos de configurações qual pode ser útil referenciar em diferentes Exemplos de Websites gatsby.
_Anotações: Existe muitos exemplos de configurações qual pode ser útil referenciar em diferentes [Exemplos de Websites Gatsby ](https://github.com/gatsbyjs/gatsby/tree/master/examples)._

## Opções de Configuração

Opções disponiveis para configurar dentro do `gatsby-config.js` incluí:

1.  [siteMetadata](#sitemetadata) (object)
2.  [plugins](#plugins) (array)
3.  [pathPrefix](#pathprefix) (string)
4.  [polyfill](#polyfill) (boolean)
5.  [mapping](#mapping-node-types) (object)
6.  [proxy](#proxy) (object)
7.  [developMiddleware](#advanced-proxying-with-developmiddleware) (function)

## siteMetadata

Quando você quer reusar alguns pedaços comum através do site( por exemplo, seu título do site), você pode armazenar estes dados em `siteMetadata`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Gatsby`,
    siteUrl: `https://www.gatsbyjs.org`,
    description: `Gerador de site moderno e veloz para React`,
  },
}
```

Desta forma você pode armazenar em um único local e puxar isto sempre que precisar, se você sempre precisar atualizar as informações, você somente tem que mudar aqui.
Veja a descrição completa e exemplo de uso em Gatsby.js Tutorial Parte 4

Desta forma você pode armazenar em um único local e puxar isto sempre que precisar, se você sempre precisar atualizar as informações, você somente tem que mudar aqui.

Veja a descrição completa e exemplo de uso em [Tutorial Gatsby.js Parte Quatro](/tutorial/part-four/#data-in-gatsby).

## Plugins

Plugins são pacotes Node.js que implementam APIs do Gatsby. As Arquivos de configurações aceitos em um array de plugins. Alguns plugins pode ser listados somente pelo nome, enquanto outros pode precisar de opções(veja a documentação para plugins individuais).

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

Veja mais sobre [Plugins](/docs/plugins/) para saber mais como utilizar plugins, e ver plugins oficiais disponíveis e plugins da comunidade.

## pathPrefix

É comum sites ser hospedado em algum outro local que não seja dominio raiz.Quando dizemos que temos um Gatsby site em `example.com/blog/`. Nesse caso, precisamos de um prefixo (`/blog`) adicionado a todas caminhos no site.

```javascript:title=gatsby-config.js
module.exports = {
  pathPrefix: `/blog`,
}
```

Veja mais sobre [Adicionar um Prefixo de Caminho](/docs/path-prefix/).

## Polyfill

Gatsby usa a API do ES6 Promise. Pelo fato de alguns navegadores não suportam isso, o Gatsby inclui um polyfill Promise por padrão.

Se você desejar fornecer seu próprio polyfill Promise, você pode configurar o `polyfill` como false.

```javascript:title=gatsby-config.js
module.exports = {
  polyfill: false,
}
```

Veja mais sobre [Suporte de Navegadores](/docs/browser-support/#polyfills) em Gatsby.

## Mapping node types

Gatsby includes an advanced feature that lets you create "mappings" between node types.

> Note: Gatsby v2.2 introduced a new way to create foreign-key relations between node types with [the `@link` GraphQL field extension](/docs/schema-customization/#foreign-key-fields).

For instance, imagine you have a multi-author markdown blog where you want to "link" from each blog post to the author information stored in a yaml file named `author.yaml`:

```markdown
---
title: A blog post
author: Kyle Mathews
---

A treatise on the efficacy of bezoar for treating agricultural pesticide poisoning.
```

```yaml:title=author.yaml
- id: Kyle Mathews
  bio: Founder @ GatsbyJS. Likes tech, reading/writing, founding things. Blogs at bricolage.io.
  twitter: "@kylemathews"
```

You can map between the `author` field in `frontmatter` to the id in the `author.yaml` objects by adding to your `gatsby-config.js`:

```javascript
module.exports = {
  plugins: [...],
  mapping: {
    "MarkdownRemark.frontmatter.author": `AuthorYaml`,
  },
}
```

You may need to install the appropriate file transformer (in this case [YAML](/packages/gatsby-transformer-yaml/)) and set up [gatsby-source-filesystem](/packages/gatsby-source-filesystem/) properly for Gatsby to pick up the mapping files. This applies to other file types later mentioned in this segment as well.

Gatsby then uses this mapping when creating the GraphQL schema to enable you to query data from both sources:

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
        # This now links to the author object
        id
        bio
        twitter
      }
    }
  }
}
```

Mapping can also be used to map an array of ids to any other collection of data. For example, if you have two JSON files
`experience.json` and `tech.json` as follows:

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

And then add the following rule to your `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [...],
  mapping: {
    'ExperienceJson.items.tech': `TechJson`
  },
}
```

You can query the `tech` object via the referred ids in `experience`:

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

Mapping also works between Markdown files. For example, instead of having all authors in a YAML file, you could have info about each author in a separate Markdown file:

```markdown
---
author_id: Kyle Mathews
twitter: "@kylemathews"
---

Founder @ GatsbyJS. Likes tech, reading/writing, founding things. Blogs at bricolage.io.
```

And then add the following rule to your `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [...],
  mapping: {
    'MarkdownRemark.frontmatter.author': `MarkdownRemark.frontmatter.author_id`
  },
}
```

Similarly to YAML and JSON files, mapping between Markdown files can also be used to map an array of ids.

## Proxy

Setting the proxy config option will tell the develop server to proxy any unknown requests to your specified server. For example:

```javascript:title=gatsby-config.js
module.exports = {
  proxy: {
    prefix: "/api",
    url: "http://examplesite.com/api/"
  }
};
```

See more about [Proxying API Requests in Develop](/docs/api-proxy/).

## Advanced proxying with `developMiddleware`

See more about [adding develop middleware](/docs/api-proxy/#advanced-proxying).
