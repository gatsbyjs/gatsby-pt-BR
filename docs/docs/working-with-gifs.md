---
<<<<<<< HEAD
title: Trabalhando com GIFs
=======
title: Working with GIFs
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1
---

Se você está construindo um blog com Gatsby, é provável que você queira incluir alguns GIFs animados: quem não gostaria de incluir um GIF de uma lontra ou de um gato dançando?

## Incluindo GIFs em componentes

Em componentes e páginas Gatsby, você vai querer importar GIFs animados em vez de usar _Gatsby Image_ por causa da forma como ele otimiza os dados da imagem para o elemento de imagem responsiva.

Aqui está um exemplo:

```jsx:title=pages/about.js
import React from 'react'

import Layout from '../components/layout'
import lontraGIF from '../gifs/otter.gif'

const AboutPage = () => (
    return (
        <Layout>
            <img src={lontraGIF} alt="Lontra dançando com um peixe" />
        </Layout>
    )
)

export default AboutPage;
```

## Incluindo GIFs em Markdown

Em posts e páginas Markdown, incluir um GIF animado é o mesmo que incluir uma imagem estática:

```markdown
<<<<<<< HEAD
![Lontra dançando com um peixe](./images/dancing-ofter.gif)
=======
![otter dancing with a fish](./images/dancing-otter.gif)
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1
```

![Lontra dançando com um peixe](./images/dancing-otter.gif)

<<<<<<< HEAD
Os GIFs animados podem ser bastante grandes em tamanho, então tenha cuidado para não sabotar a performance das suas páginas web com arquivos extremamente grandes. Você pode reduzir o tamanho do arquivo [otimizando os quadros](https://skylilies.livejournal.com/244378.html) ou convertendo-os em vídeo.
=======
Animated GIFs can be quite large in size, so be careful not to sabotage your webpages' performance with extremely large files. You could reduce file size by [optimizing the frames](https://skylilies.livejournal.com/244378.html) or converting them to video.
>>>>>>> 22a3fb4d3155774ddc223a249897020b0ee18db1

## Preocupações de acessibilidade com GIFs animados

Tenha cuidado com os GIFs que piscam e se reproduzem automaticamente pois podem causar problemas para os usuários sensíveis ao movimento. Os GIFs não devem ser reproduzidos automaticamente sempre que possível por razões de segurança. Uma técnica seria adicionar controles,utilizando-se de pacotes como [react-gif-player](https://www.npmjs.com/package/react-gif-player) como um [pacote exclusivo para o _client-side_](/docs/using-client-side-only-packages/).

Para mais informações sobre o movimento acessível:

- https://source.opennews.org/articles/motion-sick/
- https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html
