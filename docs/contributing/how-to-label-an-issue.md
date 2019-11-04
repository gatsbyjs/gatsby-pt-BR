---
title: Como classificar uma issue
---

## O que são classificadores de issues?

Classificadores de issues é uma ferramenta no GitHub usada para agrupar issues em uma ou mais categorias.

[Veja as labels do Gatsby e suas definições](https://github.com/gatsbyjs/gatsby/issues/labels)

## Por que classificar issues?

Gatsby é um projeto bem ativo e diariamente tem novas issues abertas. Classificar as issues ajuda a identificar:

- boas issues para novos contribuidores trabalharem
- bugs reportados e confirmados
- solicitar novas features
- issues duplicadas
- issues que estão paradas ou bloqueadas

## Quem pode classificar as issues?

Qualquer um que seja membro do [Time de Mantenedores do Gatsby](https://github.com/orgs/gatsbyjs/teams/maintainers) pode classificar as issues.

Você pode receber um convite do time quando seu Pull Request for _mergeado_ no projeto do Gatsby. Veja a lista de [`help wanted (precisa de ajuda)`](https://github.com/gatsbyjs/gatsby/labels/%F0%9F%93%8D%20status%3A%20help%20wanted) das issues e o [O Guia de Como Contribuir](/contributing/how-to-contribute/) para começar.

**NOTA:** Se você já teve um pull resquest _mergeado_ e _não_ foi convidado pelo time de mantenedores, por favor vá para [o dashboard](https://store.gatsbyjs.org/) e solicite um código de desconto. Você deve receber um convite do time - _e pegue de graça seu Gatsby swag!_ Se não funcionar, por favor envie um email para team@gatsbyjs.com e nós conseguiremos um convite para você.

## Como classificar uma issue

Idealmente, toda issue deve ter uma classificação `tipo:` de classificador aplicado a ela. Opcionalmente uma classificação `status:` ou mais classificações, também podem ser aplicadas.

Antes de continuar, familiarize-se com as [labels do Gatsby e suas definições](https://github.com/gatsbyjs/gatsby/issues/labels)

As etapas principais para classificar uma issue são:

- Leia a issue
- Escolha as labels que aplicam para aquela issue
- E é isso - sente e relaxe, e talvez curta por um momento a satisfação de ter feito um bom trabalho.

O resto deste documento vai descrever como escolher as labels corretas para uma issue.

### Encontre uma issue que você esteja interessado

Comece com a [lista de issues do Gatsby](https://github.com/gatsbyjs/gatsby/issues) e procure até você encontrar uma nova issue que chame a sua atenção. Alternativamente, você pode ver a [lista de issues não classificadas](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aopen+is%3Aissue+no%3Alabel).

### Leia a issue

Leia a issue e quaisquer comentários para entender do que ela se trata.

### Escolha uma label `tipo:`

Escolha uma classificação de tipo do dropdown de _labels_ que estará do lado direito da issue.

![GitHub label dropdown](./images/github-label-list.png)

Você também pode checar as [descrições das labels](https://github.com/gatsbyjs/gatsby/issues/labels) para entender melhor cada uma.

O tipo mais comum de issue é `tipo: questão ou discussão`, normalmente você pode aplicá-los à issues que são _open-ended_ ou não tem uma próxima etapa clara.

É OK mudar o tipo de issue assim que mais informações fiquem disponíveis. O que começa como `tipo: questão ou discussão`, pode mais tarde mudar para `tipo: bug`.

Mudar as labels é rápido e facilmente reversível, então não se preocupe em aplicar uma label "errada".

Escolha a _label_ `tipo:` apropriada e siga para o próximo passo.

### Escolha uma _label_ `status:` (opcional)

Veja sobre [`status:` labels (e suas descrições)](https://github.com/gatsbyjs/gatsby/issues/labels), e se nenhuma delas se aplicar à issue, adicione um novo se necessário.

Exemplos de aplicação da _label_ `status:` podem ser:

- Uma _issue_ que dependa de uma mudança em uma dependência externa, poderia classificada como `status: blocked`

- Uma issue com uma descrição clara de como ser resolvida poderia ser classificada como `status: help wanted`.

- Uma issue faltando informações necessárias para ajudar o autor da issue a resolvê-la, poderia ser classificada como `status: needs more info`

- Uma issue descrevendo um bug, sem passos claros de como reproduzí-lo, poderia ser classificada como : `status: needs reproduction`

- Uma issue descrevendo um bug com as etapas para reproduzí-lo _e_ você rodou o código localmente e viu o erro, poderia ser classificada como `status: confirmed`

### Escolha quaisquer outros classificadores

Existem outros tipos de classificadores que podem às vezes ser aplicados à uma issue. Aqui estão alguns exemplos de quando usá-los:

- `good first issue` pode ser usada quando uma issue é pequena, e a sua resolução pode ser feita por alguém que não tenha um conhecimento profundo de Gatsby e como ele funciona. Essas issues são particularmente adequadas para pessoas que estão fazendo suas primeiras contribuições _open-source_.

- `stale` pode ser usado em uma _issue_ onde o autor não respondeu às solicitações de mais informações nos últimos 20 dias.

### Terminar

E é isso, você acabou! Você pode terminar o seu dia ou voltar para a primeira etapa, para classificar outra issue.

## Conclusão

Classificar issues é uma ótima maneira de ajudar no projeto do Gatsby independente do seu nível de experiência.
