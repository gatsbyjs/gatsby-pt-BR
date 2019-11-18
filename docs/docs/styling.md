---
title: Estilizando
overview: true
---

Há várias formas de estilizar o seu _website_. Eles podem ser agrupadas em três abordagens de estilização:

- [**Arquivos CSS Globais**](/docs/global-css/): a forma tradicional de estilizar um _website_. Regras CSS são declaradas globalmente e os estilos são aplicados dependendo da especificidade e herança entre os elementos.
- [**Folhas de Estilo Modulares**](/docs/css-modules): regras CSS são escritas tradicionalmente (através de arquivos CSS), mas são consumidas por JavaScript e possuem escopo definido localmente para evitar efeitos colaterais indesejados em outros lugares. Funciona imediatamente com Gatsby.
- [**CSS-in-JS**](/docs/css-in-js/): CSS consumido e escrito com escopo local em JavaScript, possibilitando um uso mais fácil de estilização dinâmica e outras funcionalidades. Requer o uso de bibliotecas de terceiros.

Gatsby não possui uma opinião sobre qual abordagem de estilização escolher. Quase todas as opções possíveis são suportadas pelos _plugins_ oficiais e da comunidade. _(Se ainda não há um plugin para a sua opção favorita, considere [contribuir](/docs/creating-plugins) com um!)_

<GuideList slug={props.slug} />
