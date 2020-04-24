---
title: Tornando Seu Site Acessível
---

A equipe do Gatsby é apaixonada por ajudá-lo a criar sites que funcionem para todos implementando por _default_ recursos para criação de sites acessíveis e otimização de desempenho. Ao tornar seu site acessível a pessoas com deficiência, você pode criar sites mais inclusivos que alcancem e removam barreiras para um maior número de pessoas na Internet.

## O que é acessibilidade?

Nos primórdios da Web, Tim Berners-Lee, inventor da World Wide Web, [disse](https://www.w3.org/Press/IPO-announce):

> "O poder da Web está em sua universalidade.
> O acesso de todos, independentemente da deficiência, é um aspecto essencial."

A web de hoje é um recurso importante em muitos aspectos da vida, como assistência médica, educação ou comércio. A acessibilidade é uma consideração importante ao criar para a web.

[Acessibilidade na Web](https://www.w3.org/WAI/fundamentals/accessibility-intro/#what) significa que sites, ferramentas e tecnologias são projetados e desenvolvidos para que pessoas com deficiência possam usá-los. Mas não são apenas as pessoas com deficiência permanente que se beneficiam. A acessibilidade também beneficia pessoas com deficiências temporárias. Por exemplo, imagine estar em um ambiente em que você não pode ouvir áudio ou não pode usar um computador por causa de um braço quebrado.

A acessibilidade apoia a [inclusão social para todos](https://www.w3.org/standards/webdesign/accessibility#case) e tem um forte [argumento de negócios](https://www.w3.org/WAI/business-case/).

## Gatsby ajuda a implementar acessibilidade

Embora em última análise caiba a você decidir desenvolver seu site com a acessibilidade em mente, o Gatsby tem como objetivo fornecer o máximo de suporte pronto para uso.

### Roteamento acessível

Um dos recursos mais comuns de todos os sites é a navegação. As pessoas devem poder navegar pelas suas páginas e conteúdos de maneira intuitiva e acessível.

É por isso que todo site do Gatsby pretende ter uma experiência de navegação acessível por padrão. Graças ao [@reach/router](https://reach.tech/router), uma biblioteca de roteamento para o React, o Gatsby lida com anúncios de página para leitores de tela em eventos de mudança de página. Estamos ativamente aprimorando essa experiência e [seus comentários são bem-vindos](/accessibility-statement/).

Desde o [lançamento da segunda versão](/blog/2018-09-17-gatsby-v2/), seus sites Gatsby usam `@reach/router` internamente. Embora o teste de acessibilidade adicional seja sempre uma boa idéia, o [Componente Link do Gatsby](/docs/gatsby-link/) envolve o [componente link do @reach/router](https://reach.tech/router/api/Link) para melhorar a acessibilidade sem que você precise pensar nisso.

### Gatsby cria páginas HTML por padrão

Para sites, renderizar páginas [HTML estáticas](/docs/glossary#static) significa que o JavaScript não é necessário para acessar e navegar pelo conteúdo. O Gatsby [compila](/docs/glossary#compiler) páginas HTML por padrão a partir dos componentes React usando o [Node.js](/docs/glossary#nodejs). Isso significa que você não precisa se preocupar em configurar a renderização do servidor para dar suporte ao [aprimoramento progressivo](/docs/glossary#progressive-enhancement). Com o suporte estático do Gatsby pronto para o uso, você pode criar sites dinâmicos que ainda permitem o acesso do usuário sem exigir scripts no [lado do cliente](/docs/glossary#client-side).

### Linting with eslint-plugin-jsx-a11y

Gatsby ships with the `eslint-plugin-jsx-a11y` package and warnings for all of its rules enabled by default. [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) is an accessibility [linting](/docs/glossary#linting) tool for your code, helping you develop more inclusive Gatsby projects by reducing the time to find accessibility errors. This plugin encourages you to include alternative text for image tags, validates [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) props, and eliminates redundant role properties, among other things.

For more on supported rules, check out the docs for [`eslint-plugin-jsx-a11y`](https://github.com/evcohen/eslint-plugin-jsx-a11y). You can customize those rules in your [`.eslintrc`](/docs/eslint/#configuring-eslint).

```json:title=.eslintrc
{
  "extends": ["react-app", "plugin:jsx-a11y/recommended"],
  "plugins": ["jsx-a11y"],
  "rules": {
    "jsx-a11y/rule-name": "warning"
  }
}
```

Note: Including a local `.eslintrc` file will [override](/docs/eslint/#configuring-eslint) all of Gatsby's default linting and disable the built-in `eslint-loader`, meaning your tweaked rules won't make it to your browser's developer console or your terminal window but will still be displayed if you have ESLint plugins enabled in your IDE. If you would like to change this behavior and make sure the `eslint-loader` pulls in your customizations, you'll need to enable the loader yourself. One way to do this is by using the Community plugin [`gatsby-plugin-eslint`](https://www.gatsbyjs.org/packages/gatsby-plugin-eslint/). Additionally, if you would still like to take advantage of some subset of the default [ESLint config Gatsby ships with](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js), you'll need to copy them manually to your local `.eslintrc` file.

This is a start to testing for accessibility: [further recommendations](#how-to-improve-accessibility) can be found below.

## How to improve accessibility?

Accessibility by default is a win for everyone. Here's a starting point for accessibility testing when making a Gatsby site or theme:

- [Use your keyboard](https://webaim.org/techniques/keyboard/) to tab through the pages. Can you reach and operate every interactive control (links, buttons, form inputs, etc.) and see a focus indicator on the screen?
- Use [Lighthouse](https://developers.google.com/web/tools/lighthouse/), [axe](https://www.deque.com/axe/) or [Accessibility Insights](https://accessibilityinsights.io/) to find and fix common accessibility issues in development
- Test for [adequate color contrast](https://dequeuniversity.com/tips/color-contrast) with the [accessibility color picker in Chrome Developer Tools](https://developers.google.com/web/updates/2018/01/devtools#contrast)
- Create inclusive and [accessible forms](/docs/building-a-contact-form#creating-an-accessible-form)
- Employ accessible [headings, landmarks, and semantic structure](https://webaim.org/techniques/semanticstructure/)
- Include [image, video, and audio text alternatives](https://a11y-style-guide.com/style-guide/section-media.html)
- Test for [screen magnification and zoom](https://axesslab.com/make-site-accessible-screen-magnifiers/)
- Ensure accessibility of [interactive menus, modals, and custom widgets](https://developer.mozilla.org/en-US/docs/Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets)
- Create safe [animations and motion](https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity/)
- Write [Cypress accessibility tests](/docs/end-to-end-testing/#writing-tests) for your site or application

## Accessibility resources

- [React accessibility](https://reactjs.org/docs/accessibility.html)
- [Gatsby’s commitment to accessibility](/blog/2019-04-18-gatsby-commitment-to-accessibility/)
- [How to do an accessibility review](https://developers.google.com/web/fundamentals/accessibility/how-to-review) from Google Web Fundamentals
- [A11y Project's Quick Tests](https://a11yproject.com/#Quick-tests)
- [The importance of manual accessibility testing](https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/) from Smashing Magazine
- [Writing Automated Tests for Accessibility](https://www.24a11y.com/2017/writing-automated-tests-accessibility/)
- [Free web accessibility course](https://www.udacity.com/course/web-accessibility--ud891) by Google and Udacity
- [WebAIM introduction](https://webaim.org/intro/) to web accessibility
- [Deque University](https://dequeuniversity.com), with free online accessibility training for people with disabilities
- [Web.dev accessibility docs](https://web.dev/accessible)
- [All Gatsby accessibility blog posts](/blog/tags/accessibility/)
