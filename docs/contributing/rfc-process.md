---
title: Processo RFC
---

<!-- ---
title: Processo RFC
--- -->

## O que é o processo RFC?

Muitas mudanças, incluindo correções de bugs e melhorias na documentação, podem ser implementadas e revistas através do fluxo de trabalho normal do _pull request_ do GitHub.

<!-- Many changes, including bug fixes and documentation improvements can be
implemented and reviewed via the normal GitHub pull request workflow. -->

Algumas mudanças, no entanto, são "substancias", e por esse motivo, solicitamos que sejam submetidas a um processo de _design_, de modo a produzir um consenso entre os participantes da equipe principal do Gatsby.

<!-- Some changes, however, are "substantial", and we ask that these be put through
a bit of a design process and produce a consensus among the Gatsby core team. -->

O processo "RFC" (em português, "solicitação de comentários") visa fornecer um caminho consistente e controlado para que novos recursos sejam inseridos no projeto.

 <!-- 
The "RFC" (request for comments) process is intended to provide a consistent and controlled path for new features to enter the project. -->

[Lista RFC Ativa](https://github.com/gatsbyjs/rfcs/pulls)

<!-- [Active RFC List](https://github.com/gatsbyjs/rfcs/pulls) -->

Gatsby ainda está **desenvolvendo ativamente** esse processo, e ainda o mudará à medida que mais recursos forem implementados e a comunidade optar por abordagens específicas para o desenvolvimento de recursos.

<!-- Gatsby is still **actively developing** this process, and it will still change as more features are implemented and the community settles on specific approaches to feature development.  -->

## Quando seguir esse processo

<!-- ## When to follow this process -->

Você deve considerar usar esse processo se pretende fazer alterações "substanciais" no Gatsby ou em sua documentação. Alguns exemplos que se beneficiariam de uma RFC são:

<!-- You should consider using this process if you intend to make "substantial" changes to Gatsby or its documentation. Some examples that would benefit from an RFC are: -->

- Um novo recurso que cria uma nova área de superfície na API e requer um sinalizador de recurso se introduzido.

<!-- - A new feature that creates new API surface area, and would require a feature flag if introduced. -->

- A remoção de recursos que já foram disponibilizados como parte do canal de lançamento.

  <!-- - The removal of features that already shipped as part of the release channel. -->

- A introdução de novos usos ou convenções idiomáticas, mesmo que não incluam alterações de código no próprio Gatsby.
  <!-- - The introduction of new idiomatic usage or conventions, even if they do not include code changes to Gatsby itself. -->

O processo RFC é uma ótima oportunidade para atrair mais atenção da sua proposta antes de se tornar parte de uma versão lançada do Gatsby. Muitas vezes, até propostas que parecem "óbvias" podem ser significativamente melhoradas quando um grupo maior de pessoas interessadas tiver a chance de avaliá-las.

<!-- The RFC process is a great opportunity to get more eyeballs on your proposal
before it becomes a part of a released version of Gatsby. Quite often, even
proposals that seem "obvious" can be significantly improved once a wider group of interested people have a chance to weigh in. -->

O processo RFC também pode ser útil para incentivar discussões sobre um recurso proposto enquanto ele está sendo projetado e incorporar restrições importantes ao design enquanto é mais fácil alterá-lo, antes da sua completa implementação.

<!--
The RFC process can also be helpful to encourage discussions about a proposed feature as it is being designed, and incorporate important constraints into the design while it's easier to change, before the design has been fully implemented. -->

Algumas alterações não requerem um RFC:

<!-- Some changes do not require an RFC: -->

- Reformular, reorganizar ou refatorar a adição ou remoção de avisos
  <!-- - Rephrasing, reorganizing or refactoring addition or removal of warnings -->
- Modificações que melhoram estritamente os critérios de qualidade numéricos e objetivos (aceleração, melhor suporte ao navegador)

  <!-- - Additions that strictly improve objective, numerical quality
    criteria (speedup, better browser support) -->

- Modificações que provavelmente só serão _notadas_ por outros implementadores de Gatsby, e invisíveis para os usuários.
  <!-- - Additions only likely to be _noticed by_ other implementors-of-Gatsby,
    invisible to users-of-Gatsby. -->

## Qual é o processo

<!-- ## What the process is -->

Em resumo, para adicionar um recurso importante ao Gatsby, geralmente é possível fazer o _merge_ da RFC ao repositório RFC como um arquivo _markdown_. Nesse ponto, a RFC está 'ativa' e pode ser implementada com o objetivo de eventual inclusão no Gatsby.

<!-- In short, to get a major feature added to Gatsby, one usually first gets the RFC merged into the RFC repo as a markdown file. At that point the RFC is 'active' and may be implemented with the goal of eventual inclusion into Gatsby. -->

- Faça o _fork_ do repositório RFC https://github.com/gatsbyjs/rfcs. Copie `0000-template.md` para

<!-- - Fork the RFC repo https://github.com/gatsbyjs/rfcs Copy `0000-template.md` to  -->

- `text / 0000-my-feature.md` (em que 'my-feature' é descritivo. Não atribua um número ao RFC ainda).

  <!-- - `text/0000-my-feature.md` (where 'my-feature' is descriptive. Don't assign an RFC number yet). -->

- Preencha o RFC. Tenha cuidado com os detalhes: ** RFCs que não   apresentar motivação convincente, demonstrar uma compreensão do impacto do design ou ser dissimulados sobre os inconvenientes ou as alternativas tendem a ser mal recebidas **.

  <!-- - Fill in the RFC. Put care into the details: **RFCs that do not
    present convincing motivation, demonstrate understanding of the impact of the design, or are disingenuous about the drawbacks or alternatives tend to be poorly-received**. -->

- Envie um _pull request_. Como _pull request_, o RFC receberá um feedback de design da comunidade, e o autor deve estar preparado para revisá-lo em resposta.

  <!-- - Submit a pull request. As a pull request the RFC will receive design feedback from the larger community, and the author should be prepared to revise it in response. -->

- Crie consenso e integre feedback. As RFCs que têm amplo suporte têm muito mais probabilidade de progredir do que aquelas que não recebem comentários.

<!-- - Build consensus and integrate feedback. RFCs that have broad support are much more likely to make progress than those that don't receive any comments. -->

- Eventualmente, a equipe decidirá se o RFC é um candidato   para inclusão ao Gatsby.

  <!-- - Eventually, the team will decide whether the RFC is a candidate for inclusion in Gatsby. -->

- As RFCs candidatas à inclusão no Gatsby entrarão em um "período final para comentários" com duração de três dias. O início deste período será sinalizado com um comentário e uma tag na solicitação de recebimento de RFCs.

<!-- - RFCs that are candidates for inclusion in Gatsby will enter a "final comment period" lasting 3 calendar days. The beginning of this period will be signaled with a comment and tag on the RFCs pull request. -->

- Uma RFC pode ser modificada com base no feedback da equipe e da comunidade. Modificações significativas podem desencadear um novo período final para comentários.

<!-- - An RFC can be modified based upon feedback from the team and community. Significant modifications may trigger a new final comment period. -->

- Uma RFC pode ser rejeitada pela equipe após a discussão pública ter sido resolvida e comentários foram feitos resumindo a justificativa da rejeição. Um membro da equipe deve fechar a _pull request_ associada aos RFCs.

<!-- - An RFC may be rejected by the team after public discussion has settled and comments have been made summarizing the rationale for rejection. A member of the team should then close the RFCs associated pull request. -->

- Uma RFC pode ser aceita no final do seu período final de comentários. Um membro da equipe fará o _merge_ do _pull request_ associada às RFCs, quando, então, se tornará 'ativo'.

<!-- - An RFC may be accepted at the close of its final comment period. A team member will merge the RFCs associated pull request, at which point the RFC will become 'active'. -->

## O ciclo de vida da RFC

<!-- ## The RFC life-cycle -->

Depois que uma RFC se torna ativa, os autores podem implementá-la e submeter o recurso como um _pull request_ ao repositório Gatsby. Tornar-se "ativo" não corresponde a uma "aprovação automática" e, em particular, ainda não significa que o recurso será posto em produção; isso indica apenas que, a princípio, há concordância com equipe principal, e que o _merge_ é factível.

<!-- Once an RFC becomes active, then authors may implement it and submit the feature as a pull request to the Gatsby repo. Becoming 'active' is not a rubber stamp, and in particular still does not mean the feature will ultimately be merged; it does mean that the core team has agreed to it in principle and are amenable to merging it. -->

Além disso, o fato de uma determinada RFC ter sido aceita e está 'ativa' não implica nada sobre qual prioridade é atribuída à sua implementação, nem se alguém está atualmente trabalhando nela.

<!-- Furthermore, the fact that a given RFC has been accepted and is 'active' implies nothing about what priority is assigned to its implementation, nor whether anybody is currently working on it. -->

<!-- Modificações nas RFCs ativas podem ser feitas nos PRs seguintes. Nós nos esforçamos para escrever cada RFC de uma maneira que reflita o design final do recurso; mas a natureza do processo significa que não podemos esperar que todas as RFCs mescladas reflitam realmente qual será o resultado final no momento do próximo grande lançamento; portanto, tentamos manter cada documento RFC um pouco sincronizado com o recurso de idioma conforme planejado, rastreando essas alterações por meio de solicitações de recebimento de solicitação ao documento. -->

Modifications to active RFCs can be done in followup PRs. We strive to write each RFC in a manner that it will reflect the final design of the feature; but the nature of the process means that we cannot expect every merged RFC to actually reflect what the end result will be at the time of the next major release; therefore we try to keep each RFC document somewhat in sync with the language feature as planned, tracking such changes via followup pull requests to the document.

## Implementando uma RFC

<!-- ## Implementing an RFC -->

O autor de uma RFC não é obrigado a implementá-la. Obviamente, o autor da RFC (como qualquer outro desenvolvedor) pode publicar uma implementação para revisão após a aceitação da RFC.

<!-- The author of an RFC is not obligated to implement it. Of course, the RFC author (like any other developer) is welcome to post an implementation for review after the RFC has been accepted. -->

Se você estiver interessado em trabalhar na implementação de uma RFC 'ativa', mas não puder determinar se alguém já está trabalhando nela, não hesite em perguntar (por exemplo, deixando um comentário sobre o problema associado).

<!-- If you are interested in working on the implementation for an 'active' RFC, but
cannot determine if someone else is already working on it, feel free to ask
(e.g. by leaving a comment on the associated issue). -->

## Revisando RFCs

<!-- ## Reviewing RFCs -->

A cada semana, a equipe tenta revisar algum conjunto de _pull requests_ de RFC abertas.

<!-- Each week the team will attempt to review some set of open RFC pull requests. -->

Tentamos garantir que qualquer RFC que aceitamos seja aceito na reunião semanal da equipe. Todo recurso aceito deve ter um ("core team champion")(?), que irá representá-lo, bem como o seu progresso.

<!-- We try to make sure that any RFC that we accept is accepted at the weekly team meeting. Every accepted feature should have a core team champion, who will represent the feature and its progress. -->

**O processo RFC de Gatsby deve sua inspiração ao [processo RFC do React], [processo RFC do Yarn], [processo RFC Rust] e [processo RFC Ember]**
**Gatsby's RFC process owes its inspiration to the [React RFC process], [Yarn RFC process], [Rust RFC process], and [Ember RFC process]**

[processo rfc do react]: https://github.com/reactjs/rfcs
[processo rfc do yarn]: https://github.com/yarnpkg/rfcs
[processo rfc do rust]: https://github.com/rust-lang/rfcs
[processo rfc do ember]: https://github.com/emberjs/rfcs

<!-- [react rfc process]: https://github.com/reactjs/rfcs
[yarn rfc process]: https://github.com/yarnpkg/rfcs
[rust rfc process]: https://github.com/rust-lang/rfcs
[ember rfc process]: https://github.com/emberjs/rfcs -->
