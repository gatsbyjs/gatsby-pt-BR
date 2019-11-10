---
title: Utilizando Gitpod, Ambiente de Desenvolvimento Online
---

Esta página nos dá um esboço de como utilizar o Gitpod, um ambiente de desenvolvimento online gratuito, para contribuir com o core do Gatsby e seu ecossistema. Para obter instruções sobre a configuração de um ambiente de desenvolvimento local, visite a página de [configuração local](/contributing/setting-up-your-local-dev-environment/).

## Sobre o Gitpod

Gitpod deixa as contribuições no Github mais fáceis, pois permite a configuração automatizada de um ambiente de desenvolvimento. Ao invés de escrever uma longa
documentação de como instalar e configurar deixando todo contribuidor passar por essa aventura, a configuração é automatizada e reproduzível.

Além disso, o Gitpod pré-builda qualquer branch de um repositório para que você não precise aguardar por uma instalação, clonando e buildando.

## Iniciando

Para iniciar um ambiente de desenvolvimento do zero, você pode prefixar qualquer URL do Github com `gitpod.io/#`.

> Exemplo: https://gitpod.io/#https://github.com/gatsbyjs/gatsby

O ambiente de desenvolvimento irá abrir um projeto core do gatsby já buildado, bem como um exemplo de build (gatsbygram).
Três terminais serão iniciados lado a lado executando os seguintes processos:

- `yarn run watch --scope={gatsby,gatsby-image,gatsby-link}`
  Observa e rebuilda o código core do gatsby quando houver alguma alteração.
- `gatsby-dev`
  Copia as alterações do core para o exemplo.
- `gatsby develop`
  Disponibiliza o exemplo em modo de desenvolvimento.

A aplicação exemplo será exibida no lado direito, em uma janela de pré-visualização.

## Trabalhando em uma Issue

Para começar a trabalhar em uma issue, você pode pode prefixar a URL da issue com `gitpod.io/#`.

> Exemplo: https://gitpod.io/#https://github.com/gatsbyjs/gatsby/issues/1199

Isso irá abrir um ambiente de desenvolvimento local zerado, com uma branch local nomeada após a issue.
Agora você pode codar, testar, comitar, fazer pushs e criar um PR de dentro do seu ambiente de trabalho.

## Revisão de Código

Algumas das mudanças feitas precisam de uma revisão de código mais detalhada do que oque é possível se fazer no Github. Prefixar um _PR_ com `gitpod.io/#` irá abrir este branch em modo de revisão de código.

Neste modo você verá a lista de arquivos modificados na esquerda, pelos quais se pode navegar. Ainda, pode-se rodar o app e utilizar as funcionalidades modificadas para explorar mais o código alterado. Você pode ver comentários existentes ou adicionar novos comentários no editor e submeter o resultado da sua revisão também.

## Como executar outro exemplo

Se quiser executar outro exemplo vocẽ pode abrir um novo ou um já existente terminal e rodar os seguintes comandos:

```shell
yarn install
gatsby-dev --set-path-to-repo ../..
gatsby-dev
yarn run dev
```
