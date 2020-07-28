---
título: Adicionando Pesquisa com JS Search
---

## Pré-requisitos

Antes de seguir as etapas necessárias para adicionar a pesquisa de clientes ao seu site do Gatsby, você deve estar familiarizado com os conceitos básicos do Gatsby. Confira o [tutorial](/tutorial/) e atualize a [documentação](/docs/) se for preciso. Além disso, algum conhecimento de [ES6 syntax](https://medium.freecodecamp.org/write-less-do-more-with-javascript-es6-5fd4a8e50ee2) será útil.

## O que é JS Search

[JS Search](https://github.com/bvaughn/js-search) é uma biblioteca criada por Brian Vaughn, membro da equipe principal do Facebook. Ela fornece uma maneira eficiente de procurar dados no cliente com JavaScript e JSON objects. Ele também possui diversas opções de personalização; confira os documentos para obter mais detalhes.

O código e a documentação completa desta biblioteca estão [disponiveis no GitHub](https://github.com/bvaughn/js-search). Este guia é baseado no guia oficial `js-search` exemplo, mas foi adaptado para trabalhar com seu site do Gatsby.

## Configuração

Você começará criando um novo site do Gatsby com base no iniciador oficial _ola mundo_. Abra um terminal e execute o seguinte comando:

```shell
gatsby new js-search-example https://github.com/gatsbyjs/gatsby-starter-default
```

Após a conclusão do processo, são necessários alguns pacotes adicionais.

Mude os diretórios para a pasta `js-search-example` e emita o seguinte comando:

```shell
npm install --save js-search axios
```

Ou se o Yarn estiver sendo usado:

```shell
yarn add js-search axios
```

**Nota**:

Para este exemplo em particular [axios](https://github.com/axios/axios) será usado para lidar com todas as promise-based HTTP solicitadas.

## Seleção de estratégia

Nas próximas seções, você aprenderá sobre duas abordagens para implementar `js-search` no seu site. Qual você vai escolher dependerá do número de itens que você deseja pesquisar. Para um conjunto de dados pequeno a médio, a primeira estratégia documentada deve funcionar bem.

Para conjuntos de dados maiores, você pode usar a segunda abordagem, já que a maior parte do trabalho é feita antecipadamente através do uso da API interna do Gatsby.

Ambas as formas são bastante generalistas, elas foram implementadas usando a opção padrão da biblioteca, para que ela possa ser experimentada sem entrar nas especificidades da biblioteca.

E, finalmente, ao ler o código, lembre-se de que ele não segue as práticas recomendadas, é apenas para fins de demonstração. Em um site real, ele teria sido implementado de uma maneira diferente.

## JS-Search com um conjunto de dados pequeno a médio

Comece criando um arquivo chamado `SearchContainer.js` na pasta `src/components/`, em seguida adicione o seguinte código para começar:

```jsx:title=src/components/SearchContainer.js
import React, { Component } from "react"
import Axios from "axios"
import * as JsSearch from "js-search"

class Search extends Component {
  state = {
    bookList: [],
    search: [],
    searchResults: [],
    isLoading: true,
    isError: false,
    searchQuery: "",
  }
  /**
   * React lifecycle method para buscar os dados
   */
  async componentDidMount() {
    Axios.get("https://bvaughn.github.io/js-search/books.json")
      .then(result => {
        const bookData = result.data
        this.setState({ bookList: bookData.books })
        this.rebuildIndex()
      })
      .catch(err => {
        this.setState({ isError: true })
        console.log("====================================")
        console.log(`Something bad happened while fetching the data\n${err}`)
        console.log("====================================")
      })
  }

  /**
   * reconstrói o índice geral com base nas opções
   */
  rebuildIndex = () => {
    const { bookList } = this.state
    const dataToSearch = new JsSearch.Search("isbn")
    /**
     *  define uma estratégia de indexação para os dados
     * mais sobre isso aqui https://github.com/bvaughn/js-search#configuring-the-index-strategy
     */
    dataToSearch.indexStrategy = new JsSearch.PrefixIndexStrategy()
    /**
     * define o sanitizer para a pesquisa
     * para impedir que algumas palavras sejam excluídas
     *
     */
    dataToSearch.sanitizer = new JsSearch.LowerCaseSanitizer()
    /**
     * define o índice de pesquisa
     * leia mais sobre isso aqui https://github.com/bvaughn/js-search#configuring-the-search-index
     */
    dataToSearch.searchIndex = new JsSearch.TfIdfSearchIndex("isbn")

    dataToSearch.addIndex("title") // define o atributo de índice para os dados
    dataToSearch.addIndex("author") // define o atributo de índice para os dados

    dataToSearch.addDocuments(bookList) // adiciona os dados a serem pesquisados
    this.setState({ search: dataToSearch, isLoading: false })
  }

  /**
   * lida com a alteração de entrada e realiza uma pesquisa com js-search
   * em que os resultados serão adicionados ao estado
   */
  searchData = e => {
    const { search } = this.state
    const queryResult = search.search(e.target.value)
    this.setState({ searchQuery: e.target.value, searchResults: queryResult })
  }
  handleSubmit = e => {
    e.preventDefault()
  }

  render() {
    const { bookList, searchResults, searchQuery } = this.state
    const queryResults = searchQuery === "" ? bookList : searchResults
    return (
      <div>
        <div style={{ margin: "0 auto" }}>
          <form onSubmit={this.handleSubmit}>
            <div style={{ margin: "0 auto" }}>
              <label htmlFor="Search" style={{ paddingRight: "10px" }}>
                Digite sua pesquisa aqui
              </label>
              <input
                id="Search"
                value={searchQuery}
                onChange={this.searchData}
                placeholder="Enter your search here"
                style={{ margin: "0 auto", width: "400px" }}
              />
            </div>
          </form>
          <div>
            Número de ítens:
            {queryResults.length}
            <table
              style={{
                width: "100%",
                borderCollapse: "collapse",
                borderRadius: "4px",
                border: "1px solid #d3d3d3",
              }}
            >
              <thead style={{ border: "1px solid #808080" }}>
                <tr>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    ISBN do livro
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Título do livro
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Autor do livro
                  </th>
                </tr>
              </thead>
              <tbody>
                {queryResults.map(item => {
                  return (
                    <tr key={`row_${item.isbn}`}>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.isbn}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.title}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.author}
                      </td>
                    </tr>
                  )
                })}
              </tbody>
            </table>
          </div>
        </div>
      </div>
    )
  }
}
export default Search
```

Dividindo o código em partes menores:

1. Quando o componente é montado, o lifecycle method `componentDidMount()` é acionado e os dados serão buscados.
2. Se nenhum erro ocorrer, os dados recebidos serão adicionados ao estado e a função `rebuildIndex ()` será chamada.
3. O mecanismo de pesquisa é criado e configurado com as opções padrões.
4. Os dados são então indexados usando js-search.
5. Quando o conteúdo da entrada é alterado, o js-search inicia o processo de pesquisa com base no valor do `input` e retorna os resultados da pesquisa, se houver algum, ele é apresentado ao usuário através do elemento `table`.

### Juntando todas as peças

Para que ele funcione no seu site, você só precisa importar o componente recém-criado para uma página.
Como você pode ver [no site de exemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/src/pages/index.js).

Execute `gatsby develop` e se tudo correu bem, abra o navegador de sua escolha e digite a URL `http://localhost:8000` - você terá uma pesquisa totalmente funcional à sua disposição.

## JS-Search com um grande conjunto de dados

Agora tente uma abordagem diferente, desta vez, em vez de deixar o componente fazer todo o trabalho, é tarefa do Gatsby fazer isso e passar todos os dados para uma página definida pelo caminho da propriedade, via [pageContext](/docs/behind-the-scenes-terminology/#pagecontext).

Para fazer isso, são necessárias algumas alterações.

Comece modificando o arquivo `gatsby-node.js` adicionando o seguinte código:

```javascript:title=gatsby-node.js
const path = require("path")
const axios = require("axios")

exports.createPages = ({ actions }) => {
  const { createPage } = actions
  return new Promise((resolve, reject) => {
    axios
      .get("https://bvaughn.github.io/js-search/books.json")
      .then(result => {
        const { data } = result
        /**
         * cria uma página dinâmica com os dados recebidos
         * injeta os dados no objeto de contexto juntamente com algumas opções
         * configura o js-search
         */
        createPage({
          path: "/search",
          component: path.resolve(`./src/templates/ClientSearchTemplate.js`),
          context: {
            bookData: {
              allBooks: data.books,
              options: {
                indexStrategy: "Prefix match",
                searchSanitizer: "Lower Case",
                TitleIndex: true,
                AuthorIndex: true,
                SearchByTerm: true,
              },
            },
          },
        })
        resolve()
      })
      .catch(err => {
        console.log("====================================")
        console.log(`error creating Page:${err}`)
        console.log("====================================")
        reject(new Error(`error on page creation:\n${err}`))
      })
  })
}
```

Crie um arquivo chamado `ClientSearchTemplate.js` na pasta `src/templates/`, em seguida adicione o seguinte código para começar:

```jsx:title=src/templates/ClientSearchTemplate.js
import React from "react"
import ClientSearch from "../components/ClientSearch"

const SearchTemplate = props => {
  const { pageContext } = props
  const { bookData } = pageContext
  const { allBooks, options } = bookData
  return (
    <div>
      <h1 style={{ marginTop: `3em`, textAlign: `center` }}>
        Pesquise dados usando JS Search usando Gatsby Api
      </h1>
      <div>
        <ClientSearch books={allBooks} engine={options} />
      </div>
    </div>
  )
}

export default SearchTemplate
```

Crie um arquivo chamado `ClientSearch.js` na pasta `src/components/`, em seguida adicione o seguinte código como linha de base:

```jsx:title=src/components/ClientSearch.js
import React, { Component } from "react"
import * as JsSearch from "js-search"

class ClientSearch extends Component {
  state = {
    isLoading: true,
    searchResults: [],
    search: null,
    isError: false,
    indexByTitle: false,
    indexByAuthor: false,
    termFrequency: true,
    removeStopWords: false,
    searchQuery: "",
    selectedStrategy: "",
    selectedSanitizer: "",
  }
  /**
   * React lifecycle method que injeta os dados no estado.
   */
  static getDerivedStateFromProps(nextProps, prevState) {
    if (prevState.search === null) {
      const { engine } = nextProps
      return {
        indexByTitle: engine.TitleIndex,
        indexByAuthor: engine.AuthorIndex,
        termFrequency: engine.SearchByTerm,
        selectedSanitizer: engine.searchSanitizer,
        selectedStrategy: engine.indexStrategy,
      }
    }
    return null
  }
  async componentDidMount() {
    this.rebuildIndex()
  }

  /**
   * reconstrói o índice geral com base nas opções
   */
  rebuildIndex = () => {
    const {
      selectedStrategy,
      selectedSanitizer,
      removeStopWords,
      termFrequency,
      indexByTitle,
      indexByAuthor,
    } = this.state
    const { books } = this.props

    const dataToSearch = new JsSearch.Search("isbn")

    if (removeStopWords) {
      dataToSearch.tokenizer = new JsSearch.StopWordsTokenizer(
        dataToSearch.tokenizer
      )
    }
    /**
     * define uma estratégia de indexação para os dados
     * Leia mais sobre isso aqui https://github.com/bvaughn/js-search#configuring-the-index-strategy
     */
    if (selectedStrategy === "All") {
      dataToSearch.indexStrategy = new JsSearch.AllSubstringsIndexStrategy()
    }
    if (selectedStrategy === "Exact match") {
      dataToSearch.indexStrategy = new JsSearch.ExactWordIndexStrategy()
    }
    if (selectedStrategy === "Prefix match") {
      dataToSearch.indexStrategy = new JsSearch.PrefixIndexStrategy()
    }

    /**
     * define o sanitizer para a pesquisa
     * para impedir que algumas palavras sejam excluídas
     */
    selectedSanitizer === "Case Sensitive"
      ? (dataToSearch.sanitizer = new JsSearch.CaseSensitiveSanitizer())
      : (dataToSearch.sanitizer = new JsSearch.LowerCaseSanitizer())
    termFrequency === true
      ? (dataToSearch.searchIndex = new JsSearch.TfIdfSearchIndex("isbn"))
      : (dataToSearch.searchIndex = new JsSearch.UnorderedSearchIndex())

    // define o atributo de índice para os dados
    if (indexByTitle) {
      dataToSearch.addIndex("title")
    }
    // define o atributo de índice para os dados
    if (indexByAuthor) {
      dataToSearch.addIndex("author")
    }

    dataToSearch.addDocuments(books) // adiciona os dados a serem pesquisados

    this.setState({ search: dataToSearch, isLoading: false })
  }
  /**
   * lida com a alteração de entrada e realiza uma pesquisa com js-search
   * em que os resultados serão adicionados ao estado
   */
  searchData = e => {
    const { search } = this.state
    const queryResult = search.search(e.target.value)
    this.setState({ searchQuery: e.target.value, searchResults: queryResult })
  }
  handleSubmit = e => {
    e.preventDefault()
  }
  render() {
    const { searchResults, searchQuery } = this.state
    const { books } = this.props
    const queryResults = searchQuery === "" ? books : searchResults
    return (
      <div>
        <div style={{ margin: "0 auto" }}>
          <form onSubmit={this.handleSubmit}>
            <div style={{ margin: "0 auto" }}>
              <label htmlFor="Search" style={{ paddingRight: "10px" }}>
                Digite sua pesquisa aqui
              </label>
              <input
                id="Search"
                value={searchQuery}
                onChange={this.searchData}
                placeholder="Enter your search here"
                style={{ margin: "0 auto", width: "400px" }}
              />
            </div>
          </form>
          <div>
            Número de ítens:
            {queryResults.length}
            <table
              style={{
                width: "100%",
                borderCollapse: "collapse",
                borderRadius: "4px",
                border: "1px solid #d3d3d3",
              }}
            >
              <thead style={{ border: "1px solid #808080" }}>
                <tr>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    ISBN do livro
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Título do livro
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Autor do livro
                  </th>
                </tr>
              </thead>
              <tbody>
                {queryResults.map(item => {
                  return (
                    <tr key={`row_${item.isbn}`}>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.isbn}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.title}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.author}
                      </td>
                    </tr>
                  )
                })}
              </tbody>
            </table>
          </div>
        </div>
      </div>
    )
  }
}
export default ClientSearch
```

Dividindo o código em partes menores:

1. Quando o componente está montado, o lifecycle method `getDerivedStateFromProps()` é chamado e ele avaliará o estado e, se necessário, atualizará.
2. Em seguida o lifecycle method `componentDidMount()` será acionado e a função `rebuildIndex()` é invocada.
3. O mecanismo de pesquisa é então criado e configurado com as opções definidas.
4. Os dados são então indexados usando js-search.
5. Quando o conteúdo da entrada é alterado, o js-search inicia o processo de pesquisa com base no valor do `input` e retorna os resultados da pesquisa, se houver, que são apresentados ao usuário por meio do elemento `table`.

### Juntando todas as peças

Mais uma vez, para fazê-lo funcionar em seu site, você só precisará copiar [o arquivo `gatsby-node.js` localizado aqui](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/gatsby-node.js).

E ambos [modelo](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/src/templates/ClientSearchTemplate.js) e [componente de pesquisa](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/src/components/ClientSearch.js).

Emita o `gatsby develop` novamente, e se tudo correu sem problemas mais uma vez, abra o navegador de sua escolha e digite o URL `http://localhost:8000/search`, você terá uma pesquisa totalmente funcional à sua disposição, juntamente com a API do Gatsby.

Esperamos que este guia bastante extenso tenha fornecido algumas idéias sobre como implementar a pesquisa de clientes usando o js-search.

Agora vá e faça algo ótimo!
