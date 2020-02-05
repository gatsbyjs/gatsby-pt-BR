---
title: Compartilhando Componentes Entre Sites
issue: https://github.com/gatsbyjs/gatsby/issues/14042
---

Um dos benefícios de várias equipes usarem o Gatsby em sua organização é a capacidade de compartilhar componentes do React em sites diferentes.

Existem várias estratégias aqui.

**Bibliotecas de componentes** são uma abordagem mais limpa e pura, mas geralmente precisam de ferramentas adicionais ou fazem com que algumas mudanças exijam vários _pull requests_.

Como alternativa, as equipes podem implementar **sistemas para descoberta de componentes**, como o [Storybook](https://github.com/storybookjs/storybook) ou [Styleguidist](https://github.com/styleguidist/react-styleguidist ), por site e simplesmente copie e cole o código desejado nos repositórios.

Para evitar copiar e colar e reutilizar componentes, você pode usar as **ferramentas de compartilhamento de componentes** como [Bit](https://github.com/teambit/bit) para reutilizar e sincronizar componentes entre sites.

<GuideList slug={props.slug} />

--

**Nota:** você tem alguma ideia adicional sobre o compartilhamento de componentes entre sites? Agradecemos com sua contribuição para os documentos de Gatsby. Descubra [como contribuir](/contributing/docs-contributions/).
