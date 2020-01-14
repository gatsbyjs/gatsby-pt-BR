---
title: Adicionando Comentários
---

Se você está usando o Gatsby para criar um blog e começou a adicionar algum conteúdo, a próxima coisa a se pensar é como aumentar o engajamento entre os visitantes. Uma ótima maneira de fazer isso é permitir que eles façam perguntas e expressem suas opiniões sobre o que você escreveu. Isso fará com que seu blog pareça muito mais animado para o visitante.

Existem muitas opções para a funcionalidade de adicionar comentários, várias delas direcionadas especificamente para sites estáticos. Embora essa lista não seja muito grande, serve como um bom ponto de partida para ilustrar o que está disponível:

- [Disqus](https://disqus.com)
- [Commento](https://commento.io)
- [Comentários do Facebook](https://www.npmjs.com/package/react-facebook)
- [Staticman](https://staticman.net)
- [JustComments](https://just-comments.com) \([plugin oficial para o Gatsby](https://www.gatsbyjs.org/packages/gatsby-plugin-just-comments/)\)
- [TalkYard](https://www.talkyard.io)
- [Gitalk](https://gitalk.github.io)

Você também pode [desenvolver sua própria ferramenta de comentários](/blog/2019-08-27-roll-your-own-comment-system/), como Tania Rascia escreveu no blog Gatsby.

## Usando o Disqus para comentários

Neste guia, mostraremos como implementar o Disqus em seu blog, pois ele possui vários recursos interessantes.

- É de baixa manutenção, o que significa menos problemas para [moderar seus comentários e manter seu fórum](https://help.disqus.com/moderation/moderating-101).
- O [suporte ao React](https://github.com/disqus/disqus-react) é oficial.
- Oferece um [nível gratuito generoso](https://disqus.com/pricing).
- [Parece ser o serviço mais utilizado](https://www.datanyze.com/market-share/comment-systems/disqus-market-share).
- É mais fácil comentar: o Disqus possui uma grande base de usuários existente e a experiência de integração para novos usuários é rápida. Você pode se registrar com sua conta do Google, Facebook ou Twitter e os usuários podem compartilhar de maneira mais transparente os comentários que escrevem através desses canais.
- A interface de usuário do Disqus tem uma aparência distinta, porém discreta, na qual muitos usuários reconhecem e confiam.
- Todos os componentes do Disqus são _Lazy-Loaded_, o que significa que não afetarão negativamente o tempo de carregamento de suas postagens.

No entanto, lembre-se de que a escolha do Disqus também gera um ponto negativo. Seu site não é mais totalmente estático, dependendo de uma plataforma externa para enviar seus comentários por meio de um `iframe` incorporado em tempo real. Além disso, você deve considerar as implicações de privacidade ao permitir que terceiros armazenem os comentários de seus visitantes e potencialmente rastreiem o comportamento de navegação deles. Você pode consultar a [política de privacidade Disqus](https://help.disqus.com/terms-and-policies/disqus-privacy-policy), as [FAQs sobre privacidade](https://help.disqus.com/terms-and-policies/privacy-faq) (especificamente a última pergunta sobre conformidade com GDPR) e informe seus usuários [como editar suas configurações de compartilhamento de dados](https://help.disqus.com/terms-and-policies/how-to-edit-your-data-sharing-settings).

Se essas preocupações superam os benefícios do Disqus, convém examinar algumas das outras opções acima. Nós incentivamos os _pulls requests_ para expandir este guia com instruções de configuração para outros serviços.

## Implementando o Disqus

![Logo do Disqus](images/disqus-logo.svg)

Aqui estão as etapas para adicionar comentários do Disqus ao seu próprio blog:

1. [Inscreva-se no Disqus](https://disqus.com/profile/signup). Durante o processo, você terá que escolher um nome abreviado para o seu site. É assim que o Disqus identificará os comentários provenientes do seu site. Copie isso para mais tarde.
2. Instale o pacote Disqus React

```shell
npm install disqus-react
```

3. Adicione o nome abreviado da etapa 1 como `GATSBY_DISQUS_NAME` nos seus arquivos `.env` e `.env.example` para que as pessoas que estão participando do seu repositório saibam que precisam fornecer esse valor para que os comentários funcionem. (Você precisa prefixar a variável de ambiente com `GATSBY_` para [disponibilizá-la no código do lado do cliente](https://www.gatsbyjs.org/docs/environment-variables/#client-side-javascript).)

```title=.env.example
# ativa comentários do Disqus para postagens do blog
GATSBY_DISQUS_NAME=insertValue
```

```title=.env
GATSBY_DISQUS_NAME=yourSiteShortname
```

4. No modelo de postagem do seu blog (geralmente `src/templates/post.js`), importe o componente` DiscussionEmbed`.

```js:title=src/templates/post.js
import React from "react"
import { graphql } from "gatsby"
// highlight-next-line
import { DiscussionEmbed } from "disqus-react"
```

Em seguida, defina seu objeto de configuração do Disqus

```js
const disqusConfig = {
  shortname: process.env.GATSBY_DISQUS_NAME,
  config: { identifier: slug, title },
}
```

Onde `identifier` deve ser uma string ou número único que identifique a postagem. Pode ser a _slug_ da publicação, o título ou algum ID. Por fim, adicione `DiscussionEmbed` ao JSX do seu modelo de postagem.

```js:title=src/templates/post.js
return (
  <Global>
    <PageBody>
      {/* highlight-next-line */}
      <DiscussionEmbed {...disqusConfig} />
    </PageBody>
  </Global>
)
```

E você terminou. Agora você deve ver o formulário de comentários do Disqus aparecer abaixo da postagem do seu blog [parecido com este](https://janosh.io/blog/disqus-comments#disqus_thread). Divirta-se com seu blog!

[![Comentários Disqus](images/disqus-comments.png)](https://janosh.io/blog/disqus-comments#disqus_thread)
