---
title: Roteamento
---

## Criando rotas

Gatsby facilita o controle programático de suas páginas. Páginas podem ser criadas de três maneiras:

- No arquivo gatsby-node.js de seu site implementando a API [`createPages`](/docs/node-apis/#createPages)
- O Gatsby transforma automaticamente componentes React na pasta `src/pages` em páginas
- Plugins também podem implementar o `createPages` e criar páginas para você

Veja [Criando e Modificando Páginas](/docs/creating-and-modifying-pages) para mais detalhes.

## Vinculação entre rotas

Você pode usar `gatsby-link` para vincular rotas -- isso irá disponibilizar transições de páginas quase instantâneas via _prefetching_. [Veja mais em Gatsby Link](/docs/gatsby-link/).

Você também pode utilizar links normais ( _tag_ `<a>`) para vincular rotas, mas neste caso você não terá o benefício do _prefetching_.

## Criandos links para rotas autenticadas

Se você não deseja que todo seu conteúdo esteja disponível publicamente na web, o Gatsby permite que você crie [rotas "client-only"](/docs/client-only-routes-and-user-authentication) que ficam por trás de uma camada de autenticação.

<GuideList slug={props.slug} />
