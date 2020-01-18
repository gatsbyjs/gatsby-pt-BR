---
title: Publicando no Render
---

[Render](https://render.com) é uma plataforma em nuvem totalmente gerenciável onde você pode hospedar seus sites estáticos, APIs, banco de dados, agendadores de tarefas e todos os outros aplicativos em um único lugar.

Sites estáticos são **totalmente gratuitos** no Render e incluem as seguintes funcionalidades:

- Builds e publicações do Github de forma automática e contínua.
- Certificados SSL automáticos através da [Let's Encrypt](https://letsencrypt.org).
- Invalidação instantânea de cache com um CDN veloz e global. 
- Colaboradores ilimitados.
- [Domínios personalizados](https://render.com/docs/custom-domains) ilimitados.
- [Brotli compression](https://en.wikipedia.org/wiki/Brotli) automático para sites rápidos.
- Suporte nativo ao HTTP/2.
- [Visualização de pull requests](https://render.com/docs/pull-request-previews).
- Redirecionamento automático HTTP → HTTPS. 
- Redirecionamento personalizado de URL e reescrita

## Pré-requisitos

Esse guia assume que você já possui um projeto Gatsby para publicar. Se voce precisa de um projeto poderá usar o [Projeto de Introdução](/docs/quick-start) ou crie um fork do [Gatsby Starter usando Render ](https://github.com/render-examples/gatsby-starter-default)  antes de continuar.

## Configuração

Você pode configurar um site Gatsby no Render em dois passos rápidos:

1. Crie um novo **Web Service** no Render e conceda permissão para acessar o seu repositório no GitHub.
2. Use os seguintes valores durante a criação:

   |                       |                                            |
   | --------------------- | ------------------------------------------ |
   | **Ambiente**       | `Static Site`                              |
   | **Comando de build**     | `gatsby build` (ou o seu próprio comando de build) |
   | **Diretório de publicação** | `public` (ou o seu próprio diretório de publicação)    |

Pronto! Seu site vai estar disponível na sua URL do Render (algo parecido com `yoursite.onrender.com`) assim que a build finalizar.

## Publicação Contínua

Agora que o Render está conectado com o seu repositório, ele vai **automaticamente fazer a build e publicar o seu site** sempre que você enviar alterações para o Github.

Você pode escolher desabilitar publicações automáticas na seção de **Settings** para o seu site e fazer a publicação manualmente no painel de controle do Render.

## CDN do Render e Invalidação de Cache

O Render hospeda o seu site em um CDN global e veloz que garante os tempos de download mais rápidos possíveis para todos os usuários ao redor do mundo.

Cada publicação automática e instantânea invalida o cache do CDN, então seus usuários podem sempre acessar os últimos conteúdos do seu site.

## Domínios Personalizados

Adicione seu próprio domínio ao seu site facilmente usando o guia de [domínios personalizados](https://render.com/docs/custom-domains) do Render.

## Visualização de Pull Requests

Com a visualização de pull request você pode visualizar as alterações introduzidas em um pull request ao invés de simplesmente confiar em code reviews.

Uma vez habilitado todo PR para o seu site vai gerar automaticamente um novo site estático baseado no código da PR. O mesmo vai possuir sua própria URL, e vai ser deletado automaticamente quando a PR for fechada.

Leia mais sobre [Visualização de Pull Request](https://render.com/docs/pull-request-previews) na documentação do Render.

## Suporte

Converse com desenvolvedores do Render em https://render.com/chat ou no email `support@render.com` se você precisar de alguma ajuda.
