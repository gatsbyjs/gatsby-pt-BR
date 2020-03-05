---
title: Gatsby Config API
---

Site configuration options for a Gatsby site are placed in a file at the root of the project folder called `gatsby-config.js`.

_Note: There are many sample configs which may be helpful to reference in the different [Gatsby Example Websites](https://github.com/gatsbyjs/gatsby/tree/master/examples)._

## Configuration options

Options available to set within `gatsby-config.js` include:

1.  [siteMetadata](#sitemetadata) (object)
2.  [plugins](#plugins) (array)
3.  [pathPrefix](#pathprefix) (string)
4.  [polyfill](#polyfill) (boolean)
5.  [mapping](#mapping-node-types) (object)
6.  [proxy](#proxy) (object)
7.  [developMiddleware](#advanced-proxying-with-developmiddleware) (function)

## siteMetadata

When you want to reuse common pieces of data across the site (for example, your site title), you can store that data in `siteMetadata`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Gatsby`,
    siteUrl: `https://www.gatsbyjs.org`,
    description: `Blazing fast modern site generator for React`,
  },
}
```

This way you can store it in one place, and pull it whenever you need it. If you ever need to update the info, you only have to change it here.

See a full description and sample usage in [Gatsby.js Tutorial Part Four](/tutorial/part-four/#data-in-gatsby).

## Plugins

Plugins are Node.js packages that implement Gatsby APIs. The config file accepts an array of plugins. Some plugins may need only to be listed by name, while others may take options (see the docs for individual plugins).

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

See more about [Plugins](/docs/plugins/) for more on utilizing plugins, and to see available official and community plugins.

## pathPrefix

It's common for sites to be hosted somewhere other than the root of their domain. Say you have a Gatsby site at `example.com/blog/`. In this case, you would need a prefix (`/blog`) added to all paths on the site.

```javascript:title=gatsby-config.js
module.exports = {
  pathPrefix: `/blog`,
}
```

See more about [Adding a Path Prefix](/docs/path-prefix/).

## Polyfill

Gatsby uses the ES6 Promise API. Because some browsers don't support this, Gatsby includes a Promise polyfill by default.

If you'd like to provide your own Promise polyfill, you can set `polyfill` to false.

```javascript:title=gatsby-config.js
module.exports = {
  polyfill: false,
}
```

See more about [Browser Support](/docs/browser-support/#polyfills) in Gatsby.

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
    url: "http://examplesite.com/api/",
  },
}
```

See more about [Proxying API Requests in Develop](/docs/api-proxy/).

## Advanced proxying with `developMiddleware`

See more about [adding develop middleware](/docs/api-proxy/#advanced-proxying).
