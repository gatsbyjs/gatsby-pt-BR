---
title: Adicionando um Asset Prefix
---

O Gatsby produz conteúdo estático que pode ser hospedado _em qualquer lugar_ em larga escala e com baixo custo. Esse conteúdo estático é composto de arquivos HTML, Javascript, CSS, imagens 
e mais do que compõe sua grande aplicação Gatsby.

Em alguns casos você pode querer fazer a publicação dos _assets_ (Arquivos não HTML como Javascript, CSS, etc.) para um domínio diferente. Geralmente esse é o momento quando você precisa usar um CDN dedicado para os assets ou necessita seguir as políticas específicas da companhia de hospedagem. 

A funcionalidade `assetPrefix` está disponível a partir do gatsby@2.4.0, para que você possa perfeitamente usar os Gatsby assets hospedados com domínios diferentes. Para usar tal funcionalidade, certifique-se que sua versão do `gatsby` presente no seu arquivo `package.json` esteja ao menos na versão `2.4.0`.

## Uso

### Adicionando ao arquivo`gatsby-config.js`

```js:title=gatsby-config.js
module.exports = {
  assetPrefix: `https://cdn.example.com`,
}
```

Mais um passo - Ao fazer o build da aplicação, deve-se adicionar a seguinte flag para que o Gatsby reconheça essa opção corretamente. 

### Flag `--prefix-paths` 

Ao fazer o build com um `assetPrefix`, necessita-se da flag `--prefix-paths`. Caso essa flag não seja especificada, a opção será ignorada durante o build da aplicação e o conteúdo será gerado como se estivesse hospedado em um mesmo domínio. Para garantir que sua build seja gerada corretamente, use o seguinte comando: 

```shell
gatsby build --prefix-paths
```

É isso! Você já possui uma aplicação preparada para deploy com seus assets a partir de um CDN e seus arquivos principais (ex: Arquivos HTML) podem ser hospedados em um diferente domínio.

## Build / Deploy

Assim que fizer o build da sua aplicação, todos os assets terão automaticamente esse asset prefix definido. Por exemplo, se você possuir um arquivo Javascript `app-common-1234.js`, a tag desse script será mostrada em algo como: 

```html
<script src="https://cdn.example.com/app-common-1234.js"></script>
```

Todavia - Caso pretenda fazer o deploy de sua aplicação as-is, esses assets não estariam disponíveis! Você pode resolver isso de algumas formas, mas o caminho comum seria fazer o deploy dos conteúdos da pasta `public` para _ambos_ seus domínio principal e no local de seu CDN/asset prefix.

### Usando o `onPostBuild`

Utilizando API Hook [`onPostBuild`](/docs/node-apis/#onPostBuild). Isso pode ser usado para fazer o deploy do seu conteúdo ao CDN, da seguinte forma:

```js:title=gatsby-node.js
const assetsDirectory = `public`

exports.onPostBuild = async function onPostBuild() {
  // fazer algo no público
  // ex:. upload para o S3
}
```

### Usando scripts `package.json` 

Além disso, você pode usar um script npm, o que permitirá que você utilize algumas linhas de comandos de interfaces e executáveis para realizar algumas ações, nesse caso, fazendo o deploy do seu diretório de assets!

No exemplo abaixo, o `aws-cli` e `s3` estão sendo usados para sincronizar a pasta `public` (contendo todos os assets) para o `s3` bucket.

```json:title=package.json
{
  "scripts": {
    "build": "gatsby build --prefix-paths",
    "postbuild": "aws s3 sync public s3://mybucket"
  }
}
```

Agora sempre que o script `build` for chamado, ex: `npm run build`, o script `postbuild` será chamado logo _após_ o build finalizado, dessa forma fazendo com que seus assets fiquem disponíveis em um domínio _diferente_ após a finalização do build da aplicação com seu assets prefix.

## Considerações Extras

### Uso com `pathPrefix`

A funcionalidade [`pathPrefix`](/docs/path-prefix/) pode ser vista de forma levemente relacionada com a funcionalidade aqui apresentada. Essa funcionalidade permite que _todo_ o conteúdo do seu site seja prefixado com algumas constantes prefix, por exemplo, você pode querer que seu blog seja hospedado a partir de `/blog` ao invés do diretório raiz do projeto.

Essa funcionalidade trabalha perfeitamente com a `pathPrefix`. Construa sua aplicação com a flag `--prefix-paths` e você estará no caminho para hospedar sua aplicação com seus assets hospedados num CND, e suas funcionalidades principais disponíveis através de um caminho prefixo.

### Uso com `gatsby-plugin-offline`

Ao usar um asset prefix customizado com o `gatsby-plugin-offline`, seus assets podem continuar acessíveis offline. Todavia, para garantir que o plugin funcione corretamente, necessita-se realizar alguns passos.

1. Seu servidor com os assets deve ter o cabeçalho `Access-Control-Allow-Origin` em `*` ou na raiz de seu site.
2. Alguns recursos essenciais devem estar acessíveis no seu servidor de conteúdo (ex: utilizado para gerar as páginas). Isso inclui `sw.js`, assim como os recursos de pré-cache: o bundle do webpack, bundle do app, o manifest (e qualquer ícone referenciado), e os recursos para o shell do app para o plugin offline.

   Você pode encontrar a maior parte buscando pela variável `self.__precacheManifest` gerada em `sw.js`. Lembre-se de também incluir o próprio `sw.js`, e qualquer ícone referenciado em seu `manifest.webmanifest` caso tenha um. Para verificar se o seu service worker está funcionando como o esperado, verifique em Application → Service Workers na aba dev tools em seus browser, checando qualquer recurso que tenha falhado na sua aba Console/Network.
