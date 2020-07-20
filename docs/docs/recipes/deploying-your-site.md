---
title: "Receitas: Publicando Seu Site"
tableOfContentsDepth: 1
---

Hora do show! Assim que estiver feliz com seu site, você estará pronto para publicá-lo!

## Preparativos para a publicação

### Pré-requisitos

- Um [site Gatsby](/docs/docs/quick-start.md)
- A [CLI do Gatsby](/docs/docs/gatsby-cli.md) instalada

### Etapas

1. Pare a execução do seu servidor de desenvolvimento, caso ainda não tenha feito. (Na maioria dos casos é o atalho `Ctrl + C` no terminal)

2. A partir do diretório raíz do seu site (`/`), execute o comando `gatsby build` usando a CLI do Gatsby no terminal. Os arquivos serão gerados no diretório `public`.

```shell
gatsby build
```

3. Para incluir um caminho diferente de `/` (como `/site-name/`) no seu site, defina um prefixo no arquivo `gatsby-config.js`, substituindo `seuprefixo` pelo desejado:

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/seuprefixo`,
}
```

Existem algumas razões para fazer isso -- por exemplo, hospedar um blog feito com Gatsby em um domínio com outro site, não criado com Gatsby. O site principal possui o endereço `example.com`, e o site com Gatsby utilizando um prefixo, possui o endereço `example.com/blog`

4. Com um prefixo definido no arquivo `gatsby-config.js`, execute o comando `gatsby build` com o parâmetro `--prefix-paths` para adicionar o prefixo automaticamente a todas as URLs e componentes `<Link>`

```shell
gatsby build --prefix-paths
```

5. Certifique-se de que seu site funciona da mesma forma ao executar o comando `gatsby build`, como `gatsby develop`. Ao executar o comando `gatsby serve`, após efetuar a compilação do seu site, você poderá testar (e debugar, se necessário) o produto finalizado, antes de publicá-lo em produção.

```shell
gatsby build && gatsby serve
```

### Recursos adicionais

- Veja a [parte um do tutorial](/docs/tutorial/part-one/index.md#fazendo-deploy-do-seu-site-gatsby) para desenvolver e publicar um site exemplo.
- Aprenda sobre [otimização de performance](/docs/docs/performance.md)
- Leia sobre [outros tópicos relacionados a publicação](/docs/docs/preparing-for-deployment.md)
- Confira a [documentação sobre publicação](/docs/docs/deploying-and-hosting.md), para aprender sobre o processo de publicação em plataformas específicas.

## Publicando no Netlify

Use a [`netlify-cli`](https://www.netlify.com/docs/cli/) para publicar sua aplicação Gatsby sem sair do terminal.

### Pré-requisitos

- Um [site Gatsby](/docs/docs/quick-start.md) com um componente `index.js`
- O pacote [netlify-cli](https://www.npmjs.com/package/netlify-cli) instalado
- A [CLI do Gatsby](/docs/gatsby-cli) instalada

### Etapas

1. Compile a sua aplicação gatsby utilizando o comando `gatsby build`

2. Autentique-se no Netlify com o comando `netlify login`

3. Execute o comando `netlify init`. Selecione a opção "_Create & configure a new site_"

4. Digite o nome do seu website ou pressione a tecla "Enter" para receber um nome randômico.

5. Escolha o seu [Team](https://www.netlify.com/docs/teams/).

6. Altere o caminho da publicação para `public/`

7. Certifique-se de que está tudo OK antes de publicar em produção com o comando `netlify deploy -d . --prod`

### Recursos adicionais

- [Hospedagem no Netlify](/docs/hosting-on-netlify)
- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify)

## Publicando na plataforma ZEIT Now

Use a [CLI do Now](https://zeit.co/download) para publicar sua aplicação sem sair do terminal.

### Pré-requisitos

- Uma conta no [ZEIT Now](https://zeit.co/signup)
- Um [site Gatsby](/docs/docs/quick-start.md) com um componente `index.js`
- O pacote da [CLI do Now ](https://zeit.co/download) instalado
- A [CLI do Gatsby](/docs/docs/gatsby-cli.md) instalada

### Etapas

1. Autentique-se na CLI do Now com o comando `now login`

2. No terminal, mude o diretório atual para a raíz da sua aplicação Gatsby.js, caso ainda não tenha feito.

3. Execute o comando `now` para publicar a aplicação.

### Recursos adicionais

- [Publicando na plataforma ZEIT Now](/docs/docs/deploying-to-zeit-now.md)
