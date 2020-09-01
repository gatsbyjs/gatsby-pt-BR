---
title: Gatsby Link API
---

Para navegação interna o Gatbsy disponibiliza o componente `<Link>`, assim como a função `navigate` que ajuda na navegação programática.

O `<Link>` possibilita conectar páginas internas, além de permitir o uso de um poderoso recurso de desempenho chamado _preloading_ (pré-carregamento). O preloading faz um pré-carregamento de recursos para que esses já estejam disponíveis no momento que o usuário precisar. Um `IntersectionObserver` é utilizado para fazer uma requisição de baixa prioridade quando o `<Link>` está visível na tela enquanto que um evento de `onMouseOver` é responsável por disparar uma requisição de alta prioridade quando for identificada a probabilidade de que o usuário fará tal navegação.

O `<Link>` é um encapsulamento do [componente de Link do @reach/router](https://reach.tech/router/api/Link), adicionando funcionalidades específicas para o Gatsby. Todas as props são passadas para o componente de `Link` do @reach/router.

## Como usar Gatsby Link

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-why-and-how-to-use-gatsby-s-link-component"
  lessonTitle="Por que e como utilizar o componente de Link do Gatsby"
/>

### Substitua as tags `a` pela tag `Link` em links locais

Em qualquer situação que você queira criar um link entre páginas dentro do mesmo site, use o componente `Link` ao invés da tag `a`.

```jsx
import React from "react"
// highlight-next-line
import { Link } from "gatsby"

const Page = () => (
  <div>
    <p>
      {/* highlight-next-line */}
      Confira o meu <Link to="/blog">blog</Link>!
    </p>
    <p>
      {/* Note that external links still use `a` tags. */}
      Siga-me no <a href="https://twitter.com/gatsbyjs">Twitter</a>!
    </p>
  </div>
)
```

### Personalize o link ativo

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-add-custom-styles-for-the-active-link-using-gatsby-s-link-component"
  lessonTitle="Personalize o link ativo no momento usando componente Link do Gatsby"
/>

Por vezes, quer-se indicar a página que está sendo visualizada no momento através de alterações visuais no link correspondente a mesma.

O `Link` tem duas opções de estilização de links ativos:

- `activeStyle` - estilos que são aplicados ao `Link` quando seu endereço estiver ativo
- `activeClassName` - classe que será aplicada ao `Link` quando seu endereço estiver ativo

Por exemplo, para tornar o link ativo vermelho, qualquer uma das seguintes abordagens é válida:

```jsx
import React from "react"
import { Link } from "gatsby"

const SiteNavigation = () => (
  <nav>
    <Link
      to="/"
      {/* highlight-start */}
      {/* Assumindo que a classe `active` foi definida no seu CSS*/}
      activeClassName="active"
      {/* highlight-end */}
    >
      Home
    </Link>
    <Link
      to="/sobre/"
      {/* highlight-next-line */}
      activeStyle={{ color: "red" }}
    >
      Sobre
    </Link>
  </nav>
)
```

### Use `getProps` para estilização avançada de links

O componente `<Link>` do Gatsby tem uma prop chamada `getProps` que pode ser útil para estilos avançados. Ela passa um objeto com as seguintes propriedades:

- `isCurrent` - true se o`location.pathname` for exatamente o mesmo que o `to` do `Link`
- `isPartiallyCurrent` - true se o`location.pathname` começar com a prop `to` do `Link`
- `href` - o valor da prop `to`
- `location` - o objeto `location` da página

Mais informações estão disponíveis na [`documentação do @reach/router`](https://reach.tech/router/api/Link).

### Mostrar estilos ativos para links parciais e links pais

Por padrão, os props `activeStyle` e`activeClassName` são configurados no componente `<Link>` apenas se a URL atual for _exatamente_ igual a sua prop `to`. Às vezes, convém estilizar um `<Link>` como ativo, caso sua prop `to` corresponda parcialmente à URL atual. Por exemplo:

- Você pode querer que `<Link to="/blog">` fique ativo quando estiver na URL `/blog/hello-world`
- Ou que `<Link to="/gatsby-link">` fique ativo no endereço `/gatsby-link/#passing-state-through-link-and-navigate`

Em casos como esses, adicione a prop `partiallyActive` ao componente `<Link>` e o estilo também será aplicado, mesmo que a prop `to` seja parcialmente equivalente:

```jsx
import React from "react"
import { Link } from "gatsby"

const Header = <>
  <Link
    to="/articles/"
    activeStyle={{ color: "red" }}
    {/* highlight-next-line */}
    partiallyActive={true}
  >
    Artigos
  </Link>
</>;
```

_**Nota:** Disponível no Gatsby V2.1.31. Se você encontrar problemas, verifique sua versão e/ou atualização._

### Passe o estado como props para as páginas linkadas

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-include-information-about-state-in-navigation-with-gatsby-s-link-component"
  lessonTitle="Incluia informações sobre o estado na navegação com o componente de link de Gatsby"
/>

Às vezes, você deseja passar dados da página de origem para a página de destino. Você pode fazer isso passando um prop `state` para o componente `Link` ou chamando a função `navigate`. A página clicada terá um objeto `location` contendo uma propriedade `state` que contém os dados passados.

```jsx
const PhotoFeedItem = ({ id }) => (
  <div>
    {/* (ignorando o markup do item de feed por brevidade) */}
    <Link
      to={`/photos/${id}`}
      {/* highlight-next-line */}
      state={{ fromFeed: true }}
    >
      Ver Foto
    </Link>
  </div>
)

// highlight-start
const Photo = ({ location, photoId }) => {
  if (location.state.fromFeed) {
    // highlight-end
    return <FromFeedPhoto id={photoId} />
  } else {
    return <Photo id={photoId} />
  }
}
```

### Substitua o histórico para alterar o comportamento do botão "voltar"

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-replace-navigation-history-items-with-gatsby-s-link-component"
  lessonTitle="Substitua itens do histórico de navegação usando o componente de Link do Gatsby"
/>

Existem alguns casos em que pode fazer sentido modificar o comportamento do botão "voltar". Por exemplo, se você criar um fluxo no qual o usuário possa escolher algo, e então seja direcionado para outra página que pergunte "você tem certeza?". Ao confirmar o usuário é finalmente direcionado para uma página de confirmação. Nesse caso pode ser desejável pular a página "você tem certeza?" no fluxo de retorno do botão "voltar".

Nesse caso use o objeto `replace` para substituir o URL atual no histórico pelo destino do `Link`.

```jsx
import React from "react"
import { Link } from "gatsby"

const AreYouSureLink = () => (
  <Link
    to="/confirmation/"
    {/* highlight-next-line */}
    replace
  >
    Sim, tenho certeza
  </Link>
)
```

## Como usar a função `navigate`

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-navigate-to-a-new-page-programmatically-in-gatsby"
  lessonTitle="Navegue para uma nova página programaticamente usando Gatsby"
/>

Às vezes, você precisa navegar para as páginas programaticamente, como durante o envio de formulários. Nesses casos, o `Link` não funcionará.

_**Note:** `navigate` era chamado de `navigateTo` originalmente. O `navigateTo` foi descontinuado no Gatsby v2 e será removido na próxima versão principal._

Em vez disso, o Gatsby exporta uma função `navigate` que aceita os argumentos `to` e `options`.

| Argumento         | Obrigatório | Descrição                                                                                                         |
| ----------------- | ----------- | ----------------------------------------------------------------------------------------------------------------- |
| `to`              | sim         | A página de destino (e.g. `/blog/`).                                                                              |
| `options.state`   | não         | Um objeto. Os valores aqui passados estarão disponíveis em `location.state` dentre as props da página de destino. |
| `options.replace` | não         | Valor booleano. Se true, sobrescreve o valor da URL atual no histórico.                                           |

Por padrão, o `navigate` opera da mesma maneira que o clique no`Link`.

```jsx
import React from "react"
import { navigate } from "gatsby" // highlight-line

const Form = () => (
  <form
    onSubmit={event => {
      event.preventDefault()

      // TODO: fazer algo com os valores do form
      // highlight-next-line
      navigate("/form-submitted/")
    }}
  >
    {/* (ignorando os inputs do form por brevidade) */}
  </form>
)
```

### Adicionar estado à navegação programática

Para incluir informações de estado, inclua um objeto com uma propriedade `state` com os valores desejados.

```jsx
import React from "react"
import { navigate } from "gatsby"

const Form = () => (
  <form
    onSubmit={event => {
      event.preventDefault()

      // A implementação desta função é um exercício para o leitor.
      const formValues = getFormValues()

      navigate(
        "/form-submitted/",
        // highlight-start
        {
          state: { formValues },
        }
        // highlight-end
      )
    }}
  >
    {/* (ignorando os inputs do form por brevidade) */}
  </form>
)
```

A partir da página de destino é possível acessar o estado `location`, conforme demonstrado em [Passe o estado como props para as páginas linkadas](#passe-o-estado-como-props-para-as-paginas-linkadas).

### Substitua o histórico na programação programática

Se o objetivo na navegação é substituir o histórico ao invés de inserir uma nova entrada, adicione o objeto `replace` com um valor de `true` ao argumento `options` de `navigate`.

```jsx
import React from "react"
import { navigate } from "gatsby"

const Form = () => (
  <form
    onSubmit={event => {
      event.preventDefault()

      // TODO: fazer algo com os valores do form
      navigate(
        "/form-submitted/",
        // highlight-next-line
        { replace: true }
      )
    }}
  >
    {/* (ignorando os inputs do form por brevidade) */}
  </form>
)
```

## Adicione prefixo aos endereços usando `withPrefix`

É comum hospedar sites em um subdiretório de um site. Gatsby permite que você [defina o prefixo do caminho do seu site](/docs/path-prefix/). Após fazer isso, o componente `<Link>` de Gatsby manipulará automaticamente a construção da URL correta em desenvolvimento e produção.

Para endereços construídos manualmente, há uma função auxiliar, `withPrefix`, que adicina o prefixo nos endereços em produção (mas não durante o desenvolvimento, pois os endereços não precisam ser prefixados).

```jsx
import { withPrefix } from "gatsby"

const IndexLayout = ({ children, location }) => {
  const isHomepage = location.pathname === withPrefix("/")

  return (
    <div>
      <h1>Bem vindo {isHomepage ? "home" : "a bordo"}!</h1>
      {children}
    </div>
  )
}
```

## Lembrete: use `<Link>` apenas para links internos!

O uso desse componente destina-se apenas para páginas internas, pois estas são tratadas pelo Gatsby. Para links extenrnos (páginas em outros domínios ou páginas no mesmo domínio não tratadas pelo site atual do Gatsby), use o elemento `<a>` normal.

Às vezes, você não saberá com antecedência se um link será interno ou não, como quando os dados são provenientes de um CMS. Nesses casos, pode ser útil criar um componente que inspecione o endereço e determine se este deverá ser renderizado com o `<Link>` de Gatsby ou com uma tag `<a>`.

A decisão se um link é interno ou não depende do site em questão. Pode ser necessário personalizar a heurística para o seu ambiente, mas o exemplo a seguir pode ser um bom ponto de partida:

```jsx
import { Link as GatsbyLink } from "gatsby"

// Como os elementos DOM <a> não podem receber activeClassName
// e parcialmenteActive, desestruture a prop aqui e
// passe apenas para o GatsbyLink
const Link = ({ children, to, activeClassName, partiallyActive, ...other }) => {
  // Adapte o seguinte teste ao seu ambiente.
  // Esse exemplo supõe que qualquer link interno (destinado ao Gatsby)
  // começará exatamente com uma barra e qualquer outra coisa é externa.
  const internal = /^\/(?!\/)/.test(to)

  // Use o Link do Gatsby para links internos e <a> para outros
  if (internal) {
    return (
      <GatsbyLink
        to={to}
        activeClassName={activeClassName}
        partiallyActive={partiallyActive}
        {...other}
      >
        {children}
      </GatsbyLink>
    )
  }
  return (
    <a href={to} {...other}>
      {children}
    </a>
  )
}

export default Link
```

### Download de arquivos

Você pode também verificar se o link concerne download de algum arquivo.

```jsx
  const file = /\.[0-9a-z]+$/i.test(to)

  ...

  if (internal) {
    if (file) {
        return (
          <a href={to} {...other}>
            {children}
          </a>
      )
    }
    return (
      <GatsbyLink to={to} {...other}>
        {children}
      </GatsbyLink>
    )
  }
```

## Recomendações para navegação programática no aplicativo

Nem `<Link>` nem `navigate` podem ser usados para navegação na própria página usando hash ou parâmetro de consulta. Se você precisar desse comportamento, use uma âncora ou importe o pacote `@reach/router` - que já é uma dependência do Gatsby - e utilize sua função `navigate`, da seguinte forma:

```jsx
import { navigate } from '@reach/router';

...

onClick = () => {
  navigate('#some-link');
  // OR
  navigate('?foo=bar');
}
```

## Recursos adicionais

- [Tutorial de autenticação para rotas do cliente](/tutorial/authentication-tutorial/)
- [Roteamento: Obtendo dados de localização das props](/docs/location-data-from-props/)
- [`gatsby-plugin-catch-links`](https://www.gatsbyjs.org/packages/gatsby-plugin-catch-links/) identificar automaticamente links locais em arquivos Markdown e substitui seu comportamento para o mesmo utilizado pela função `navigate` do `gatsby-link`
