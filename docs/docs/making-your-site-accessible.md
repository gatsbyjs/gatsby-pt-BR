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

<!-- ### Linting with eslint-plugin-jsx-a11y

Gatsby ships with the `eslint-plugin-jsx-a11y` package and warnings for all of its rules enabled by default. [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) is an accessibility [linting](/docs/glossary#linting) tool for your code, helping you develop more inclusive Gatsby projects by reducing the time to find accessibility errors. This plugin encourages you to include alternative text for image tags, validates [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) props, and eliminates redundant role properties, among other things.

For more on supported rules, check out the docs for [`eslint-plugin-jsx-a11y`](https://github.com/evcohen/eslint-plugin-jsx-a11y). You can customize those rules in your [`.eslintrc`](/docs/eslint/#configuring-eslint). -->

```json:title=.eslintrc
{
  "extends": ["react-app", "plugin:jsx-a11y/recommended"],
  "plugins": ["jsx-a11y"],
  "rules": {
    "jsx-a11y/rule-name": "warning"
  }
}
```

<!-- Note: Including a local `.eslintrc` file will [override](/docs/eslint/#configuring-eslint) all of Gatsby's default linting and disable the built-in `eslint-loader`, meaning your tweaked rules won't make it to your browser's developer console or your terminal window but will still be displayed if you have ESLint plugins enabled in your IDE. If you would like to change this behavior and make sure the `eslint-loader` pulls in your customizations, you'll need to enable the loader yourself. One way to do this is by using the Community plugin [`gatsby-plugin-eslint`](https://www.gatsbyjs.org/packages/gatsby-plugin-eslint/). Additionally, if you would still like to take advantage of some subset of the default [ESLint config Gatsby ships with](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js), you'll need to copy them manually to your local `.eslintrc` file. -->

This is a start to testing for accessibility: [further recommendations](#how-to-improve-accessibility) can be found below.

## Como melhorar a acessibilidade?

A acessibilidade por padrão é uma vitória para todos. Aqui está um ponto de partida para o teste de acessibilidade ao criar um site ou tema Gatsby:

- [Use o teclado](https://webaim.org/techniques/keyboard/) para navegar pelas páginas. Você pode acessar e operar todos os controles interativos (links, botões, inputs de formulário, etc.) e ver um indicador de foco na tela?
- Use [Lighthouse](https://developers.google.com/web/tools/lighthouse/), [axe](https://www.deque.com/axe/) ou [Accessibility Insights](https://accessibilityinsights.io/) para encontrar e corrigir problemas comuns de acessibilidade no desenvolvimento
- Teste o [contraste de cores adequado](https://dequeuniversity.com/tips/color-contrast) com o [seletor de cores de acessibilidade nas Ferramentas de Desenvolvedor do Chrome](https://developers.google.com/web/updates/2018/01/devtools#contrast)
- Crie formulários inclusivos e [acessíveis](/docs/building-a-contact-form#creating-an-accessible-form)
- Empregue [títulos acessíveis, pontos de referência e estrutura semântica](https://webaim.org/techniques/semanticstructure/)
- Inclua [alternativas de imagem, vídeo e texto em áudio](https://a11y-style-guide.com/style-guide/section-media.html)
- Teste a [ampliação e zoom da tela](https://axesslab.com/make-site-accessible-screen-magnifiers/)
- Garanta a acessibilidade de [menus interativos, modais e widgets personalizados](https://developer.mozilla.org/en-US/docs/Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets)
- Crie [animações e movimentos](https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity/) seguros
- Escreva [testes de acessibilidade Cypress](/docs/end-to-end-testing/#writing-tests) para o seu site ou aplicativo

## Recursos de acessibilidade

- [Acessibilidade no React](https://reactjs.org/docs/accessibility.html)
- [O compromisso do Gatsby com a acessibilidade](/blog/2019-04-18-gatsby-commitment-to-accessibility/)
- [Como fazer uma revisão de acessibilidade](https://developers.google.com/web/fundamentals/accessibility/how-to-review) nos Fundamentos da Web do Google
- [Testes rápidos do projeto A11y](https://a11yproject.com/#Quick-tests)
- [A importância do teste de acessibilidade manual](https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/) da Smashing Magazine
- [Escrevendo testes automatizados para acessibilidade](https://www.24a11y.com/2017/writing-automated-tests-accessibility/)
- [Curso gratuito de acessibilidade na web](https://www.udacity.com/course/web-accessibility--ud891) pelo Google e Udacity
- [Introdução ao WebAIM](https://webaim.org/intro/) para acessibilidade da Web
- [Universidade Deque](https://dequeuniversity.com), com treinamento online gratuito de acessibilidade para pessoas com deficiência
- [Documentação de Acessibilidade do Web.dev](https://web.dev/accessible)
- [Todas as postagens de acessibilidade no blog do Gatsby](/blog/tags/accessibility/)
