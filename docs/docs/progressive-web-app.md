---
title: Progressive Web Apps (PWAs)
---

## O que é uma Progressive Web App?

Aplicação da Web Progressiva do inglês "Progressive web app" (PWA) é um termo geral para a nova filosofia de criação de sites e um termo específico com um conjunto estabelecido de três requisitos explícitos, testáveis e padronizados.

Como um termo geral, a abordagem do PWA é caracterizada por empenhar-se em satisfazer o [seguinte conjunto de atributos](https://infrequently.org/2015/06/progressive-apps-escaping-tabs-without-losing-our-soul/):

1.  Responsividade
2.  Conectividade Independente
3.  Interações App-like
4.  Moderno
5.  Segurança
6.  Detectável
7.  Re-engajável
8.  Instalável
9.  Linkavel

Como um termo específico, para serem classificadas como PWA os sites podem ser testados conforme os seguintes [três critérios de base](https://infrequently.org/2016/09/what-exactly-makes-something-a-progressive-web-app/):

1.  Deve ser executado sob protocolo HTTPS.
2.  Deve incluir o Web App Manifest.
3.  Deve implementar um service worker.

As PWAs são apps derivadas da web (contrariamente às aplicações nativas, que são empacotadas e implatadas através de lojas de aplicativos). Como o Alex Russell, que juntamente com o Francês Berriman [cunhou o termo PWA](https://infrequently.org/2015/06/progressive-apps-escaping-tabs-without-losing-our-soul/), disse:

> são apenas sites que tomaram todas as vitaminas certas.

## Como um site da Gatsby é um Aplicativo da Web Progressivo?

O Gatsby foi projetado para fornecer desempenho de primeira qualidade imediatamente. Ele lida com divisão de código, minimização de código e otimizações como pré-carregamento em segundo plano, processamento de imagem, etc., para que o site que você constrói tenha alto desempenho, sem qualquer tipo de ajuste manual. Esses recursos de desempenho são uma grande parte do suporte à abordagem progressiva de aplicativos da web.

Então existem três critérios base para um site ser classificado como PWA.

### Deve ser executado sob protocolo HTTPS

Executar sob protocolo HTTPS é uma prática de segurança extremamente recomendada, não importa o conteúdo do site. Especificamente sobre aplicativos da web progressivos, a execução em HTTPS é um critério para muitos novos recursos do navegador necessário para o funcionamento dos aplicativos da web progressivos.

Este é todo você!

### Deve incluir o Manifesto do Aplicativo Web

O [Manifesto do Aplicativo Web](https://www.w3.org/TR/appmanifest/) é um ficheiro JSON que fornece ao navegador informações sobre o seu aplicativo Web e possibilita que os usuários salvem na tela inicial.

Inclui informações do aplicativo web tais como `name`, `icons`, `start_url`, `background-color` e [mais](https://developers.google.com/web/fundamentals/web-app-manifest/).

Gatsby fornece uma interface de plug-in para adicionar suporte ao envio de um manifesto com seu site -- [gatsby-plugin-manifest](/packages/gatsby-plugin-manifest).

### Deve implementar um service worker

Um [service worker](https://developers.google.com/web/fundamentals/primers/service-workers/) fornece suporte para uma experiência offline para o seu site, e torna o seu site mais resistente a más conexões de rede.

É um script executado separadamente em segundo plano, suportando recursos como notificações push e sincronização em segundo plano.

Gatsby fornece uma interface de plugin para criar e carregar um service worker em seu site -- [**gatsby-plugin-offline**](/packages/gatsby-plugin-offline).

Recomenadamos o uso do plugin juntamente com o [plugin do manifesto](/packages/gatsby-plugin-manifest). (Não se esqueça de listar o plugin `offline` depois do plugin do `manifesto` para que o arquivo de manifesto seja incluso no service worker).
