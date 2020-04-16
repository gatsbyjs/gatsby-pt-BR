---
title: Criando Bibliotecas de Componentes
---

Bibliotecas de componentes são frequentemente utilizadas em sistemas de interface baseados em componentes como React e Vue. Elas são normalmente versionadas em repositórios de componentes.

IBM's [Carbon Design System](https://www.carbondesignsystem.com/) e Palantir's [Blueprint](https://blueprintjs.com/) são ambos bons exemplos.

## Por que bibliotecas de componentes

Existem vários fundamentos para a criação de bibliotecas de componentes.

- **Criando um design unificado**. Em grandes propriedades da web e aplicativos web, a aparência e sentimento podem divergir através de diferentes seções mantidas por diferentes times. Bibliotecas de componentes são frequentemente usadas para implementar um [sistema de design](https://www.designsystems.com/).
- **Evite reinventar a roda**. Bibliotecas de componentes incluem elementos comuns, como carousels ou dropdowns, para evitar a necessidade de equipes individuais reimplementarem estes componentes.

## Ferramentas e configurações de equipe

Bibliotecas de componentes são geralmente mantidos por um indivíduo ou uma equipe de design que atua como curador; quando uma equipe de website ou um time de recursos precisa de um componente, ele normalmente está disponivel para uso, para que eles possam avançar rapidamente.

Bibliotecas de componentes são geralmente armazenadas em um repositório separado. Aplicativos individuais ou websites especificam em suas dependências (dentro do `package.json`) qual versão de cada componente eles estão usando.

Uma desvantagem de usar bibliotecas de componentes é a complexidade adicional das dependências entre repositórios.

Por exemplo, se um desenvolvedor de recursos precisar alterar uma biblioteca de componentes, o fluxo de trabalho do desenvolvedor normalmente envolve dois pull requests; um para o repositório do compenente que foi feito alterações, e um para o repositório do site para aumentar a versão do componente.

## Diferentes abordagens de versionamento

Existem duas diferentes abordagens para o versionamento de bibliotecas de componentes.

A primeira é para a versão global na biblioteca de componentes. Para cada commit dado, a biblioteca tem um número de versão (e.g. `30.3.1`). Qualquer commit atualizando o componente irá então adicionar o número de versão de acordo. Ambos, Carbon Design System e Blueprint adotam essa abordagem.

A segunda abordagem é para a versão de cada componente na biblioteca de componentes. Isto era usado, por exemplo, [pelo Walmart.com](https://medium.com/walmartlabs/how-to-achieve-reusability-with-react-components-81edeb7fb0e0) -- eles construiram sua biblioteca de componentes com React componentes, criando cada componente separado, versionado por pacotes npm.

Esta abordagem permite mais granularidade -- _e se você desejar de uma versão mais antiga de um componente, mas uma versão mais recente de outro?_ -- mas requer ferramentas adicionais para fazer os fluxos de trabalho mais agradáveis.
