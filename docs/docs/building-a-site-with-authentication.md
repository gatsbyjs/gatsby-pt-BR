---
title: Construindo um site com autenticação
---

Muitos sites exigem que os usuários sejam autenticados para proteger dados privados.

## Compreendendo a autenticação entre cliente e servidor

Em muitos sites modernos, o [cliente](/docs/glossary#client-side) -- ou [frontend](/docs/glossary#frontend) -- é [desacoplado](/docs/glossary#decoupled) do [backend](/docs/glossary#backend). Esse padrão é como o Gatsby funciona para combinar dados de uma infinidade de fontes (backends) para facilitar a construção do front-end.

Para fornecer funcionalidade de autenticação, outro serviço deve ser aproveitado e conectado ao Gatsby. Existem muitas tecnologias de _open source_ que podem fornecer essa funcionalidade. Alguns exemplos são:

- Um aplicação Node.js usando Passport.js
- Uma API Ruby on Rails usando Devise

Outra opção são tecnologias de terceiros como:

- Firebase
- Auth0
- AWS Amplify
- Netlify Identity

Essas ferramentas seguem um processo para verificar um usuário no cliente em relação a um serviço de autenticação. O serviço retorna um _token_ que o cliente pode usar para acessar dados protegidos. Este diagrama visualiza o processo:

![Diagrama do Gatsby utilizando um serviço de autenticação para buscar dados de uma API](./images/basic-auth.png)

1. Inicialmente, uma requisição é feita de um Gatsby site (o cliente) para um serviço de autenticação para realizar uma ação como registrar um novo usuário ou _login_.

2. Se as credenciais (como o _username_ e _password_) fornecidos pelo cliente corresponderem a um usuário no serviço de autenticação, o serviço retornará um _token_ (por exemplo, um JSON Web Token, abreviado como JWT), então o usuário tem a chave que ele pode usar para provar quem ele diz ser. Os dados do usuário retornados podem ser guardados na aplicação Gatsby passando eles para os componentes usando um componente de Provider por meio da React Context API e [`wrapRootElement` API](/docs/browser-apis/#wrapRootElement) do Gatsby.

3. Com a chave o cliente pode fazer requisições para uma fonte externa de dados como uma API (o servidor) onde os dados protegidos são armazenados. A chave é exclusiva para um usuário específico e permite que o cliente acesse seus dados específicos.

4. O servidor retorna os dados de volta ao cliente que podem ser usados para passar informações aos componentes.

_**Note**: esse é o mesmo padrão que outros sites criados com o React(como Create React App) precisam seguir._

## Implementando autenticação em um site Gatsby

Há algumas coisas a serem observadas ao implementar a autenticação em um site do Gatsby, por causa de como o Gatsby cria páginas de forma exclusiva e renderiza ativos estáticos com recursos dinâmicos.

### Configurando Rotas Somente para o Cliente

Com o Gatsby, você pode criar áreas restritas no seu aplicativo usando [rotas do cliente](/docs/building-apps-with-gatsby/#client-only-routes).

Gatsby é um pouco [diferente de um aplicativo tradicional do React](/docs/adding-app-and-website-functionality/#differences-between-gatsby-and-other-react-apps) em como suas rotas e páginas são criadas. Como os arquivos HTML estáticos gerados pelo Gatsby ficam em um servidor de arquivos, você não pode controlar programaticamente o acesso a esses arquivos (por exemplo: um usuário pode adivinhar ou digitar um URL e navegar diretamente para a página). Como a seção [adicionando funcionalidade de aplicativo e site](/docs/adding-app-and-website-functionality/#client-only-routes) página de visão geral demonstra, é possível criar rotas apenas para clientes para rotear um usuário entre páginas usando um roteador baseado no React, em vez de navegar entre diferentes arquivos HTML estáticos em um servidor.

Aproveitar esse roteamento do lado do cliente permite proteger ou personalizar suas rotas. Usando a [`@reach/router` library](https://reach.tech/router/), que vem instalada com o Gatsby, você pode configurar um roteador em uma página e controlar qual componente é carregado quando uma determinada rota é chamada e verifique a existência de uma variável como o estado de autenticação antes de veicular o conteúdo.

<!-- prettier-ignore -->
```jsx
<Router>
  {isAuthenticated ? <PrivateRoute /> : <Login />}
</Router>
```

Exemplos de código mais específicos para esse padrão estão descritos em [Rotas somente para clientes e guia de autenticação do usuário](/docs/client-only-routes-and-user-authentication/#implementing-client-only-routes).

### Protegendo o código contra o acesso global ao navegador durante a compilação

Objetos globais acessíveis no navegador como `localStorage` não estão disponíveis enquanto um site do Gatsby está em construção, porque a compilação é executada em um ambiente Node.js.

No entanto, alguns serviços de terceiros podem tentar acessar o `localStorage` ou o objeto`window` com métodos internos. Para impedir que esses trechos quebrem a compilação, essas invocações devem ser agrupadas em condições ou hooks, `useEffect`, para verificar se o código está em execução no navegador e é ignorado durante o processo de compilação:

```javascript
import app from "firebase/app"

...

if (typeof window !== 'undefined') { // highlight-line
  app.initializeApp(config)
} // highlight-line
```

Mais informações sobre erros relacionados à compilação estão disponíveis no guia em [debugging artefatos HTML](/docs/debugging-html-builds/).

## Exemplo do mundo real: loja do Gatsby

A [loja do Gatsby](https://github.com/gatsbyjs/store.gatsbyjs.org) é um aplicativo ao vivo criado com o Gatsby que implementa a autenticação usando o Auth0.

[Funções utilitárias](https://github.com/gatsbyjs/store.gatsbyjs.org/blob/master/src/utils/auth.js) no repositório da Gatsby Store, usam as APIs do Auth0 para autenticar usuários com o GitHub e englobam as APIs do Auth0 para garantir que [alguns dos códigos Auth0 são executados apenas no navegador](https://github.com/gatsbyjs/store.gatsbyjs.org/blob/master/src/utils/auth.js#L3).

Para proteger o conteúdo autenticado com uma rota privada, um `<Router />` é implementado no componente `<PrivateRoute />` que verifica se um usuário está autenticado ou o redireciona para `/ login`.

```jsx
// import ...
const PrivateRoute = ({ component: Component, ...rest }) => {
  if (
    !isAuthenticated() &&
    isBrowser &&
    window.location.pathname !== `/login`
  ) {
    // If we’re not logged in, redirect to the home page.
    navigate(`/app/login`)
    return null
  }

  return (
    <Router>
      <Component {...rest} />
    </Router>
  )
}
```

Esse padrão de rota particular também é abordado no [tutorial sobre como criar um site com autenticação](/tutorial/authentication-tutorial/#controller-private-routes).

## Leitura adicional

Se você quiser obter mais informações sobre áreas autenticadas com Gatsby, isso (lista não exaustiva) pode ajudar:

- [Criando um site com autenticação de usuário](/tutorial/authentication-tutorial), um tutorial avançado do Gatsby
- [Exemplo de "autenticação simples" do repositório Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/examples/simple-auth)
- [Versão ao vivo do exemplo "autenticação simples"](https://simple-auth.netlify.com/)
- [Uma aplicação de email Gatsby](https://github.com/DSchau/gatsby-mail), usando a API do React Context para lidar com a autenticação
- [Adicione autenticação aos seus aplicativos Gatsby com Auth0](/blog/2019-03-21-add-auth0-to-gatsby-livestream/) (livestream com Jason Lengstorf)
- [Adicione autenticação aos seus aplicativos Gatsby com Okta](https://www.youtube.com/watch?v=7b1iKuFWVSw&t=9s)
- [Outras postagens relacionadas à autenticação no blog Gatsby](/blog/tags/authentication/)
