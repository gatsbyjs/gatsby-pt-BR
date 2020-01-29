---
title: Tornando Seu Site Acessível
---

A equipe do Gatsby é apaixonada por ajudá-lo a criar sites que funcionem para todos, com padrões úteis que envolvem acessibilidade na Web, além de otimizações de desempenho. Ao tornar seu site acessível a pessoas com deficiência, você pode criar sites mais inclusivos que alcancem e removam barreiras para mais pessoas na Internet.

## O que é acessibilidade?

Nos primórdios da Web, Tim Berners-Lee, inventor da World Wide Web, [disse](https://www.w3.org/Press/IPO-announce):

> "O poder da Web está em sua universalidade.
> O acesso de todos, independentemente da deficiência, é um aspecto essencial ".

A web de hoje é um recurso importante em muitos aspectos da vida, como assistência médica, educação ou comércio. A acessibilidade é uma consideração importante ao criar para a web.

[Acessibilidade na Web](https://www.w3.org/WAI/fundamentals/accessibility-intro/#what) significa que sites, ferramentas e tecnologias são projetados e desenvolvidos para que pessoas com deficiência possam usá-los. Mas não são apenas as pessoas com deficiência permanente que se beneficiam. A acessibilidade também beneficia pessoas com deficiências temporárias. Por exemplo, imagine estar em um ambiente em que você não pode ouvir áudio ou não pode usar um computador por causa de um braço quebrado.

A acessibilidade apoia a [inclusão social para todos](https://www.w3.org/standards/webdesign/accessibility#case) e tem um forte [argumento de negócios](https://www.w3.org/WAI/business-case/).

## Gatsby ajuda a aumentar a acessibilidade

Embora em última análise caiba a você decidir desenvolver seu site com a acessibilidade em mente, o Gatsby tem como objetivo fornecer o máximo de suporte pronto para uso.

### Roteamento acessível

Um dos recursos mais comuns de todos os sites é a navegação. As pessoas devem poder navegar pelas suas páginas e conteúdo de maneira intuitiva e acessível.

É por isso que todo site do Gatsby pretende ter uma experiência de navegação acessível por padrão. Graças ao [@reach/router](https://reach.tech/router), uma biblioteca de roteamento para o React, o Gatsby lida com anúncios de página para leitores de tela  em eventos de mudança de página. Estamos ativamente aprimorando essa experiência e [seus comentários são bem-vindos](/accessibility-statement/).

Desde o [lançamento da segunda versão](/blog/2018-09-17-gatsby-v2/), seus sites do Gatsby usam `@reach/router` internamente. Embora o teste de acessibilidade adicional seja sempre uma boa idéia, o [Componente Link do Gatsby](/docs/gatsby-link/) envolve o [componente link do @reach/router](https://reach.tech/router/api/Link) para melhorar a acessibilidade sem que você precise pensar nisso.

### Gatsby cria páginas HTML por padrão

For websites, rendering [static HTML](/docs/glossary#static) pages means that JavaScript isn't required to access and navigate through content. Gatsby [compiles](/docs/glossary#compiler) HTML pages by default from React components using [Node.js](/docs/glossary#nodejs), meaning you don't have to worry about setting up server-rendering yourself to support [progressive enhancement](/docs/glossary#progressive-enhancement). With Gatsby's static support out of the box, you can build dynamic sites that still enable user access without requiring [client-side](/docs/glossary#client-side) scripting.

Para sites, renderizar páginas [HTML estáticas](/docs/glossary#static) significa que o JavaScript não é necessário para acessar e navegar pelo conteúdo. O Gatsby [compila](/docs/glossary#compiler) páginas HTML por padrão a partir dos componentes React usando o [Node.js](/docs/glossary#nodejs). Isso significa que você não precisa se preocupar em configurar a renderização do servidor para dar suporte ao [aprimoramento progressivo](/docs/glossary#progressive-enhancement). Com o suporte estático do Gatsby pronto para o uso, você pode criar sites dinâmicos que ainda permitem o acesso do usuário sem exigir scripts no [lado do cliente](/docs/glossary#client-side).

### Linting com eslint-jsx-plugin-a11y

O Gatsby vem com `eslint-config-react-app` por padrão, que inclui o pacote `eslint-jsx-plugin-a11y`. [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) é uma ferramenta de linting de acessibilidade para seu código, ajudando você a desenvolver projetos Gatsby mais inclusivos. Este plugin incentiva você a incluir texto alternativo para _tags_ de imagem, valida _props_ [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) e elimina propriedades redundantes de função, entre outras coisas. É um ponto de partida para testar a acessibilidade: [mais recomendações](#how-to-improve-accessibility) podem ser encontradas abaixo.

A inclusão desse plugin e do [conjunto de regras recomendado](https://github.com/facebook/create-react-app/tree/master/packages/eslint-config-react-app#accessibility-checks) reduz o tempo necessário para implementar a acessibilidade, lembrando você durante o desenvolvimento. As regras ativadas no `eslint-plugin-jsx-a11y` por padrão podem ser [personalizadas em `.eslintrc`](/docs/eslint/#configuring-eslint).

```json:title=.eslintrc
{
  "extends": ["react-app", "plugin:jsx-a11y/recommended"],
  "plugins": ["jsx-a11y"],
  "rules": {
    "jsx-a11y/rule-name": 2
  }
}
```

Para mais informações sobre regras suportadas, consulte a documentação para [`eslint-plugin-jsx-a11y`](https://github.com/evcohen/eslint-plugin-jsx-a11y).

## Como melhorar a acessibilidade?

A acessibilidade por padrão é uma vitória para todos. Aqui está um ponto de partida para o teste de acessibilidade ao criar um site ou tema do Gatsby:

- [Use o teclado](https://webaim.org/techniques/keyboard/) para navegar pelas páginas. Você pode acessar e operar todos os controles interativos (links, botões, inputs de formulário, etc.) e ver um indicador de foco na tela?
- Use [Lighthouse](https://developers.google.com/web/tools/lighthouse/), [axe](https://www.deque.com/axe/) ou [Accessibility Insights](https://accessibilityinsights.io/) para encontrar e corrigir problemas comuns de acessibilidade no desenvolvimento
- Teste o [contraste de cores adequado](https://dequeuniversity.com/tips/color-contrast) com o [seletor de cores de acessibilidade nas Ferramentas de Desenvolvedor do Chrome](https://developers.google.com/web/updates/2018/01/devtools#contrast)
- Crie formulários inclusivos e [acessíveis](/docs/building-a-contact-form#creating-an-accessible-form)
- Empregue [títulos acessíveis, pontos de referência e estrutura semântica](https://webaim.org/techniques/semanticstructure/)
- Incluir [alternativas de imagem, vídeo e texto em áudio](https://a11y-style-guide.com/style-guide/section-media.html)
- Teste de [ampliação e zoom da tela](https://axesslab.com/make-site-accessible-screen-magnifiers/)
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
- [Introdução ao WebAIM](https://webaim.org/intro/) à acessibilidade da Web
- [Universidade Deque](https://dequeuniversity.com), com treinamento on-line gratuito de acessibilidade para pessoas com deficiência
- [Documentação de Acessibilidade do Web.dev](https://web.dev/accessible)
- [Todas as postagens de acessibilidade no blog do Gatsby](/blog/tags/accessibility/)
