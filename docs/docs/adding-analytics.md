---
title: Adicionando o Analytics
---

## Por que usar o analytics?

Uma vez que você tem o seu site no ar você vai começar a querer ter uma ideia de quantos visitantes estão chegando ao seu site, juntamente com outras métricas, tais como:

- Quais são as páginas mais populares?
- De onde vêm os meus visitantes?
- Quando é que as pessoas visitam o meu site?

O Google Analytics oferece uma maneira de coletar esses dados e realizar análises sobre eles, respondendo às perguntas acima, entre muitas outras. A plataforma é gratuita para 10 milhões de visitas por mês por ID de acompanhamento. Há outras opções de análise - veja a seção "Outros plugins de Analytics do Gatsby" na parte inferior deste documento para obter mais ideias.

## Configurando o Google Analytics

O primeiro passo é configurar uma conta do Google Analytics. Você pode fazer isso [aqui](https://analytics.google.com/) acessando a partir da sua conta do Google.

O Google também tem uma [página inicial](https://support.google.com/analytics/answer/1008015?hl=pt-BR) para referência.

Uma vez que você tenha uma conta, você será solicitado a configurar uma nova propriedade. Esta propriedade terá um ID de acompanhamento associado a ela. Neste caso, a propriedade será o próprio site. Preencha o formulário com o nome e URL do seu site.

O ID de acompanhamento é o que é usado para identificar dados relacionados ao tráfego do seu site. Normalmente, você usaria um ID de acompanhamento diferente para cada site que estiver monitorando.

Agora você deve ter um ID de acompanhamento; anote-o, pois seu site precisará referenciá-lo ao enviar as visualizações das páginas para o Google Analytics. O ID deve estar no formato `UA-XXXXXXXXX-X`.

Você pode encontrar este ID de acompanhamento mais tarde, indo para `Administração > Informações de acompanhamento > Código de acompanhamento`.

## Usando `gatsby-plugin-google-analytics`

Agora, é hora de configurar o Gatsby para enviar visualizações das páginas para sua conta do Google Analytics.

Vamos usar o `gatsby-plugin-google-analytics`. Para outras opções de analytics (incluindo Google Analytics gtag.js e Google Tag Manager), verifique [outros plugins de Analytics do Gatsby](#outros-plugins-de-analytics-do-gatsby).

```shell
npm install --save gatsby-plugin-google-analytics
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-google-analytics`,
      options: {
        // substitua "UA-XXXXXXXXX-X" pelo seu próprio ID de acompanhamento
        trackingId: "UA-XXXXXXXXX-X",
      },
    },
  ],
}
```

> Observação: Leia mais sobre [gatsby-config.js](/docs/gatsby-config/)

A documentação completa para o plugin pode ser encontrada [aqui](/packages/gatsby-plugin-google-analytics/).

Há um número de opções de configuração extra - tanto com o plugin do Gatsby como também na sua conta do Google Analytics - para que você possa adaptar as coisas para atender às necessidades do seu site.

Uma vez configurado, você pode publicar seu site para testar! Se você navegar para a página inicial do Google Analytics, você deve ver um painel com estatísticas diferentes.

## Outros plugins de Analytics do Gatsby

- [Google Tag Manager](/packages/gatsby-plugin-google-tagmanager/)
- [Google Analytics gtag.js](/packages/gatsby-plugin-gtag/)
- [Segment](/packages/gatsby-plugin-segment-js)
- [Amplitude Analytics](/packages/gatsby-plugin-amplitude-analytics)
- [Fathom](/packages/gatsby-plugin-fathom/)
- [Baidu](/packages/gatsby-plugin-baidu-analytics/)
- [Matomo (formerly Piwik)](/packages/gatsby-plugin-matomo/)
- [Simple Analytics](/packages/gatsby-plugin-simple-analytics)
- [Parse.ly Analytics](/packages/gatsby-plugin-parsely-analytics/)
