---
title: Adicionando Formulários
---

Gatsby é construído utilizando o React. Portanto, tudo o que é possível fazer com um formulário React é possível fazer também no Gatsby. Detalhes adicionais sobre como criar formulários do React podem ser encontrados na [Documentação de Formulários do React](https://pt-br.reactjs.org/docs/forms.html) (e esta página da documentação de formulários do React foi criada usando Gatsby!)

Vamos começar com a seguinte página.

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

Esta página do Gatsby é um componente do React. Quando você deseja criar um formulário, é necessário armazenar o estado do formulário - o que o usuário digitou. Converta seu componente de função (stateless) em um componente de classe (stateful).

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  render() {
    return <div>Hello world!</div>
  }
}
```

Agora que você criou um componente de classe, você pode adicionar um estado(`state`) ao componente.

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    nome: "",
    sobrenome: ""
  }

  render() {
    return <div>Hello world!</div>
  }
}
```

Agora você pode adicionar alguns campos de `input`:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    nome: "",
    sobrenome: ""
  }

  render() {
    return (
      <form>
        <label>
          Nome
          <input type="text" name="nome" />
        </label>
        <label>
          Sobrenome
          <input type="text" name="sobrenome" />
        </label>
        <button type="submit">Enviar</button>
      </form>
    )
  }
}
```

Quando o usuário digita em um `input`, o estado deve ser atualizado. Adicione a propriedade `onChange` para atualizar o estado e adicione a propriedade `value` para manter o `input` atualizado com o novo estado:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    nome: "",
    sobrenome: ""
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value
    })
  }

  render() {
    return (
      <form>
        <label>
          Nome
          <input
            type="text"
            name="nome"
            value={this.state.nome}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Sobrenome
          <input
            type="text"
            name="sobrenome"
            value={this.state.sobrenome}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Enviar</button>
      </form>
    )
  }
}
```

Agora que os seus `inputs` estão funcionando, você deseja que algo aconteça ao enviar o formulário, certo?

Então, adicione a propriedade `onSubmit` no `form` e crie uma função chamada `handleSubmit` para mostrar um alerta quando o usuário enviar o formulário:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    nome: "",
    sobrenome: ""
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value
    })
  }

  handleSubmit = event => {
    event.preventDefault()
    alert(`Bem-vindo ${this.state.nome} ${this.state.sobrenome}!`)
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Nome
          <input
            type="text"
            name="nome"
            value={this.state.nome}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Sobrenome
          <input
            type="text"
            name="sobrenome"
            value={this.state.sobrenome}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Enviar</button>
      </form>
    )
  }
}
```

Este formulário não está fazendo nada além de mostrar as informações do usuário que ele acabou de receber. Neste ponto, convém mover este formulário para um componente, envie o estado do formulário para um servidor back-end, ou adicione uma validação robusta. Você também pode usar fantásticas bibliotecas de formulários do React, como o [Formik](https://github.com/jaredpalmer/formik) ou [Final Form](https://github.com/final-form/react-final-form) para acelerar seu processo de desenvolvimento.

Tudo isso é possível e muito mais, aproveitando o poder do Gatsby e do ecossistema React!
