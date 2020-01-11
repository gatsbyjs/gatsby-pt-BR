---
title: Como criar um caso de teste minimamente reproduzível
---

## O que é um caso de teste reproduzível?

Um caso de teste reproduzível é um pequeno website construído com Gatsby que demonstre um problema - frequentemente esse problema é causado por um bug no Gatsby ou em um plugin do Gatsby. O seu teste de caso reproduzível deve conter o conjunto mínimo de funcionalidades necessárias para demonstrar o bug claramente.

## Por que você deveria criar um caso de teste reproduzível?

Um caso de teste reproduzível permite que você isole a causa de um problema, o que é o primeiro passo na direção de corrigi-lo!

A [parte mais importante de se reportar um bug](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Bug_writing_guidelines#Writing_precise_steps_to_reproduce) é descrever exatamante os passos necessários para reproduzi-lo.

Um caso de teste reproduzível é uma excelente maneira de compartilhar as condições específicas que causam o bug. Seu caso de teste reproduzível é a melhor maneira de ajudar as pessoas que querem ajudar _você_.

## Passos para criar um caso de teste reproduzível

- Crie um novo website com Gatbsy a partir de um _starter_, o _starter_ oficial `hello-world`  é um excelente exemplo de caso base ou ponto de partida: `gatsby new bug-repro https://github.com/gatsbyjs/gatsby-starter-hello-world`
- Adicione os plugins do Gatsby que estejam relacionados com o problema. Por exemplo, se você estiver tendo problemas com o Gatsby MDX você deve instalar e configurar o [`gatsby-plugin-mdx`](https://www.gatsbyjs.org/packages/gatsby-plugin-mdx/). Apenas adicione os plugins que são necessários para a demonstração do problema.
- Adicione o código necessário para recriar o erro que você observou.
- Publique o código (a sua conta do GitHub é um bom lugar para fazer isso) e então adicione o link para ele quando estiver [_criando uma issue_](/contributing/how-to-file-an-issue/).

## Locais para desenvolver um caso de teste reproduzível

- Localmente com um _starter_: Você pode começar com um [_starter_](/docs/starters) localmente para então fazer um build na sua própria máquina. Os _starters_ oficiais do Gatsby [`hello-world`](https://github.com/gatsbyjs/gatsby/tree/master/starters/hello-world) ou [`default`](https://github.com/gatsbyjs/gatsby-starter-default) ambos são boas bases para um caso de teste reproduzível.
- Hospede no CodeSandbox: Você pode desenvolver um website com Gatsby diretamente do seu navegador com o CodeSandbox usando o [template Gatsby](https://codesandbox.io/s/github/gatsbyjs/gatsby-starter-default) deles. CodeSandbox também hospeda o seu website automaticamente, o que pode ser útil para demonstrar o comportamento do seu site.

## Benefícios de um caso de teste reproduzível

- Menor superfície de contato: Ao remover tudo, menos o erro, faz com que você não tenha que cavar para encontrar o bug.
- Não há necessidade de publicar código privado: Talvez você não consiga publicar o seu website principal (por diversas razões). Recriar uma pequena parte dele como um caso de teste reproduzível permite que você demonstre publicamente o problema sem expor qualquer código privado.
- Prova da existência do bug: Algumas vezes um bug é causado por alguma combinação de configurações na sua máquina. Um caso de teste reproduzível permite que os contribuidores baixem o seu build e testem ele em suas máquinas também. Isso ajuda a verificar e restringir a causa do problema.
- Receba ajuda para corrigir o seu bug: Se outra pessoa consegue reproduzir o problema, normalmente ela tem uma boa chance de corrigi-lo. É quase impossível corrigir um bug sem primeiro conseguir reproduzi-lo.
