---
title: Bulma
---

[Bulma](https://bulma.io) é um framework CSS gratuito e de código aberto baseado no Flexbox. Este guia mostrará como começar com Gatsby e Bulma.

Este guia pressupõe que você tenha um projeto Gatsby configurado. Se você precisar configurar um projeto, vá para o [**Guia de início rápido**](/docs/quick-start) e depois volte.

<<<<<<< HEAD
### Instalação
=======
## Installation
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

Para começar, vamos instalar todos os pacotes necessários.

`yarn add bulma node-sass gatsby-plugin-sass`

Em seguida, adicione o  `gatsby-plugin-sass` no `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

<<<<<<< HEAD
### Arquivo para estilização

Agora é a hora de criar um arquivo _scss_ que contém nossa simples customização de estilo, além da importação do Bulma.

(Para simplificar, insira o arquivo junto do _index.js_ no diretório de páginas)
=======
## File for styles

Now is the time to create a scss-file that holds your simple style customisation and the import statement for bulma.

(To keep things simple, insert the file next to `index.js` in the pages-directory)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```scss:title=mystyles.scss
@charset "utf-8";

// Se necessário, altere suas variáveis ​​antes de importar o Bulma
$title-color: #ff0000;

@import "~bulma/bulma.sass";
```

<<<<<<< HEAD
### Usando o Bulma
=======
## Using Bulma
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

O último passo é importar o estilo e usá-lo.

<<<<<<< HEAD
Vamos substituir o conteúdo padrão do arquivo index.js.
=======
Replace the default contents of the `index.js` file.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

```jsx:title=index.js
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

<<<<<<< HEAD
- [Documentação do Bulma sobre como usar o sass](https://bulma.io/documentation/customize/with-node-sass/)
=======
## Resources

- [Bulma documentation on how to use sass](https://bulma.io/documentation/customize/with-node-sass/)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1
