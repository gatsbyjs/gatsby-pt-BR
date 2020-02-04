---
title: Preparando um site para publicação
---

## Criar um novo projeto com Gatsby

Primeira coisa que você precisa fazer é criar e configurar seu novo projeto Gatsby.
Se você ainda não [configurou um projeto Gatsby](/docs/quick-start) você pode fazer isso instalando o Gatsby globalmente:

```shell
npm install --global gatsby-cli
```

Então, crie um projeto com o seguinte comando:

```shell
gatsby new your-new-project
```

Finalmente, mude para o novo diretório do site:

```shell
cd your-new-project
```

## Crie seu site

Para gerar arquivos estáticos da maneira mais simples, escreva:

```shell
gatsby build
```

Então, no diretório `public` haverá arquivos para copiar para o servidor.

<<<<<<< HEAD
## Adicionando um prefixo de rota

Se você quer ir para um prefixo de rota específico, por exemplo `exemplo.com/blog/` ao invés de `exemplo.com/` leia [Adicionando um prefixo de rota](/docs/path-prefix)
=======
## Adding a path prefix

If you want a specific Path Prefix, for example `example.com/blog/` instead of `example.com/` read [adding a path prefix](/docs/path-prefix)
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

## Publicação específica

Ações adicionais podem ser obrigatórias, dependendo de qual servidor você usa.
Se você possui um servidor de um dos provedores a seguir, leia as subpáginas individuais:

- [AWS Amplify](/docs/deploying-to-aws-amplify)
- [S3/Cloudfront](/docs/deploying-to-s3-cloudfront)
- [Aerobatic](/docs/deploying-to-aerobatic)
- [Heroku](/docs/deploying-to-heroku)
- [ZEIT Now](/docs/deploying-to-zeit-now)
- [GitLab Pages](/docs/deploying-to-gitlab-pages)
- [Netlify](/docs/deploying-to-netlify)
- [Render](/docs/deploying-to-render)
- [Surge](/docs/deploying-to-surge)
- [GitHub Pages](/docs/how-gatsby-works-with-github-pages)
- [Microsoft Internet Information Server (IIS)](/docs/deploying-to-iis)
- [Firebase Hosting](/docs/deploying-to-firebase)
- [KintoHub](/docs/deploying-to-kintohub)

Se você não vê a hospedagem que você está interessado, é possível adicionar outros provedores de hospedagem através de [contribuições a documentação](/contributing/docs-contributions).
