---
title: Usando a Pasta de Arquivos Estáticos
---

No geral, todo _website_ precisa de _assets_: imagens, folhas de estilo, _scripts_, etc. Quando se está usando Gatsby, nós recomendamos
[Importar _Assets_ diretamente](/docs/importing-assets-into-files/) em arquivos JavaScript, por causa dos benefícios que são adquiridos:

- _Scripts_ e folhas de estilo são minificados e empacotados juntos para evitar chamadas adicionais de rede.
- Arquivos não encontrados causam erros de compilação ao invés de erros 404 para seus usuários.
- Nomes de arquivos resultantes incluem _hashes_ de conteúdo para que você não precise se preocupar sobre o cacheamento de versões antigas pelo browser.

Entretanto, existe um **saída** para que você consiga utilizar um _asset_ fora do sistema de módulos.

## Adicionando _assets_ fora do sistema de módulos

Você consegue criar uma pasta chamada `static` na raiz de seu projeto. Cada arquivo colocado nessa pasta será copiado para a pasta `public`. Por exemplo, se você adicionar um arquivo chamado `sun.jpg` dentro da pasta `static`, ele será copiado para `public/sun.jpg`.

### Referenciando seu _asset_ estático

Você pode referenciar _assets_ da pasta `static` no seu código sem precisar de nada especial:

```jsx
render() {
  // Nota: essa é uma saída que deve ser usada com moderação!
  // Normalmente nós recomendamos usar `import` para pegar URLs de assets
  // como descrito na página "Importando _Assets_ diretamente".
  return <img src={'/logo.png'} alt="Logo" />;
}
```

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-a-local-image-from-the-static-folder-in-a-gatsby-component"
  lessonTitle="Use a local image from the static folder in a Gatsby component"
/>

### Desvantagens

Tenha em mente as desvantagens dessa implementação:

- Nenhum desses arquivos na pasta `static` será pós-processado ou minificado.
- Arquivos não encontrados não serão invocados em tempo de compilação, e irão causar um erro 404 para seus usuários
- Nomes de arquivos resultantes não terão _hashes_ de conteúdo, então você precisará adicionar argumentos na _query_ ou renomeá-los cada vez que eles mudam.

## Quando usar a pasta `static`

Normalmente, nós recomentamos importar [folhas de estilo, imagens, e assets de fonte](/docs/importing-assets-into-files/) pelo JavaScript. A pasta
`static` é util como um contorno para um pequeno número de casos comuns, como:

<<<<<<< HEAD
- Você precisa de um arquivo com um nome específico na saída do _build_,
  como [`manifest.webmanifest`](https://developer.mozilla.org/en-US/docs/Web/Manifest).
- Voce tem milhares de imagens e precisa referenciar dinamicamente seus caminhos.
- Você gostaria de adicionar um script pequeno como
  [`pace.js`](http://github.hubspot.com/pace/docs/welcome/) fora do
  código empacotado.
- Algumas bibliotecas podem ser incompatíveis com Webpack e você não tem outra opçào senão a incluir como uma tag `<script>`.
=======
- You need a file with a specific name in the build output, such as
  [`manifest.webmanifest`](https://developer.mozilla.org/en-US/docs/Web/Manifest).
- You have thousands of images and need to dynamically reference their paths.
- You want to include a small script like
  [`pace.js`](http://github.hubspot.com/pace/docs/welcome/) outside of the
  bundled code.
- Some libraries may be incompatible with Webpack and you have no other option but to include it as a `<script>` tag.
- You need to import JSON file that doesn't have a consistent schema, like [TopoJSON files](https://en.wikipedia.org/wiki/GeoJSON#TopoJSON), which is difficult to handle with GraphQL. Note that importing JSON files directly inside a page, a template, or a component using `import` syntax results in adding that file to the app bundle and increasing the size of all site's pages. Instead, it's better to place your JSON file inside the `static` folder and use the dynamic import syntax (`import('/static/myjson.json')`) within the `componentDidMount` lifecycle or the `useEffect` hook.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f
