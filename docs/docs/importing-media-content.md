---
title: Importando Conteúdo de Mídia
---

"Conteúdo de mídia" é um termo amplo que geralmente inclui imagens, vídeos, documentos e arquivos que são exibidos em seu site. Para sites Gatsby, você tem várias opções para importar conteúdo de mídia dependendo do tipo:

## Imagens, SVG e PDFs

- [Gráficos de imagem podem ser importados](/docs/importing-assets-in-files/) com Webpack e consultados com GraphQL.
- Imagens também podem ser [incluidas da 'pasta static'](/docs/static-folder/).
- O conteúdo SVG pode ser incorporado no JSX. Aqui está um [prático conversor JSX](https://transform.tools/svg-to-jsx).
- O SVG pode ser incluído em tags `img` ou fundos CSS. [Dicas de SVG do CSS Tricks](https://css-tricks.com/using-svg/).
- Para arquivos PDF, recomendamos incorporar uma [imagem do PDF](https://helpx.adobe.com/acrobat/using/exporting-pdfs-file-formats.html) com [texto alternativo](https://a11y-101.com/development/infographics), e fornecer um link para baixar um [PDF marcado](https://helpx.adobe.com/acrobat/using/creating-accessible-pdfs.html).

## Assets de vídeo

Como imagens, assets de vídeo apresentam muitas opções e requisitos para suporte a cross-browsers. Saiba mais sobre os vídeos incorporados na página de documentos Gatsby em [trabalhando com vídeo](/docs/working-with-video/).

## Canvas e WebGL

O elemento HTML5 `<canvas>` fornece um espaço para desenho bidimensional em um ambiente web. Em Gatsby e React, incluir uma biblioteca como [react-konva](https://github.com/konvajs/react-konva) ou uma das bibliotecas de comparação para cortar o boilerplate, pode facilitar o desenho dentro do `canvas`.

[WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Tutorial/Getting_started_with_WebGL), por outro lado, cria um espaço tridimensional em um ambiente web usando o elemento `<canvas>`. Bibliotecas como [Three.js](https://threejs.org/) são frequentemente usadas para habilitar experiências WebGL em aplicativos React.

> A utilização de canvas e/ou WebGL pode exigir a modificação da configuração do seu Webpack. Você tem experiência em fazer isso funcionar no seu site Gatsby? Contribua para os documentos adicionando mais detalhes a esta página.
