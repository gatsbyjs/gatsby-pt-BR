---
title: Submit to Site Showcase
---

Quer enviar um site para o [Site Showcase](/showcase/)? Siga estas instruções.

## Passos

São basicamente 3 passos:

1. Se esse é sua primeira contribuição para o repositório open source do Gatsby, siga as [Instruções de contribuição](/contributing/code-contributions/).

2. Se existe a possíbilidade de alguém já ter submetido o site, certifique-se que ninguém tenha submetido procurando nos PRs existentes: https://github.com/gatsbyjs/gatsby/pulls

3. Edite o arquivo [`sites.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/sites.yml) e adicione sua submissão no final da lista dos sites seguindo o seguinte formato:

```yaml:title=docs/sites.yml
- title: Title of the Site

  # esta URL que é vinculada no showcase
  main_url: https://titleofthesite.com

  # esta URL é utilizada para gerar a captura da tela
  url: https://titleofthesite.com/portfolio

  # opcional: para sites open-source, esta URL aponta pra o repositório que contém o site
  source_url: https://github.com/{username}/{titleofthesite}

  # opcional: um parágrafo curto descrevendo o conteúdo e/ou propósito do site que irá aparecer no modal de visualização de detalhes e permalink para seu site
  description: >
    {titleofthesite} is a shiny new website built with Gatsby v2 that makes important contributions towards a faster web for everyone.

  # Você pode listar quantas categorias você quiser. Verifique a lista de categorias abaixo nessa documentação!
  # Se você gostaria de criar uma nova categoria, simplesmente liste aqui.
  categories:
    - Relevant category 1
    - Relevant category 2

  # Adicione o nome (desenvolvedor ou empresa) e URL (por exemplo, Twitter, GitHub, portfólio) para ser usada para atribuição
  built_by: Jane Q. Developer
  built_by_url: https://example.org

  # deixe como falso, o time de revisão do Gatsby irá escolher os sites em destaque trimestralmente
  featured: false
```

Use o seguinte templete para garantir que os campos obrigatórios estão preenchidos:

```yaml:title=docs/sites.yml
- title: (obrigatório)
  url: (obrigatório)
  main_url: (obrigatório)
  source_url: (opcional - https://github.com/{username}/{titleofthesite})
  description: >
    (opcional)
  categories:
    - (obrigatório)
  built_by: (opcional)
  built_by_url: (opcional)
  featured: false
```

## Informações úteis

### Categorias


Atualmente, categorias incluem dois _tipos de site_ (estrutura) e o _conteúdo do site_. Por ora, você deverá colocar todas em "categorias" na sua submissão. As razões pelas quais esses dois estão em listas separadas é para mostrar que você pode ter um site para marketing de uma escola (tipo do site seria marketing, e conteúdo seria educação) ou um site que entrega ensino de marketing online (tipo de site seria educação e conteúdo seria marketing).


#### Tipo de site

- Blog
- Directory
- Documentation
- eCommerce
- Education
- Portfolio
- Gallery
- Confira [`categories.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/categories.yml) para uma lista atualizada de categorias válidas.

#### Conteúdo do site

Algumas notas sobre o conteúdo do site: uma pergunta que é comum: "todos os sites Gatsby não estão tecnicamente na categoria "_web development_"? Bem, não, por que esta categoria significa que o _conteúdo_ do site deveria ser sobre desenvolvimento web, como [ReactJS](https://reactjs.org/). Ainda, a diferença entre tecnologia e desenvolvimento web é como isto. [Cardiogram](https://cardiogr.am/) é uma tecnologia, enquanto [ReactJS](https://reactjs.org/) é desenvolvimento web.

- Agency
- Education
- Entertainment
- Finance
- Food
- Healthcare
- Government
- Marketing
- Music
- Media
- Nonprofit
- Open Source
- Photography
- Podcast
- Real Estate
- Science
- Technology
- Web Development
- Veja [`categories.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/categories.yml) para uma lista atualizada de categorias válidas.

#### Adicionando uma nova tag

Caso você ache que há alguma _tag_ faltando na lista, você pode atualizar o arquivo [`categories.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/categories.yml) e adicionar uma tag nova. No entanto, encorajamos que utilize as _tags_ existentes.

### Notas sobre sites em destaque

#### Processo de Revisão

Por padrão, todos os sites que são enviados ao _showcase_ de sites serão revisados pelo comitê revisor de sites do Gatsby como um candidato para a seção de "Sites em Destaque" do _showcase_. Se você não quer que seu site seja destacado, adicione 'DO NOT FEATURE' no _pull request_.

Sites em destaque serão escolhidos trimestralmente baseados nos seguintes critérios:


- Marcas bem conhecidas
- Diversidade de casos de uso
- Apelo visual
- Diversidade visual

#### Quantos podem ser destacados ao mesmo tempo?

9, por que essa é a quantidade que cabe na pagina de _showcase_ do site.

#### Como definir um site como destacado

_Nota: O time do Gatsby irá escolher sites em destaque, deixe como `featured: false` na primeira submissão_

Se seu site for escolhido como destaque, você precisará fazer isso:

1.  Altere `featured: false` para `featured: true`

2.  Adicione `featured` como categoria.

```shell
categories:
  - featured
```

### Precisa alterar sua submissão?

Caso, queira editar qualquer coisa na submissão do seu site posteriormente, simplesmente edite o arquivo `.yml` submetendo outro PR.
