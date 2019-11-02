---
title: Enviar para Biblioteca Starter
---

Você criou um Gatsby _starter_ que gostaria de adicionar na [Biblioteca _Starter_](/starters/)? Siga estas instruções.

## Etapas

Para adicionar seu site à biblioteca _starter_, siga as duas etapas abaixo.

1. Se esta é sua primeira contribuição ao repositório _open source_ do Gatsby, siga as [Orientações de contribuição](/contributing/code-contributions/).

2. Edite o arquivo [`starters.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/starters.yml) adicionando suas informações _starter_ no final da lista no seguinte formato:

```yaml:title=docs/starters.yml
- url: Link para uma demonstração de seu starter
  repo: Link para o repositório do GitHub
  description: Sua descrição do starter

  # Estes correspondem aos filtros na biblioteca
  # Veja docs/categories.yml tags válidas.
  tags:
    - Redux

  # Adicione funcionalidades ao seu site
  # Elas serão incluídas na página de detalhes do seu starter.
  features:
    - Lista de postagens do blog com visualizações (imagem + resumo) de cada postagem do blog
```

Use o seguinte modelo para garantir que os campos obrigatórios sejam preenchidos:

```yaml:title=docs/starters.yml
- url: (obrigatório)
  repo: (obrigatório - https://github.com/{usuario}/{titulodosite})
  description: (opcional)
  tags:
    - (obrigatório)
  features:
    - (obrigatório)
```

Confira o arquivo [`starters.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/starters.yml) para exemplos.

Preferimos solicitações pull com o título no seguinte formato:
`chore (iniciantes): adicione meu nome de iniciante-aqui`
Se houver problemas com o seu PR, você poderá corrigi-los executando o `npm run format`.

Preferimos pull requests com o título no seguinte formato:
`chore(starters): adicionar nome-do-meu-starter-aqui`
Se houver problemas com o seu PR, você poderá corrigi-los executando o `npm run format`.

### Precisa alterar detalhes?

Se você deseja editar qualquer coisa no envio do seu site posteriormente, basta editar o arquivo .yml enviando outro PR. Os dados do GitHub (como estrelas) serão automaticamente puxados e atualizados, mas sua descrição, tags e lista de funcionalidades são de sua responsabilidade!

### Adicionando nova tag

Se você acha que algo está faltando na lista de tags, atualize o [`categories.yml`](https://github.com/gatsbyjs/gatsby/blob/master/docs/categories.yml) e adicione um novo. No entanto, recomendamos que você use tags existentes.
