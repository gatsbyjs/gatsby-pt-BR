---
title: Conheça os Blocos de Construção do Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Na [seção anterior](/tutorial/part-zero/), você preparou o seu ambiente de desenvolvimento instalando os softwares necessários e criando o seu primeiro site com Gatsby utilizando o [**“hello world” starter**](https://github.com/gatsbyjs/gatsby-starter-hello-world). Agora, vamos ir um pouco mais fundo no código gerado pelo starter.

## Utilizando Gatsby starters

Na [parte zero do tutorial](/tutorial/part-zero/), você criou um novo site com o “hello world” _starter_ rodando o seguinte comando:

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Ao criar um novo site com Gatsby, você pode usar a seguinte estrutura de comando, que serve para qualquer starter existente:

```shell
gatsby new [NOME_DO_DIRETORIO_DO_SITE] [URL_DO_STARTER_NO_GITHUB]
```

Se você não colocar a URL no final do comando, o Gatsby vai automaticamente criar um site com base no [starter default](https://github.com/gatsbyjs/gatsby-starter-default). Mas, para essa seção do tutorial, fique com o site “Hello World” que você já criou na parte zero. Você pode aprender a como [modificar starters](/docs/modifying-a-starter) na documentação.

### ✋ Abra o código

No seu editor de código, abra o código gerado para o seu site “Hello World” e dê uma olhada nos diferentes diretórios e arquivos contidos no diretório ‘hello-world’. Deve ser algo parecido com isto:

![Hello World project in VS Code](01-hello-world-vscode.png)

_Nota: Novamente, o editor mostrado aqui é o Visual Studio Code. Se você estiver usando um editor diferente, vai parecer um pouco diferente._

Vamos dar uma olhada no código da página inicial.

> 💡 Se você parou o seu servidor de desenvolvimento depois de rodar `gatsby develop` na seção anterior, inicie ele novamente — chegou a hora de fazermos algumas alterações ao hello-world site!

## Familiarizando-se com páginas Gatsby

Abra o diretório `/src` no seu editor de código. Dentro tem um diretório único: `/pages`.

Abra o código em `src/pages/index.js`. O código nesse arquivo cria um componente que contém uma div única e um pouco de texto — adequadamente, “Hello world!”

### ✋ Faça alterações na página inicial do “Hello World”

1.  Mude o texto “Hello World!” para “Hello Gatsby!” e salve o seu arquivo. Se as suas páginas estão lado a lado, você pode ver que as alterações no seu código e conteúdo são refletidas quase instantaneamente no navegador depois de salvar o arquivo.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./02-demo-hot-reloading.mp4"></source>
  <p>Desculpe! O seu browser não suporta este video.</p>
</video>

> 💡 O Gatsby utiliza **hot reloading** para acelerar o seu processo de desenvolvimento. Essencialmente, quando você está rodando um servidor de desenvolvimento do Gatsby, os arquivos do site estão sendo “observados” em background — toda vez que você salvar um arquivo, suas alterações vão ser refletidas imediatamente no navegador. Você não precisa recarregar a página ou reiniciar o servidor de desenvolvimento — suas alterações simplesmente aparecem.

2.  Agora que você pode tornar suas alterações um pouco mais visíveis. Tente substituir o código em `src/pages/index.js` pelo código abaixo e salve novamente. Você verá alterações no texto — a cor do texto será roxa e o tamanho da fonte maior.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

> 💡 Abordaremos mais sobre estilo no Gatsby na [**parte dois**](/tutorial/part-two/) do tutorial.

3.  Remova o estilo do tamanho da fonte, altere o texto “Hello Gatsby!” para um cabeçalho nível um, e adicione um parágrafo abaixo do header.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  {/* highlight-start */}
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
  {/* highlight-end */}
  </div>
)
```

![Mais alterações com hot reloading](03-more-hot-reloading.png)

4.  Adicione uma imagem. (Nesse caso, uma imagem aleatória do Unsplash).

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
    {/* highlight-next-line */}
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

![Adicione uma imagem](04-add-image.png)

### Espere… HTML no nosso JavaScript?

_Se você é familiar com React e JSX, sinta-se à vontade para pular essa seção._ Se você não trabalhou com o framework React antes, você pode estar se perguntando o que o HTML está fazendo em um função JavaScript. Ou por que estamos importando `react` na primeira linha, mas aparentemente não estamos usando em nenhum lugar. Esse híbrido “HTML-in-JS” é na verdade uma extensão de sintaxe do JavaScript, para o React, chamada JSX. Você pode acompanhar este tutorial sem experiência anterior com o React, mas se tiver curiosidade, aqui está uma breve cartilha…

Considere o conteúdo original do arquivo `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

Em JavaScript puro, parece mais com isso:

```javascript:title=src/pages/index.js
import React from "react"

export default () => React.createElement("div", null, "Hello world!")
```

Agora você pode identificar o uso da importação `'react'`! Mas espere. Você está escrevendo JSX, não HTML e JavaScript puro. Como o navegador lê isso? A resposta curta: ele não lê. Sites Gatsby vem com ferramentas já configuradas para converter seu código fonte em algo que os navegadores possam interpretar.

## Construindo com componentes

A página inicial na qual você estava editando foi criada com a definição de um componente de página. O que exatamente é um “componente”?

Amplamente definido, um componente é um bloco de código para o seu site; É um trecho de código independente que descreve uma seção da UI (interface do usuário).

Gatsby é baseado no React. Quando falamos sobre o uso e definição de **componentes**, estamos realmente falando de **componentes React** — partes de código independentes (geralmente escritas com JSX) que podem aceitar entrada e retornar elementos React que descrevem uma seção da interface do usuário.

Uma das grandes mudanças mentais que você faz ao começar a construir com componentes (se você já é um desenvolvedor) é que agora seu CSS, HTML e JavaScript estão fortemente acoplados e geralmente vivem mesmo no mesmo arquivo.

Embora seja uma mudança aparentemente simples, isso tem implicações profundas em como você pensa em criar sites.

Veja o exemplo da criação de um botão personalizado. No passado, você criaria uma classe CSS (talvez `.primary-button`) com o seu estilo customizado e usaria ela sempre que você quiser aplicar esses estilos. Por exemplo:

```html
<button class="primary-button">Click me</button>
```

No mundo dos componentes, você cria um componente `PrimaryButton` com os estilos do seu botão e usaria ao longo do seu site como:

<!-- prettier-ignore -->
```jsx
<PrimaryButton>Click me</PrimaryButton>
```

Os componentes se tornam elementos construtivos do seu site. Ao invés de se limitar a estrutura que o navegador fornece, e.g. `<button />`, você pode facilmente criar uma nova estrutura que elegantemente satisfaz as necessidades do seus projetos.

### ✋ Usando componentes de página

Qualquer componente React que estiver dentro de `src/pages/*.js` se tornará automaticamente uma página. Vamos ver isso na prática.

Você já possui um arquivo `src/pages/index.js` que veio com o “Hello World” starter. Vamos criar uma página "Sobre".

1.  Crie um novo arquivo em `src/pages/about.js`, copie o código abaixo no novo arquivo e salve.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div style={{ color: `teal` }}>
    <h1>About Gatsby</h1>
    <p>Such wow. Very React.</p>
  </div>
)
```

2.  Abra o seguinte link no seu navegador: `http://localhost:8000/about/`.

