---
title: Triagem de Issues do GitHub
---

## Qual o objetivo desse documento?

No time principal do Gatsby, nós encontramos padrões que nos ajudam efetivamente a realizar triagem das _issues_ recebidas no GitHub, responder aos questionamentos da comunidade, identificar _bugs_, e proporcionar oportunidades de contribuição. A triagem de _issues_ é uma ótima forma de contribuir com a comunidade Gatsby e compartilhar seu conhecimento, sem necessariamente conhecer a fundo como a base de código do Gatsby funciona.

Queremos compartilhar esse padrões com toda a comunidade, de modo que, se você tem interesse em nos ajudar na triagem, que possa fazê-la da forma mais eficiente possível!

Nesse documento, iremos responder perguntas frequentes, listar orientações e ilustrar uma árvore de decisão.

## Suporte ao primeiro contato

Para o Gatsby, a primeira linha de comunicação entre um usuário e o time são as _issues_ no GitHub. Tipicamente, todo dia são abertas 20-30 _issues_ -- isso significa que recebemos uma a cada hora!

Uma _issue_ aberta poderia ser:

<<<<<<< HEAD:docs/contributing/triaging-github-issues.md
- uma questão que pode ser respondida imediatamente
- um relatório de um _bug_
- uma solicitação de uma _feature_
- ou uma discussão sobre um caso de uso complicado
=======
- [a question that can be answered immediately](#questions-with-immediate-answers)
- a bug report
- a request for a feature
- or a discussion on a complicated use case
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f:docs/contributing/triaging-github-issues/index.md

No time principal, nós regularmente designamos alguém para ser um mantenedor de primeiro contato. Essa pessoa pode filtrar, triar, comunicar e gerenciar essa primeira linha de comunicação.

Mantenedores de primeiro contato tipicamente irão:

<<<<<<< HEAD:docs/contributing/triaging-github-issues.md
- lidar com perguntas que podem ser respondidas imediatamente
- testar e reproduzir relatórios de possíveis _bugs_ e rotulá-los apropriadamente
- comunicar solicitações de _features_ para o restante do time e garantir uma resposta válida
- possibilitar discussões sobre casos de uso complicados, seja entre os usuários ou através do time
=======
- [answer questions by pointing to documentation](#questions-with-immediate-answers)
- test and reproduce possible bug reports and label them appropriately
- communicate feature requests to the rest of the team and ensure a valid response
- enable discussions on complicated use cases, whether themselves or via the rest of team
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f:docs/contributing/triaging-github-issues/index.md

## Por que damos suporte ao primeiro contato?

Fazemos isto porque:

- As perguntas são respondidas rápida e corretamente, deixando os usuários felizes
- Os relatórios de _bug_ são reproduzidos e os dados mais relevantes são coletados antes que alguém apresente uma solução
- _Issues_ não relacionadas são resolvidas imediatamente, de modo que não gastamos muito tempo com elas

## O que o Gatsby tem de único?

Gatsby é único entre a maioria do projetos _open source_ porque:

- Gatsby se integra a muitas ferramentas de terceiros (WordPress, Drupal, Contentful etc) através de _plugins_ e, consequentemente, o escopo típico das _issues_ aumenta de modo significativo
- Gatsby visa ser realmente amigável para os iniciantes (queremos ser a nova forma de iniciar no desenvolvimento web) e isso significa que precisamos acomodar uma ampla gama de níveis de habilidades
- No Gatsby, nós definimos um conjunto de métricas que usamos para garantir que estamos sendo responsivos e úteis à nossa comunidade _open source_

## Como fazemos o suporte ao primeiro contato?

### Orientações gerais

- **Seja empático.** O autor de uma _issue_ pode estar perguntando algo que é óbvio para você, mas isso não significa que seja óbvio para ele - é importante enxergar a _issue_ sob o ponto de vista do autor. As pessoas frequentemente lembram-se de como você as fez sentir, e não do que você as disse.
- **Contextualize.** Ao responder uma _issue_, pode ser útil anexar _links_ para documentação, _issues_ ou PR's existentes, ou fornecer um contexto relacionado. Assim, a _issue_ pode servir como referência para leitores futuros.
- **Incentive contribuições da comunidade.** Envolver as pessoas causa um impacto enorme. Muitas vezes, vale mais a pena dedicar seu tempo para escrever uma _task_ `good first issue` do que propriamente resolvê-la. Isso pode proporcionar uma maneira menos desgastante de alguém se envolver mais no _open source_!
- **Dê tempo para os autores fecharem suas _issues_.** Às vezes, pode parecer que uma _issue_ está resolvida, no entanto, o autor pode ter questionamentos a serem feitos. Geralmente, é melhor dar a ele um ou dois dias para fechar a _issue_.

### Etiquetas

As etiquetas além de ajudarem a agrupar _issues_ em conjuntos gerenciáveis, melhoram as capacidades de pesquisa e identificação. Nós temos um conjunto de etiquetas que usamos para agrupar as _issues_ de acordo com seus tipos e _status_. Embora queiramos limitar o número de etiquetas, sinta-se à vontade para adicionar alguma se parecer relevante e for ajudar no agrupamento!

É legal atualizar as etiquetas à medida que o estado ou tipo da _issue_ é alterado, por exemplo, se uma pergunta se torna uma solicitação de _feature_. Isso significa que as etiquetas são de natureza transitória e são sujeitas a serem atualizadas de acordo com o progresso da _issue_.

Confira os [documentos sobre rotulagem](/contributing/how-to-label-an-issue/) para mais informações.

### Fluxograma de resolução

<<<<<<< HEAD:docs/contributing/triaging-github-issues.md
O [fluxograma de resolução](https://whimsical.co/QvuMgo31T2C3xcWbou8xhy) fornece uma árvore de decisão a respeito de como as _issues_ devem ser categorizadas em um dos cinco tipos: _question ou discussion_, _bug report_, _feature request_, _documentation_, ou _maintenance_.
=======
Issues are categorized into one of five types: question or discussion, bug report, feature request, documentation, or maintenance.

#### Questions with immediate answers

- Point to existing documentation to answer the question
- If insufficient, do the following:
  1. Provide an answer
  2. Label the issue with documentation
  3. Keep it open until a PR has added the answer to the documentation, and the issue includes a link to said documentation

If an issue comes in as a question with a known answer it can be tempting to answer it and close the issue. However, the consequence of this approach is that the answer to a question others may have is now buried in a closed issue and may be hard to surface. The preferred solution is to get that answer documented in the main Gatsby documentation and connect the issue to an answer by including a docs link.

#### Bug Report

Bug Reports are issues that identify functionality in Gatsby that should work but does not in a given scenario. If an issue is a Bug Report, it should include steps to reproduce the problem. If it doesn't, ask the issue filer for those steps and label the issue with `needs reproduction`.

Attempt to reproduce the bug using the steps given. If that's not possible, ask for more information and label the issue as `needs more info`.

If the reproduction is successful, label the issue with `confirmed` and determine who is best suited to implement a fix. If it's approachable for the community, consider the `help wanted` or `good first issue` labels. Otherwise, label with `inkteam to review` so it can be picked up by a Gatsby team member.

![Flow chart for handling a Bug Report](./BugFlow.png)

#### Feature Request

Feature Requests are issues that request support for additional functionality not currently covered in the existing codebase. The first step in triaging a feature request is to determine if it's a reasonable request; this is a challenge and if you don't feel comfortable making this determination please label with `inkteam to review`. If it's clear that this isn't a feature it makes sense for Gatsby to implement, provide a comment explaining the decision making and close the issue. Review the [saved replies](#saved-replies) to see if there is an appropriate response already available.

If it's determined to be a worthwhile feature, the next decision point is whether the feature should be added to core or upstream. Upstream issues are those that are outside of Gatsby's control and caused by dependencies. Upstream features should be labeled with `upstream` and include comments about the scope.

If it's a core change, is it a breaking change? Breaking changes should be labeled with `breaking change` and typically closed. Note that they may sometimes be left open with the note that the functionality can only be added in a major release.

Non-breaking changes can be labeled as `help wanted` and it is often best to ask the creator of the issue if they'd be interested in helping develop the PR.
![Flow chart for handling a Feature Request](./FeatureFlow.png)

#### Documentation

Issues can be filed requesting documentation on a particular topic. Sometimes the documentation already exists, so you can link to it and close the issue.

Alternatively, the issue may be something the team is unable to address. Consider using a [saved reply](#saved-replies) in that circumstance.

Otherwise, label the issue with `documentation` and ask the issuer filer if they'd like to help with a PR.
![Flow chart for handling a Documentation Request](./DocumentationFlow.png)

#### Maintenance

Maintenance issues are things like bumping a package version. These issues should be labeled with `maintenance`.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f:docs/contributing/triaging-github-issues/index.md

### Respostas salvas

Os membros do time Gatsby salvaram certas [respostas comuns de formulário](https://github.com/orgs/gatsbyjs/teams/admin/discussions/3) para acelerar a triagem das _issues_.

## _Bot_

Temos um _bot_ que nos ajuda a automatizar algumas coisas:

- _Issues_ com interrogação em seus títulos ou que começam com _"how"_ ("como") são automaticamente etiquetadas como perguntas (`question`)
- _Issues_ com um corpo vazio são fechadas
- _Issues_ inativas são marcadas como obsoletas depois de 20 dias. Após mais 10 dias elas são então fechadas, a menos que existam comentários adicionais ou estejam com a etiqueta `not stale` ("não obsoleta").

## Perguntas frequentes

> Quando devo fazer uma demo para uma _issue_?

Quando uma _feature_ ou padrão não está documentado, pode ser legal criar uma demo para dar mais clareza ao autor bem como ajudar leitores futuros.

> Como reproduzo um _bug_?

Todo relatório de _bug_ deve fornecer detalhes sobre como reproduzí-lo. Isso é tão importante que há uma [documentação dedicada sobre como criar um bom guia de reprodução de um _bug_](/contributing/how-to-make-a-reproducible-test-case/). Incentive os autores das _issues_ a descreverem exatamente como reproduzir um _bug_.

> Quanto tempo devo gastar em uma _issue_?

Algumas _issues_ demandam mais tempo que outras e não há nenhuma regra rígida sobre isso. Entretanto, é melhor dedicar tempo para _issues_ depois que informações relevantes e o guia para reprodução são disponibilizados.

> Eu tenho que olhar o Discord?

Você não precisa. Alguns de nós são ativos no Discord, e você pode ser também, se desejar.

> Uso a mesma _issue_ para rastrear adições na documentação ou abro uma nova?

Se a _issue_ descreve o contexto bem o suficiente, então não há problema em atualizar seu título e utilizá-la para rastrear adições na documentação.

> Quando devo acompanhar uma _issue_?

Se o autor não responder a um comentário por uma ou duas semanas, pode ser legal acompanhá-la e perguntar se há algo em que possamos ajudar. Se a _issue_ se tornar obsoleta após isso, nosso _bot_ poderá limpá-la.

> O que faço se uma _issue_ é relacionada a algo no _upstream_?

É uma boa prática abrir uma _issue_ no repositório _upstream_ em casos como esse, mas não é estritamente necessário. _Upstream_ nesse caso refere-se a repositórios que hospedam dependências para o Gatsby.
