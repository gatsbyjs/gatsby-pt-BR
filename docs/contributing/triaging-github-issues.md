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

- uma questão que pode ser respondida imediatamente
- um relatório de um _bug_
- uma solicitação de uma _feature_
- ou uma discussão sobre um caso de uso complicado

No time principal, nós regularmente designamos alguém para ser um mantenedor de primeiro contato. Essa pessoa pode filtrar, triar, comunicar e gerenciar essa primeira linha de comunicação.

Mantenedores de primeiro contato tipicamente irão:

- lidar com perguntas que podem ser respondidas imediatamente
- testar e reproduzir relatórios de possíveis _bugs_ e rotulá-los apropriadamente
- comunicar solicitações de _features_ para o restante do time e garantir uma resposta válida
- possibilitar discussões sobre casos de uso complicados, seja entre os usuários ou através do time

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

O [fluxograma de resolução](https://whimsical.co/QvuMgo31T2C3xcWbou8xhy) fornece uma árvore de decisão a respeito de como as _issues_ devem ser categorizadas em um dos cinco tipos: _question ou discussion_, _bug report_, _feature request_, _documentation_, ou _maintenance_.

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