![Nova página "Sobre"](05-about-page.png)

Apenas colocando um componente React no arquivo `src/pages/about.js`, agora você tem uma página acessível em `/about`.

### ✋ Utilizando subcomponentes

Digamos que a página inicial e a página "Sobre" ficaram muito grandes e você estava reescrevendo muitas coisas. Nesse caso, você pode utilizar subcomponentes para dividir a interface do usuário em partes reutilizáveis. Ambas as páginas tem cabeçalhos `<h1>` — crie um componente que descreverá um `Header`.

1.  Crie um novo diretório `components` dentro de `src` e um arquivo dentro desse diretório chamado `header.js`.
2.  Adicione o seguindo trecho de código para o novo arquivo em `src/components/header.js`.

```jsx:title=src/components/header.js
import React from "react"

export default () => <h1>This is a header.</h1>
```

3.  Modifique o arquivo `about.js` para importar o componente `Header`. Substitua o `h1` pelo `<Header />`:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header" // highlight-line

export default () => (
  <div style={{ color: `teal` }}>
    <Header /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Adicionando um componente de Header](06-header-component.png)

No navegador, o texto “About Gatsby” do header deve ser substituído por “This is a header.” Mas você não quer que a página de “About” tenha o título “This is a header.” Você quer que ela tenha: “About Gatsby”.

4.  Volte para `src/components/header.js` e faça as seguintes alterações:

```jsx:title=src/components/header.js
import React from "react"

export default props => <h1>{props.headerText}</h1> {/* highlight-line */}
```

5.  Volte para `src/pages/about.js` e faça as seguintes alterações:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Passando dados para o header](07-pass-data-header.png)

Agora você deve ver o header “About Gatsby” novamente!

### O que são “props”?

Anteriormente, você definiu os componentes React como trechos de código reutilizáveis que descrevem uma interface do usuário. Para deixar esses trechos dinâmicos, você precisa ser capaz de fornecer dados diferentes. Você faz isso com a entrada chamada "props". Props são (adequadamente) propriedades fornecidas aos componentes do React.

Na página `about.js` você passou uma propriedade `headerText` com o valor `"About Gatsby"` para o subcomponente importado `Header` :

```jsx:title=src/pages/about.js
<Header headerText="About Gatsby" />
```

No `header.js`, o componente de header espera receber a propriedade `headerText` (porque você o escreveu para esperar isso). Para que você possa acessá-lo assim:

```jsx:title=src/components/header.js
<h1>{props.headerText}</h1>
```

> 💡 Em JSX, você pode incorporar qualquer expressão JavaScript envolvendo ela com `{}`. É assim que você pode acessar a propriedade `headerText` (ou “prop!”) a partir do objeto “props”.

Se você tivesse passado outra propriedade para o seu componente `<Header />`, igual a...

