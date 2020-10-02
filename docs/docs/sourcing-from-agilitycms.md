---
título: Integrando do Agility CMS
---

Esse guia vai explicar em detalhes os passos para configurar um site do Gatsby que busca conteúdo do [Agility CMS](https://agilitycms.com/).

## O que é Agility CMS? O que o faz diferente?

[Agility CMS](https://agilitycms.com/) é um Sistema de Gerenciamento de Conteúdo (Content Management System, CMS) headless, que permite que você defina seus tipos de conteúdo personalizados e relacionamentos. Isso é chamado de Arquitetura de Conteúdo, e você pode reusar esse conteúdo para os seus websites e apps.

Além disso, o Agility CMS provê uma API de roteamento de página, que permite transferir o controle do sitemap para os editores de conteúdo.

Todo o conteúdo está disponível nas APIs Agility CMS Fetch ou Preview.

## Começando

### Crie uma conta gratuita Agility

Crie uma conta Agility CMS com o Plano Gratuito (esse plano é gratuito para sempre). [Cadastre-se no Agility CMS](https://account.agilitycms.com/sign-up?product=agility-free).

Quando sua conta for criada, você precisará pegar seu GUID e as API Keys.

### Execute o código

Certifique-se de que você tem o Gatsby CLI instalado:

```shell
npm install -g gatsby-cli
```

Clone o repositório do GitHub, [Agility CMS Gatsby Starter](https://github.com/agility/agility-gatsby-starter), que tem todo o código que você precisa para começar:

```shell
git clone https://github.com/agility/agility-gatsby-starter.git
```

Instale as dependências:

```shell
npm install
```

Depois de configurar a infraestrutura, execute o site no modo de desenvolvimento:

```shell
gatsby develop
```

O site é apenas um starter, mas ele possui várias funcionalidades interessantes que você pode usar para construir. O próximo passo é conectar esse código à sua nova instância Agility CMS que você acabou de criar.

## Conecte sua instância Agility CMS

Edite o arquivo `gatsby-config.js` e substitua o `guid` e `apiKey` pelos seus.

Você pode encontrar suas API Keys na página Começando no Agility CMS Content Manager.

![Agility CMS - Dashboard - API Keys](./images/agilitycms-api-keys.png)

Se você usar a key `preview`, você não vai precisar publicar para ver as alterações feitas. Se você usar a key `fetch`, certifique-se de que você publicou qualquer conteúdo que deseja ver alterado.

## Como funciona

O plugin Gatsby Source baixa todas as páginas do Agility CMS Sitemap, assim como qualquer conteúdo compartilhado que é referenciado na propriedade `sharedContent` no arquivo `gatsby-config.js`.

Todas essas páginas e conteúdos são disponibilizados em GraphQL para os componentes React que você irá escrever para renderizar essas páginas.

Confira o componente chamado "Jumbotron". Esse é um exemplo de como exibir um cabeçalho e subtítulo estilizados com o conteúdo que vem do Agility CMS. Aqui está o módulo que fornece esse conteúdo sendo editado no Agility CMS Content Manager:

![Agility CMS - Example Module - Jumbotron](./images/agilitycms-jumbotron.png)

E aqui está o código usado para renderizar. Perceba que os campos `title` e `subTitle` estão disponíveis como propriedades do objeto `item.fields`.

```jsx:title=src/modules/Jumbotron.js
import React, { Component } from "react"
import { graphql, StaticQuery } from "gatsby"

import "./Jumbotron.css"

export default class Jumbotron extends Component {
  render() {
    return (
      <section className="jumbotron">
        <h1>{this.props.item.fields.title}</h1>
        <h2>{this.props.item.fields.subTitle}</h2>
      </section>
    )
  }
}
```

Quando você adiciona novos módulos e definições de conteúdo ao Agility CMS, os componentes usados para renderizar esses módulos automaticamente irão receber os dados fortemente tipados fornecidos a esses módulos como props.