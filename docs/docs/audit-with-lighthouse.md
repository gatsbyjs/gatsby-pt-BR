---
title: Auditoria com o Lighthouse
---

Citando o [site do Lighthouse](https://developers.google.com/web/tools/lighthouse/):

> O Lighthouse é uma ferramenta automatizada de código aberto para aprimorar a qualidade de páginas da web. O lighthouse pode ser executado em qualquer página pública ou que exija autenticação. Ele tem auditorias de performance, acessibilidade, progressive web apps (PWAs) e mais.

O Lighthouse é incluido por padrão no Chrome DevTools. Executar as auditorias dele, abordar os erros encontrados e então implementar as melhorias sugeridas é uma maneira excelente de preparar seu site para ir ao ar. Ele te ajuda a garantir que seu site seja o mais rápido e acessível possível.

Caso você não tenha ainda, você precisa criar pacote de produção do seu site Gatsby. O servidor de desenvolvimento do Gatsby é perfeito para agilizar o desenvolvimento, mas o site gerado, apesar de se assemelhar muito à versão de produção do site, não é otimizado.

## Create a production build

1.  Stop the development server (if it's still running) and run:

```shell
gatsby build
```

> 💡 This does a production build of your site and outputs the built static files into the `public` directory.

2.  View the production site locally. Run:

```shell
gatsby serve
```

Once this starts, you can now view your site at `http://localhost:9000`.

## Run a Lighthouse audit

Now run your first Lighthouse test.

1.  Open the site in Chrome (if you didn't already do so) and then open up the Chrome DevTools.

2.  Click on the "Audits" tab where you'll see a screen that looks like:

![Lighthouse audit start](./images/lighthouse-audit.png)

3.  Click "Perform an audit..." (All available audit types should be selected by default). Then click "Run audit". (It'll then take a minute or so to run the audit). Once the audit is complete, you should see results that look like this:

![Lighthouse audit results](./images/lighthouse-audit-results.png)

As you can see, Gatsby's performance is excellent out of the box but we're missing some things for PWA, Accessibility, Best Practices, and SEO that will improve your scores (and in the process make your site much more friendly to visitors and search engines). To improve your scores further, see the links under "Next steps" below.

Next steps:

- [Add a manifest file](/docs/add-a-manifest-file/)
- [Add offline support](/docs/add-offline-support-with-a-service-worker/)
- [Add page metadata](/docs/add-page-metadata/)
