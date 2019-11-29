---
title: Arquivos de API
---

O Gatsby utiliza 4 arquivos na raiz do projeto para configurar o site e controlar o seu comportamento. Todos esses arquivos são opcionais.

- [gatsby-config.js](/docs/api-files-gatsby-config) - Habilita _plugins_, define dados comuns do site, e contém outra configuração do site que se integra à camada de dados GraphQL do Gatsby.
- [gatsby-browser.js](/docs/api-files-gatsby-browser) - Lhe dá controle sobre o comportamento do Gatsby no navegador. Por exemplo, responder quando o usuário altera as rotas, ou chamar uma função quando o usuário abre pela primeira vez qualquer página.
- [gatsby-node.js](/docs/api-files-gatsby-node) - Lhe permite responder a eventos no ciclo de _build_ do Gatsby. Por exemplo, adicionar páginas dinamicamente, editar os nós do GraphQL conforme são criados, ou realizar uma ação após a finalização da _build_.
- [gatsby-ssr.js](/docs/api-files-gatsby-ssr) - Expõe o processo de renderização do lado servidor do Gatsby, assim você pode controlar como ele constrói as páginas HTML.
