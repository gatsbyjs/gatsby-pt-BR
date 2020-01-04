---
title: Aprimorando estilos com CSS-in-JS
overview: true
---

_CSS-in-JS_ se refere a uma abordagem onde os estilos são escritos no JavaScript ao invés de arquivos CSS externos, para manter facilmente os estilos no escopo dos componentes, eliminando código morto, encorajando um desempenho mais rápido e estilos dinâmicos, e mais.

O _CSS-in-JS_ preenche a lacuna entre o CSS e o JavaScript:

1. **Componentes**: você vai estilizar seu site com componentes, o que integra bem com a filosofia do React "tudo é um componente".
2. **Escopo**: este é uma consequência do primeiro. Assim como [Módulos CSS](/docs/css-modules/), o _CSS-in-JS_ possui seu escopo nos componentes por padrão.
3. **Dinâmico**: estilize seu site dinamicamente baseado no estado do componente integrando variáveis JavaScript.
4. **Bônus**: muitas bibliotecas _CSS-in-JS_ geram nomes únicos para classes o que pode ajudar no armazenamento de cache, na inserção automática de prefixos para os navegadores, no carregamento oportuno de CSS crítico, além de implementar diversas outras funcionalidades, dependendo da biblioteca que você escolher.

Enquanto o _CSS-in-JS_ não é necessário no Gatsby, ele é muito popular entre os desenvolvedores JavaScript pelas razões citadas acima. Para uma melhor contextualização, leia o artigo do Max Stoiber (criador da biblioteca de _CSS-in-JS_ [styled-components](/docs/styled-components/)) [_Porquê eu escrevo CSS no JavaScript_](https://mxstbr.com/thoughts/css-in-js/). Entretanto, você deve considerar se o _CSS-in-JS_ é necessário, pois não depender dele pode encorajar habilidades de front-end mais inclusivas. Também é mais difícil migrar estilos do JSX para o CSS e vice-versa.

_Note que esta funcionalidade não é parte do React ou do Gatsby, e requer o uso de alguma das muitas [bibliotecas CSS-in-JS_ de terceiros](https://github.com/MicheleBertoli/css-in-js#css-in-js)._

> Adicionar uma classe CSS estável na sua marcação JSX junto com seu _CSS-in-JS_ pode facilitar aos usuários incluir [Folhas de Estilo do Usuário](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para acessibilidade. Veja o exemplo do [Styled Components](/docs/styled-components#enabling-user-stylesheets-with-a-stable-class-name).

Tenha em mente que os estilos não são aplicados até que o JavaScript carregue, então um plugin para extrair os estilos é necessário para evitar momentos de conteúdo sem estilo (FOUC). Para atender a isto, toda biblioteca de _CSS-in-JS_ possui um plugin no Gatsby para o qual você precisa extrair os estilos e inserir no HTML durante a montagem e isto previne o FOUC. 

Esta seção contém guias para estilizar seu site com algumas das bibliotecas para _CSS-in-JS_ mais populares, incluindo como configurar estilos globais utilizando cada biblioteca.

<GuideList slug={props.slug} />
