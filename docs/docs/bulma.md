---
title: Bulma
---

[Bulma](https://bulma.io) é um framework open-source baseado em _flexbox_. Este guia mostrará como começar a usar o Gatsby com o Bulma.

Este guia pressupõe que você tenha um projeto Gatsby configurado. Se você precisa configurar um projeto, veja primeiro o [**Guia rápido**](/docs/quick-start), então após isso volte para cá.

### Instalação

Para iniciantes, vamos instalar todos os pacotes necessários.

`yarn add bulma node-sass gatsby-plugin-sass`

Então adicione o `gatsby-plugin-sass` ao `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

### Arquivo para estilos

Agora é a hora de criar um arquivo _scss_ que contém nossa simples customização de estilo e a declaração de importação do Bulma.

(Para manter as coisas simples insira o arquivo junto ao _index.js_ no diretório de páginas)

```scss:title=mystyles.scss
@charset "utf-8";

// Se necessário, altere suas variáveis antes de importar o Bulma
$title-color: #ff0000;

@import "~bulma/bulma.sass";
```

### Usando o Bulma

O último passo é importar o estilo e usá-lo.

Vamos substituir o conteúdo padrão do arquivo _index.js_.

```javascript:title=index.js
import React from "react"
import "./mystyles.scss"

const IndexPage = () => {
  return (
    <div className="container">
      <div className="columns">
        <div className="column">
          <h2 className="title is-2">Level 2 heading</h2>
          <p className="content">Conteúdo legal. Usando o Bulma!</p>
        </div>

        <div className="column is-four-fifths">
          <h2 className="title is-2">Cabeçalho de Level 2</h2>
          <p className="content">Essa coluna é legal também!</p>
        </div>
      </div>
    </div>
  )
}

export default IndexPage
```

E é só isso! Agora você pode usar o Bulma como faria normalmente.

### Materiais

- [Documentação do Bulma sobre como usar com sass](https://bulma.io/documentation/customize/with-node-sass/)