```jsx:title=src/pages/about.js
<Header headerText="About Gatsby" arbitraryPhrase="is arbitrary" />
```

...você poderia acessar a propriedade `arbitraryPhrase` com: `{props.arbitraryPhrase}`.

6.  Para enfatizar como isso torna seus componentes reutilizáveis, adicione um componente extra `<Header />` à página "Sobre" e adicione o seguinte código ao arquivo `src/pages/about.js` e salve.

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" />
    <Header headerText="It's pretty cool" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Header duplicado para mostrar reusabilidade](08-duplicate-header.png)

E aí está; Um segundo cabeçalho - sem reescrever nenhum código - passando dados diferentes com props.

### Utilizando componentes de layout

Componentes layout são para seções de um site que você deseja compartilhar em várias páginas. Por exemplo, sites do Gatsby geralmente têm um componente de layout com cabeçalho e rodapé compartilhados. Outras coisas comuns a serem adicionadas aos layouts incluem uma barra lateral e/ou um menu de navegação.

Você vai explorar componentes de layout na [**parte três**](/tutorial/part-three/).

## Navegando entre páginas

Muitas vezes, você precisa navegar entre páginas — Vamos ver sobre navegação em um site Gatsby.

### ✋ Utilizando o componente `<Link />`

1.  Abra o componente da página index (`src/pages/index.js`), importe o component `<Link />` do Gatsby, adicione o  `<Link />` acima do header, e dê a ele uma propriedade `to` com o valor `"/contact/"` para o nome do caminho:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import Header from "../components/header"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link> {/* highlight-line */}
    <Header headerText="Hello Gatsby!" />
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

Ao clicar no novo link "Contato" na página inicial, você verá...

![Página de erro 404 de desenvolvimento do Gatsby](09-dev-404.png)

...a página de erro 404 de desenvolvimento do Gatsby. Por que? Pois você está tentando navegar para uma página que ainda não existe.

2.  Agora você precisa criar um componente de página para a sua nova página de "Contato" em `src/pages/contact.js` e colocar um link de volta para a página inicial:

```jsx:title=src/pages/contact.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Link to="/">Home</Link>
    <Header headerText="Contact" />
    <p>Send us a message!</p>
  </div>
)
```

Depois que você salvar o arquivo, você deve ver a página contato e conseguir acessar através do link na página inicial.

<video controls="controls" loop="true">
  <source type="video/mp4" src="./10-linking-between-pages.mp4"></source>
  <p>Desculpa, seu navegador não suporta este vídeo.</p>
</video>

O componente `<Link />` do Gatsby é utilizado para navegar entre páginas do seu site. Para links externos para páginas não tratadas pelo seu site Gatsby, use a tag padrão do HTML `<a>`.

## Fazendo deploy do seu site Gatsby

O Gatsby.js é um _gerador de site moderno_, o que significa que não há servidores para configurar ou banco de dados complicados para fazer deploy. Em vez disso, o comando `build` do Gatsby produz um diretório de arquivos HTML e JavaScript estáticos que você pode implantar em um serviço de hospedagem de site estático.

Tente usar o [Surge](http://surge.sh/) para fazer o deploy do seu primeiro site Gatsby. O Surge é um dos muitos "hosts de sites estáticos" que possibilitam o deploy de sites Gatsby.

Se você não instalou o Surge anteriormente, abra uma nova janela do terminal e instale a partir dessa linha de comando:

```shell
npm install --global surge

# Agora crie um conta gratuita com eles
surge login
```

Em seguida, crie seu site executando o seguinte comando no terminal na raiz do site (dica: verifique se você está executando este comando na raiz do site, neste caso na pasta hello-world, que você pode fazer abrindo uma nova aba na mesma janela usada para executar o `gatsby develop`):

```shell
gatsby build
```

O build deve levar de 15 a 30 segundos. Após a conclusão do build, é interessante dar uma olhada nos arquivos que o comando `gatsby build` acabou de preparar para deploy.

Dê uma olhada na lista dos arquivos gerados digitando o seguinte comando de terminal na raiz do seu site, o que permitirá que você veja o diretório `public`:

```shell
ls public
```

Por fim, faça o deploy do seu site publicando os arquivos gerados em surge.sh.

```shell
surge public/
```

> Note que precisa pressionar o botão `enter` depois que ver a mensagem `domain: some-name.surge.sh` em seu terminal.

Quando o processo de deploy terminar, você verá no seu terminal algo como:

![Captura de tela do processo de deploy de site Gatsby com Surge](surge-deployment.png)

Abra o endereço da web listado na linha inferior (`lowly-pain.surge.sh` neste
caso) e você verá seu site recém-publicado! Ótimo trabalho!

## ➡️ O que vem a seguir?

Nessa seção você:

- Aprendeu sobre os starters do Gatsby, e como utilizá-los para criar novos projetos
- Aprendeu sobre a sintaxe JSX
- Aprendeu sobre componentes
- Aprendeu sobre componentes de página do Gatsby e subcomponentes 
- Aprendeu sobre as “props” do React e sobre reutilizar componentes

Agora, vamos em frente para [**adicionar estilos no nosso site**](/tutorial/part-two/)!
