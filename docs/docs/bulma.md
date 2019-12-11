---
título: Bulma
---

[Bulma](https://bulma.io) é uma framework CSS gratuito e de código aberto baseado no Flexbox. Este guia mostrará como começar com Gatsby e Bulma.

Este guia pressupõe que você tenha um projeto Gatsby configurado. Se você precisar configurar um projeto, vá para o [**Guia de início rápido**](/docs/quick-start) e depois volte.

### Instalação

Para iniciantes, vamos instalar todos os pacotes necessários.

`yarn add bulma node-sass gatsby-plugin-sass`

Em seguida, adicione o  `gatsby-plugin-sass` no `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

### Arquivo para estilização

Agora é a hora de criar um arquivo _scss_ que contém nossa simples customização de estilo e a importação do Bulma.

(Para simplificar, insira o arquivo junto do _index.js_ no diretório de páginas)

```scss:title=mystyles.scss
@charset "utf-8";

// Se necessário, altere suas variáveis ​​antes de importar o Bulma
$title-color: #ff0000;

@import "~bulma/bulma.sass";
```

### Usando o Bulma

O último passo é importar o estilo e usá-lo.

Vamos substituir o conteúdo padrão do arquivo index.js.

```javascript:title=index.js
import React from "react"
import "./mystyles.scss"

const IndexPage = () => {
  return (
    <div className="container">
      <div className="columns">
        <div className="column">
          <h2 className="title is-2">Título do nível 2</h2>
          <p className="content">Conteúdo legal. Usando Bulma!</p>
        </div>

        <div className="column is-four-fifths">
          <h2 className="title is-2">Título do nível 2 </h2>
          <p className="content">Esta coluna também é legal!</p>
        </div>
      </div>
    </div>
  )
}

export default IndexPage
```
E é só isso! Agora você pode usar o Bulma como faria normalmente.

### Recursos

- [Documentação do Bulma sobre como usar o sass](https://bulma.io/documentation/customize/with-node-sass/)
