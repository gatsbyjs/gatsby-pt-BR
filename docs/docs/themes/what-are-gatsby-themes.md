---
title: O Que São Temas Gatsby?
---

**Temas Gatsby** são plugins que incluem um arquivo `gatsby-config.js` e adicionam funcionalidades pré-configuradas, fonte de dados, e/ou código UI a sites Gatsby. Você pode pensar em temas Gatsby como sites Gatsby separados que podem ser colocados juntos, o que te permite dividir um projeto maior.

## Introdução

Para entender temas no Gastby, vamos percorrer a jornada que levou ao surgimento dessa funcionalidade.

Se você já criou um site Gatsby do zero, você sabe que há um número de decisões a serem tomadas. Por exemplo, criando um blog você precisa decidir onde seus dados estarão alocados, como é acessado, como é exibido e estilizado, etc.

## Gatsby Starters

Uma forma existente para se criar rapidamente sites Gatsby com funcionalidades similares é usar "[_Gatsby starters_](/docs/starters/)". _Starters_ são essencialmente sites Gatsby com funcionalidades pré-configuradas para um propósito específico. Você faz o download de um site Gatsby inteiro, pré-construído para um propósito específico (por exemplo, blogs, sites de portfólio, etc) e pode customizá-lo a partir disso.

Esses _starters_ tradicionais são um primeiro passo visando reduzir o nível de esforço envolvido na criação de um novo site Gatsby. No entanto, há dois principais problemas com _starters_ tradicionais:

- Sites criados a partir de starters tradicionais são basicamente “ejetados” desse _starter_ — Eles não mantém conexão com o _starter_ e começam a divergir imediatamente. Se o _starter_ for atualizado depois, não há uma forma fácil de puxar essas mudanças para um projeto existente.
- Se você criou múltiplos sites usando o mesmo _starter_, e depois quiser realizar as mesmas atualizações em todos eles, você teria que fazê-lo individualmente, site por site. 

## Temas Gatsby 

Temas Gatsby permitem que funcionalidades de sites Gatsby sejam “empacotados” em um produto autônomo para que outros (e você mesmo!) as reutilize facilmente. Usando um starter tradicional, todas as suas configurações padrão vivem diretamente no seu site. Usando um tema, todas as suas configurações padrão vivem em um pacote npm.

Temas resolvem os problemas geralmente enfrentados com starters tradicionais:

- Sites criados usando tema Gatsby podem adotar posteriores atualizações do tema — temas são pacotes versionados que podem ser atualizados como qualquer outro pacote.
- Você pode criar diversos sites que usam o mesmo tema. Para fazer atualizações por todos eles, você pode atualizar o tema central e enviar a nova versão nesses sites por meio de arquivos em `pacotes .JSON` (o que é melhor que gastar tempo tediosamente atualizando as funcionalidades de cada um deles).
- Temas são personalizáveis. Você poderia instalar um tema de blog junto de um tema de anotações, junto de um tema de e-commerce (e por aí vai).

> Um tema Gatsby é efetivamente uma configuração Gatsby customizável. O qual possibilita uma abordagem de maior nível ao lidar com Gatsby, extraindo partes complexas e repetitivas em pacotes reutilizáveis.

## Quando eu deveria usar ou construir um tema?

**Considere usar um tema se:**

- Você já tem um site Gatsby e não pode recomeçá-lo do zero a partir de um starter
- Você quer ser capaz de atualizar seu site com a última versão de determinada funcionalidade
- Você quer muitas funcionalidades em seu site, mas não há nenhum starter com todas elas — Você pode usar múltiplos temas, reunidos em um único site Gatsbsy

**Considere construir um tema se:**

- Você planeja reutilizar alguma funcionalidade similar entre vários sites Gatsby
- Você gostaria de compartilhar uma nova funcionalidade com a comunidade Gatsbsy 

## O que vem em seguida?

- [Usando um Tema Gatsby](/docs/themes/using-a-gatsby-theme)
- [Usando Múltiplos Temas Gatsby](/docs/themes/using-multiple-gatsby-themes)
- [Sombreando](/docs/themes/shadowing/)
- [Construindo Temas](/docs/themes/building-themes)
- [Convertendo um Starter](/docs/themes/converting-a-starter/)
- [Composição de Temas](/docs/themes/theme-composition/)
- [Convenções](/docs/themes/conventions/)

## Artigos relacionados

Para informações adicionais, confira artigos publicados durante o desenvolvimento de temas:

- [Why Themes?](/blog/2019-01-31-why-themes/)
- [Themes Roadmap](/blog/2019-03-11-gatsby-themes-roadmap/)
- [Getting Started with Gatsby Themes and MDX](/blog/2019-02-26-getting-started-with-gatsby-themes/)
- [Watch Us Build a Theme Live](/blog/2019-02-11-gatsby-themes-livestream-and-example/)
- [Introducing Gatsby Themes by Chris Biscardi at Gatsby Days](https://www.gatsbyjs.com/gatsby-days-themes-chris/)
- [See all blog posts on themes](/blog/tags/themes)
