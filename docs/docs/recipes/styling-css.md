---
title: "Recipes: Styling with CSS"
tableOfContentsDepth: 1
---

There are so many ways to add styles to your website; Gatsby supports almost every possible option, through official and community plugins.

## Using global CSS files without a Layout component

### Prerequisites

- An existing [Gatsby site](/docs/quick-start/) with an index page component
- A `gatsby-browser.js` file

### Directions

1. Create a global CSS file as `src/styles/global.css` and paste the following into the file:

```css:title=src/styles/global.css
html {
  background-color: lavenderblush;
}

p {
  color: maroon;
}
```

2. Import the global CSS file in the `gatsby-browser.js` file such as the following:

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"
```

> **Note:** You can also make use of `require('./src/styles/global.css')` to import the global CSS file in your `gatsby-config.js` file.

3. Run `gatsby-develop` to observe the global styling being applied across your site.

> **Note:** This approach is not the best fit if you are using CSS-in-JS for styling your site, in which case a layout page with all the shared components should be used. This is covered in the next recipe.

### Additional resources

- More on [adding global styles without a layout component](/docs/global-css/#adding-global-styles-without-a-layout-component)

## Using global styles in a layout component

### Prerequisites

- A [Gatsby site](/docs/quick-start/) with an index page component

### Directions

You can add global styles to a [shared layout component](/tutorial/part-three/#your-first-layout-component). This component is used for things that are common throughout the site, like a header or footer.

1. If you don't already have one, create a new directory in your site at `/src/components`.

2. Inside the components directory, create two files: `layout.css` and `layout.js`.

3. Add the following to `layout.css`:

```css:title=/src/components/layout.css
body {
  background: red;
}
```

4. Edit `layout.js` to import the CSS file and output layout markup:

```jsx:title=/src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

5. Now edit your site's homepage at `/src/pages/index.js` and use the new layout component:

```jsx:title=/src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

### Additional resources

- [Standard Styling with Global CSS Files](/docs/global-css/)
- [More about layout components](/tutorial/part-three)

## Using Styled Components

### Prerequisites

- A [Gatsby site](/docs/quick-start/) with an index page component
- [gatsby-plugin-styled-components, styled-components, and babel-plugin-styled-components](/packages/gatsby-plugin-styled-components/) installed in `package.json`

### Directions

1. Inside your `gatsby-config.js` file add `gatsby-plugin-styled-components`

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

2. Open the index page component (`src/pages/index.js`) and import the `styled-components` package

3. Style components by creating style blocks for each element type

4. Apply to the page by including styled components in the JSX

```jsx:title=src/pages/index.js
import React from "react"
import styled from "styled-components" //highlight-line

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const Avatar = styled.img`
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const User = props => (
  <>
    <Avatar src={props.avatar} alt={props.username} />
    <Username>{props.username}</Username>
  </>
)

export default () => (
  <Container>
    <h1>About Styled Components</h1>
    <p>Styled Components is cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
    />
  </Container>
)
```

4. Run `gatsby develop` to see the changes

### Additional resources

- [More on Using Styled Components](/docs/styled-components/)
- [Egghead lesson](https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components)

## Using CSS Modules

### Prerequisites

- An existing [Gatsby site](/docs/quick-start/) with an index page component

### Directions

1. Create a CSS module as `src/pages/index.module.css` and paste the following into the module:

```css:title=src/pages/index.module.css
.feature {
  margin: 2rem auto;
  max-width: 500px;
}
```

2. Import the CSS module as a JSX object `style` in the `index.js` file by modifying the page so it looks like the following:

```jsx:title=src/pages/index.js
import React from "react"

// highlight-start
import style from "./index.module.css"

export default () => (
  <section className={style.feature}>
    <h1>Using CSS Modules</h1>
  </section>
)
// highlight-end
```

3. Run `gatsby develop` to see the changes.

**Note:**
Notice that the file extension is `.module.css` instead of `.css`, which tells Gatsby that this is a CSS module.

### Additional resources

