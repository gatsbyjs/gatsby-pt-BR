---
title: Roteamento
---

Parte do que torna os sites feitos com Gatsby tão rápidos, é que quase todo o trabalho é feito durante a compilação, fazendo com que durante a execução, os sites usem principalmente [conteúdo estático](/docs/adding-app-and-website-functionality/#static-pages). Durante este processo, o Gatsby cria caminhos para acessar esse conteúdo, gerenciando [as rotas](/docs/glossary#routing) pra você. Navegar em um aplicativo Gatsby necessita de conhecimento sobre o que são esses caminhos e como eles são gerados.

Além disso, sua aplicação pode ter funcionalidades que não podem ser gerenciadas durante a compilação ou através da [reidratação](/docs/adding-app-and-website-functionality/#how-hydration-makes-apps-possible). Incluindo coisas como autenticação ou requisitar conteúdo dinâmico. Para gerenciar essas páginas, você pode usar [rotas apenas no lado do cliente](/docs/client-only-routes-and-user-authentication), utilizando [`@reach/router`](/docs/reach-router-and-gatsby/) que está incorporado ao Gatsby.

## Criando rotas

Gatsby facilita o controle programático de suas páginas. Páginas podem ser criadas de três maneiras:

- No arquivo gatsby-node.js de seu site, implementando a API [`createPages`](/docs/node-apis/#createPages)
- O Gatsby transforma automaticamente componentes React na pasta `src/pages` em páginas
- Plugins também podem implementar o `createPages` e criar páginas para você

Veja [Criando e Modificando Páginas](/docs/creating-and-modifying-pages) para mais detalhes.

Quando o Gatsby cria páginas, automaticamente gera os caminhos para acessá-las. Esse caminho será diferente dependendo de como a página foi criada.

### Páginas criadas em `src/pages`

Cada arquivo `.js` dentro do diretório `src/pages`, vai gerar sua própria página do site. O caminho para estas páginas corresponde a estrutura dos arquivos desta pasta.

Por exemplo, o arquivo `contato.js` é encontrado no endereço `seusite.com/contato`, e o arquivo `home.js` em `seusite.com/home`. Funciona assim para qualquer nível em que o arquivo for criado. Se `contato.js` for movido para o diretório `informacao`, localizado em `src/pages`, a página agora será acessada em `seusite.com/informacao/contato`.

Existe uma exceção para esta regra, que é qualquer arquivo nomeado como `index.js`. Estes arquivos correspondem ao diretório raíz em que estão localizados. Isso significa que, um `index.js` na raíz da pasta `src/pages`, é encontrado em `seusite.com`. Porém, se existe um `index.js` dentro do diretório `informacao`, será encontrado em `seusite.com/informacao`. 

Note que se o arquivo `index.js` não existir em algum diretório, a página raíz também não existirá, e qualquer tentativa de acesso será redirecionada para a [página 404](/docs/add-404-page/). Por exemplo, `seusite.com/informacao/contato` pode existir, mas isso não garante que `seusite.com/informacao` exista. 

### Páginas criadas com `createPages`

Outro jeito de criar páginas é no arquivo `gatsby-node.js` usando a API `createPage`. Quando as páginas são criadas desta forma, o caminho é definido de maneira explícita. Por exemplo:

```js:title=gatsby-node.js
createPage({
  path: "/routing",
  component: routing,
  context: {},
})
```
Para mais informações, visite a [documentação da API `createPage`](/docs/actions/#createPage)

## Rotas conflitantes

Como existem diversas maneiras de criar uma página, diferentes plugins, temas, ou trechos de código no arquivo `gatsby-node` podem acidentalmente criar múltiplas páginas com o mesmo caminho. Quando isso acontece, o Gatsby irá mostrar um aviso durante a compilação, mas o site ainda vai compilar com sucesso. Nessa situação, a página que foi compilada por último será a única acessível dentre as conflitantes. Alterar qualquer caminho conflitante para produzir URLs únicas deve solucionar o problema.

## Rotas aninhadas

Se o seu objetivo é definir caminhos que tem múltiplos níveis, como `portfolio/arte/item1`, isso pode ser feito diretamente ao criar páginas, como mencionado em [Criando rotas](#criando-rotas)

Como alternativa, se você quiser criar páginas que vão mostrar diferentes componentes dependendo do caminho na URL (como uma barra lateral específica), o Gatsby pode gerenciar isso a nível de página usando [layouts](/docs/layout-components/).

## Link entre rotas

Para criar links entre as páginas, você pode usar [`gatsby-link`](/docs/gatsby-link/). Com o `gatsby-link` você tem [benefícios no desempenho](#desempenho-e-prefetching), que estão incorporados ao componente.

Também é possível navegar entre páginas usando a tag padrão `<a>`, mas você não vai ter os benefícios do prefetching nesse caso.

## Criandos links para rotas autenticadas

Para páginas que tratam dados sensíveis, ou outro comportamento dinâmico, você pode gerenciar esses dados no lado do servidor. Gatsby te permite criar [rotas apenas no lado do cliente](/docs/client-only-routes-and-user-authentication), atrás de um bloqueio de autenticação, garantindo que os dados fiquem disponíveis apenas a usuários autorizados.

## Desempenho e Prefetching

A fim de melhorar o desempenho, o Gatsby procura por todos os links que aparecem na página atual para fazer prefetching. Antes mesmo do usuário clicar em um link, o Gatsby já começou a requisitar a página que ele aponta. [Aprenda mais sobre prefetching](/docs/how-code-splitting-works/#prefetching-chunks).

<GuideList slug={props.slug} />
