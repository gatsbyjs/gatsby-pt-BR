---
title: Auditoria com o Lighthouse
---

Citando o [site do Lighthouse](https://developers.google.com/web/tools/lighthouse/):

> O Lighthouse é uma ferramenta automatizada de código aberto para aprimorar a qualidade de páginas da web. O lighthouse pode ser executado em qualquer página pública ou que exija autenticação. Ele tem auditorias de performance, acessibilidade, progressive web apps (PWAs) e mais.

O Lighthouse é incluído por padrão no Chrome DevTools. Executar as auditorias dele, abordar os erros encontrados e então implementar as melhorias sugeridas é uma maneira excelente de preparar seu site para ir ao ar. Ele te ajuda a garantir que seu site seja o mais rápido e acessível possível.

Caso você não tenha ainda, você precisa criar pacote de produção do seu site Gatsby. O servidor de desenvolvimento do Gatsby é perfeito para agilizar o desenvolvimento, mas o site gerado, apesar de se assemelhar muito à versão de produção do site, não é otimizado.

## Crie um pacote de produção

1.  Pare o servidor de desenvolvimento (caso ainda esteja em execução) e então execute:

```shell
gatsby build
```

> 💡 Esse comando cria um pacote de produção do seu site e envia os arquivos estáticos criados para o diretório `public`.

2.  Sirva o pacote de produção localmente. Execute:

```shell
gatsby serve
```

Uma vez iniciado, você poderá visualizar seu site em `http://localhost:9000`.

## Execute o Lighthouse

Agora execute sua primeira auditoria Lighthouse.

1.  Vá para o URL que você deseja auditar (http://localhost:9000).

2.  Abra o [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools#open)

3.  Clique na aba "Audits" e então você verá uma tela parecida com esta:

![Lighthouse audit start](./images/lighthouse-audit.png)

4.  Clique no botão "Perform an audit". Então o DevTools irá mostrar uma lista de categorias de auditoria. Deixe todos eles ativados.

5.  Clique no botão "Run audit" para executar os testes. Após 30 a 60 segundos, o Lighthouse te fornece um relatório da página parecido com este:

![Lighthouse audit results](./images/lighthouse-audit-results.png)

Como poderão comprovar, o Gatsby proporciona por padrão uma performance excelente. Entretanto ainda falta algumas melhorias de acessibilidade, SEO, PWA e boas práticas que irão melhorar suas pontuações e consequentemente fazer seu site mais amigável aos visitantes e aos motores de busca. Para melhorar ainda mais suas pontuações, consulte os links em "Próximas etapas" abaixo:

Próximas etapas:

- [Adicionando o Arquivo de Manifesto](/docs/add-a-manifest-file/)
- [Adicionando o modo off-line](/docs/add-offline-support-with-a-service-worker/)
- [Adicionando metadados da página](/docs/add-page-metadata/)
