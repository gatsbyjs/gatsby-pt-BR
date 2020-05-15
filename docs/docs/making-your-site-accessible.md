---
title: Tornando o seu site acessível
---

A equipe do Gatsby é apaixonada em ajudá-lo a criar sites que funcionem para todos, com padrões úteis que envolvem acessibilidade na Web e otimizações de desempenho. Ao tornar seu site acessível a pessoas com deficiência, você pode criar sites mais inclusivos que removem barreiras e alcançam um maior número de pessoas na Internet.

## O que é acessibilidade?

Nos primórdios da Web, Tim Berners-Lee, inventor da World Wide Web, [disse](https://www.w3.org/Press/IPO-announce):

> "O poder da Web está em sua universalidade.
> O acesso de todos, independentemente da sua deficiência, é um aspecto essencial."

A web de hoje é um recurso importante em muitos aspectos da vida, como assistência médica, educação, comércio. A acessibilidade é um ponto importante a se considerar no desenvolvimento de um site para a web.

[Acessibilidade na Web](https://www.w3.org/WAI/fundamentals/accessibility-intro/#what) significa que sites, ferramentas e tecnologias são projetados e desenvolvidos para que pessoas com deficiência possam usá-los. Mas não são apenas as pessoas com deficiência permanente que se beneficiam. A acessibilidade também beneficia pessoas com deficiências temporárias. Por exemplo, imagine estar em um ambiente em que você não pode ouvir áudio ou não pode usar um computador por causa de um braço quebrado.

A acessibilidade apoia a [inclusão social para todos](https://www.w3.org/standards/webdesign/accessibility#case) e é um forte [caso de negócio](https://www.w3.org/WAI/business-case/).

## O Gatsby te ajuda no desenvolvimento com acessibilidade

Mesmo que no último momento você decida inserir a acessibilidade em seu site, o Gatsby visa fornecer o máximo de recurso necessário pronto para uso.

### Roteamento acessível

Um dos recursos mais comuns de todos os sites é a navegação. As pessoas devem poder navegar pelas suas páginas e conteúdos de maneira intuitiva e acessível.

É por isso que todo site do Gatsby visa oferecer uma experiência de navegação acessível por padrão. Graças ao [@reach/router](https://reach.tech/router), uma biblioteca de roteamento para o React, o Gatsby lida com anúncios de página para leitores de tela em eventos de mudança de página. Estamos ativamente aprimorando essa experiência e [nós agradecemos o seu feedback](/accessibility-statement/).

Desde o [lançamento da segunda versão](/blog/2018-09-17-gatsby-v2/), seus sites Gatsby usam `@reach/router` internamente. Embora testes de acessibilidade adicionais sejam sempre uma boa idéia, o [componente Link do Gatsby](/docs/gatsby-link/) envolve o [componente Link do @reach/router](https://reach.tech/router/api/Link) para melhorar a acessibilidade sem que você precise pensar nisso.

### Gatsby cria páginas HTML por padrão

Para sites, renderizar páginas [HTML estáticas](/docs/glossary#static) significa que o JavaScript não é necessário para acessar e navegar pelo conteúdo. O Gatsby [compila](/docs/glossary#compiler) páginas HTML por padrão a partir dos componentes React usando o [Node.js](/docs/glossary#nodejs). Isso significa que você não precisa se preocupar em configurar a renderização do servidor para dar suporte ao [aprimoramento progressivo](/docs/glossary#progressive-enhancement). Com o suporte estático do Gatsby pronto para o uso, você pode criar sites dinâmicos que ainda permitem o acesso do usuário sem exigir scripts no [lado do cliente](/docs/glossary#client-side).

### Linting com eslint-plugin-jsx-a11y

Com o `eslint-plugin-jsx-a11y` o Gatsby envia pacotes e avisos para todas as suas regras habilitadas por padrão. [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) é uma ferramenta de acessibilidade do tipo [linting](/docs/glossary#linting) para o seu código, que te ajuda a desenvolver projetos Gatsby mais inclusivos ao reduzir o tempo para encontrar erros de acessibilidade. Este plugin te encoraja a incluir o texto alternativo nas tags para imagens, validar o conjunto de atributos especiais [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA), eliminar propriedades redundantes de função, entre outras coisas.

Para saber mais sobre as regras suportadas, veja a documentação do [`eslint-plugin-jsx-a11y`](https://github.com/evcohen/eslint-plugin-jsx-a11y). Você pode personalizar essas regras no seu [`.eslintrc`](/docs/eslint/#configuring-eslint).

```json:title=.eslintrc
{
  "extends": ["react-app", "plugin:jsx-a11y/recommended"],
  "plugins": ["jsx-a11y"],
  "rules": {
    "jsx-a11y/rule-name": "warning"
  }
}
```

Nota: Ao incluir um arquivo local `.eslintrc` este irá [sobrescrever](/docs/eslint/#configuring-eslint) todo o linting padrão do Gatsby e desabilitar a construção `eslint-loader`, o que significa que as suas regras aprimoradas não chegarão no console do seu navegador ou do seu terminal mas as regras serão exibidas se você tiver os plugins ESLint habilitados na sua IDE. Se você deseja alterar esse comportamento e garantir que o `eslint-loader` puxe as suas customizações, você precisa habilitar o loader por conta própria. Uma forma de fazer isso é utilizando o Community plugin [`gatsby-plugin-eslint`](https://www.gatsbyjs.org/packages/gatsby-plugin-eslint/). Além disso, se você ainda quiser aproveitar algum subconjunto do padrão da [Configuração do ESLint fornecida pelo Gatsby](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js), você vai precisar copiá-los para o seu arquivo `.eslintrc` local.

Este é um começo para testar a acessibilidade: [Recomendações adicionais](#como-melhorar-a-acessibilidade) podem ser encontradas abaixo.

## Como melhorar a acessibilidade?

Acessibilidade por padrão é uma vitória para todos. Aqui está um ponto de partida para o teste de acessibilidade ao criar um site ou tema Gatsby:

- [Utilize o seu teclado](https://webaim.org/techniques/keyboard/) para percorrer as páginas. Você consegue alcançar e operar todos os controles alternativos (links, botões, formulários, etc.) e ver um indicador de foco na tela?
- Utilize o [Lighthouse](https://developers.google.com/web/tools/lighthouse/), [axe](https://www.deque.com/axe/) ou [Accessibility Insights](https://accessibilityinsights.io/) para encontrar e corrigir erros comuns de acessibilidade no desenvolvimento
- Teste para [o contraste de cores adequado](https://dequeuniversity.com/tips/color-contrast) com o [seletor de cores acessíveis disponível nas ferramentas de desenvolvimento do Chrome](https://developers.google.com/web/updates/2018/01/devtools#contrast)
- Crie [formulários acessíveis](/docs/building-a-contact-form#creating-an-accessible-form) e inclusivos
- Empregue [headings, landmarks, e estrutura semântica](https://webaim.org/techniques/semanticstructure/) acessíveis
- Inclua [textos alternativos para imagem, video, e audio](https://a11y-style-guide.com/style-guide/section-media.html)
- Teste para [ampliação e zoom da tela](https://axesslab.com/make-site-accessible-screen-magnifiers/)
- Garanta a acessibilidade de [menus interativos, modais e widgets personalizados](https://developer.mozilla.org/en-US/docs/Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets)
- Crie [animações e movimentos](https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity/) seguros
- Escreva [testes de acessibilidade com Cypress](/docs/end-to-end-testing/#writing-tests) para o seu site ou aplicativo

## Recursos de acessibilidade

- [Acessibilidade com React](https://reactjs.org/docs/accessibility.html)
- [O compromisso do Gatsby com a acessibilidade](/blog/2019-04-18-gatsby-commitment-to-accessibility/)
- [Como fazer uma análise de acessibilidade](https://developers.google.com/web/fundamentals/accessibility/how-to-review) do Google Web Fundamentals
- ["Testes rápidos" projetos do A11y](https://a11yproject.com/#Quick-tests)
- [A importância de um teste manual de acessibilidade](https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/) da Smashing Magazine
- [Escrevendo testes automatizados para acessibilidade](https://www.24a11y.com/2017/writing-automated-tests-accessibility/)
- [Curso gratuito de acessibilidade web](https://www.udacity.com/course/web-accessibility--ud891) por Google e Udacity
- [WebAIM introducão](https://webaim.org/intro/) para a acessibilidade web
- [Deque University](https://dequeuniversity.com), com treinamento online gratuito para pessoas com deficiência
- [Web.dev documentação sobre acessibilidade](https://web.dev/accessible)
- [Todos os posts do Gatsby sobre acessibilidade](/blog/tags/accessibility/)