- More on [Using CSS Modules](/tutorial/part-two/#css-modules)
- [Live example on Using CSS modules](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-css-modules)

## Using Sass/SCSS

Sass is an extension of CSS that gives you more advanced features like nested rules, variables, mixins, and more.

Sass has 2 syntaxes. The most commonly used syntax is "SCSS", and is a superset of CSS. That means all valid CSS syntax, is valid SCSS syntax. SCSS files use the extension `.scss`

Sass will compile `.scss` and `.sass` files to `.css` files for you, so you can write your stylesheets with more advanced features.

### Prerequisites

- A [Gatsby site](/docs/quick-start/).

### Directions

1. Install the Gatsby plugin [gatsby-plugin-sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/) and `node-sass`.

`npm install --save node-sass gatsby-plugin-sass`

2. Include the plugin in your `gatsby-config.js` file.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

3.  Write your stylesheets as `.sass` or `.scss` files and import them. If you don't know how to import styles, take a look at [Styling with CSS](/docs/recipes/#2-styling-with-css)

```css:title=styles.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css:title=styles.sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```javascript
import "./styles.scss"
import "./styles.sass"
```

_Note: You can use Sass/SCSS files as modules too, like mentioned in the previous recipe about CSS modules, with the difference that instead of `.css` the extensions have to be `.scss` or `.sass`_

### Additional resources

- [Difference between .sass and .scss](https://responsivedesign.is/articles/difference-between-sass-and-scss/)
- [Sass guide from the official Sass website](https://sass-lang.com/guide)
- [A more complete installation tutorial on Sass with some more explanations and more resources](https://www.gatsbyjs.org/docs/sass/)

## Adding a Local Font

### Prerequisites

- A [Gatsby site](/docs/quick-start/)
- A font file: `.woff2`, `.ttf`, etc.

### Directions

1. Copy a font file into your Gatsby project, such as `src/fonts/fontname.woff2`.

```text
src/fonts/fontname.woff2
```

2. Import the font asset into a CSS file to bundle it into your Gatsby site:

```css:title=src/css/typography.css
@font-face {
  font-family: "Font Name";
  src: url("../fonts/fontname.woff2");
}
```

**Note:** Make sure the font name is referenced from the relevant CSS, e.g.:

```css:title=src/components/layout.css
body {
  font-family: "Font Name", sans-serif;
}
```

By targeting the HTML `body` element, your font will apply to most text on the page. Additional CSS can target other elements, such as `button` or `textarea`.

If fonts are not updating following steps above, make sure to replace the existing font-family in relevant CSS.

### Additional resources

- More on [importing assets into files](/docs/importing-assets-into-files/)

## Using Emotion

[Emotion](https://emotion.sh) is a powerful CSS-in-JS library that supports both inline CSS styles and styled components. You can use each styling feature individually or together in the same file.

### Prerequisites

- A [Gatsby site](/docs/quick-start)

### Directions

1. Install the [Gatsby Emotion plugin](/packages/gatsby-plugin-emotion/) and Emotion packages.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

2. Add the `gatsby-plugin-emotion` plugin to your `gatsby-config.js` file:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

3. If you don't already have one, create a page in your Gatsby site at `src/pages/emotion-sample.js`.

Import Emotion's `css` core package. You can then use the `css` prop to add [Emotion object styles](https://emotion.sh/docs/object-styles) to any element inside a component:

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import { css } from "@emotion/core"

export default () => (
  <div>
    <p
      css={{
        background: "pink",
        color: "blue",
      }}
    >
      This page is using Emotion.
    </p>
  </div>
)
```

4. To use Emotion's [styled components](https://emotion.sh/docs/styled), import the package and define them using the `styled` function.

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import styled from "@emotion/styled"

const Content = styled.div`
  text-align: center;
  margin-top: 10px;
  p {
    font-weight: bold;
  }
`

export default () => (
  <Content>
    <p>This page is using Emotion.</p>
  </Content>
)
```

### Additional resources

- [Using Emotion in Gatsby](/docs/emotion/)
- [Emotion website](https://emotion.sh)
- [Getting started with Emotion and Gatsby](https://egghead.io/lessons/gatsby-getting-started-with-emotion-and-gatsby)

## Using Google Fonts

Hosting your own [Google Fonts](https://fonts.google.com/) locally within a project means they won't have to be fetched over the network when your site loads, increasing your site's speed index by up to ~300 milliseconds on desktop and 1+ seconds on 3G. It's also recommended to limit custom font usage to only the essential for performance.

### Prerequisites

- A [Gatsby site](/docs/quick-start)
- The [Gatsby CLI](/docs/gatsby-cli/) installed
- Choosing a font package from [the typefaces project](https://github.com/KyleAMathews/typefaces)

### Directions

1. Run `npm install --save typeface-your-chosen-font`, replacing `your-chosen-font` with the name of the font you want to install from [the typefaces project](https://github.com/KyleAMathews/typefaces).

An example to load the popular 'Source Sans Pro' font would be: `npm install --save typeface-source-sans-pro`.

2. Add `import "typeface-your-chosen-font"` to a layout template, page component, or `gatsby-browser.js`.

```jsx:title=src/components/layout.js
import "typeface-your-chosen-font"
```

3. Once it's imported, you can reference the font name in a CSS stylesheet, CSS Module, or CSS-in-JS.

```css:title=src/components/layout.css
body {
  font-family: "Your Chosen Font";
}
```

_NOTE: So for the above example, the relevant CSS declaration would be `font-family: 'Source Sans Pro';`_

### Additional resources

- [Typography.js](/docs/typography-js/) - Another option for using Google fonts on a Gatsby site
- [The Typefaces Project Docs](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Live example on Kyle Mathews' blog](https://www.bricolage.io/typefaces-easiest-way-to-self-host-fonts/)
