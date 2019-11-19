---
title: Processo RFC
---

## O que é o processo RFC?

Muitas mudanças, incluindo correções de bugs e melhorias na documentação, podem ser implementadas e revistas através do fluxo de trabalho normal da _pull request_ do GitHub.

Algumas mudanças, no entanto, são "substancias", e por esse motivo, solicitamos que sejam submetidas a um processo de _design_, de modo a produzir um consenso entre os participantes da equipe principal do Gatsby.

O processo "RFC" (em português, "solicitação de comentários") visa fornecer um caminho consistente e controlado para que novos recursos sejam inseridos no projeto.

[Lista de RFCs Ativas](https://github.com/gatsbyjs/rfcs/pulls)

Gatsby ainda está **desenvolvendo ativamente** esse processo, e ainda o mudará à medida que mais recursos forem implementados e a comunidade optar por abordagens específicas para o desenvolvimento de recursos.

## Quando seguir esse processo

Você deve considerar usar esse processo se pretende fazer alterações "substanciais" no Gatsby ou em sua documentação. Alguns exemplos que se beneficiariam de uma RFC são:

- Um novo recurso que cria uma nova área de superfície na API e requer um _feature flag_ se introduzido.
- A remoção de recursos que já foram disponibilizados como parte da _release channel_.
- A introdução de novos usos ou convenções idiomáticas, mesmo que não incluam alterações de código no próprio Gatsby.

O processo RFC é uma ótima oportunidade para atrair mais atenção da sua proposta antes de se tornar parte de uma versão lançada do Gatsby. Muitas vezes, até propostas que parecem "óbvias" podem ser significativamente melhoradas quando um grupo maior de pessoas interessadas tiver a chance de avaliá-las.

O processo RFC também pode ser útil para incentivar discussões sobre um recurso proposto enquanto ele está sendo projetado e incorporar restrições importantes ao design enquanto é mais fácil alterá-lo, antes da sua completa implementação.

Algumas alterações não requerem uma RFC:

- Reformular, reorganizar ou refatorar a adição ou remoção de avisos
- Modificações que melhoram estritamente os critérios de qualidade numéricos e objetivos (aceleração, melhor suporte ao navegador)
- Modificações que provavelmente só serão _notadas por_ outros implementadores de Gatsby, e invisíveis para os usuários.

## Qual é o processo

Em resumo, para adicionar um recurso importante ao Gatsby, geralmente é possível fazer o _merge_ da RFC ao repositório de RFCs como um arquivo _markdown_. Nesse ponto, a RFC está 'ativa' e pode ser implementada com o objetivo de eventual inclusão no Gatsby.

- Faça o _fork_ do repositório RFC https://github.com/gatsbyjs/rfcs. Copie `0000-template.md` para
- `text / 0000-my-feature.md` (onde 'my-feature' é descritivo. Não atribua um número à RFC ainda).
- Preencha a RFC. Tenha cuidado com os detalhes: **RFCs que não apresentar motivação convincente, demonstrar uma compreensão do impacto do design ou ser dissimulados sobre os inconvenientes ou as alternativas tendem a ser mal recebidas**.
- Envie uma _pull request_. Como _pull request_, a RFC receberá um _feedback_ de design da comunidade, e o autor deve estar preparado para revisá-lo em resposta.
- Crie consenso e integre feedback. As RFCs que têm amplo suporte têm muito mais probabilidade de progredir do que aquelas que não recebem comentários.
- Eventualmente, a equipe decidirá se a RFC é um candidata à inclusão ao Gatsby.
- As RFCs candidatas à inclusão no Gatsby entrarão em um "período final para comentários" com duração de três dias. O início deste período será sinalizado com um comentário e uma _tag_ na _pull request_ das RFCs.
- Uma RFC pode ser modificada com base no feedback da equipe e da comunidade. Modificações significativas podem desencadear um novo período final para comentários.
- Uma RFC pode ser rejeitada pela equipe após a discussão pública ter sido resolvida e comentários foram feitos resumindo a justificativa da rejeição. Um membro da equipe deve fechar a _pull request_ associada aos RFCs.
- Uma RFC pode ser aceita no final do seu período final de comentários. Um membro da equipe fará o _merge_ da _pull request_ associada às RFCs, quando, então, se tornará 'ativa'.

## O ciclo de vida da RFC

Depois que uma RFC se torna ativa, os autores podem implementá-la e submeter o recurso como uma _pull request_ ao repositório Gatsby. Tornar-se "ativa" não corresponde a uma "aprovação automática" e, em particular, ainda não significa que o recurso será posto em produção; isso indica apenas que, a princípio, há concordância com equipe principal, e que o _merge_ é factível.

Além disso, o fato de uma determinada RFC ter sido aceita e está 'ativa' não implica nada sobre qual prioridade é atribuída à sua implementação, nem se alguém está atualmente trabalhando nela.

Modifications to active RFCs can be done in followup PRs. We strive to write each RFC in a manner that it will reflect the final design of the feature; but the nature of the process means that we cannot expect every merged RFC to actually reflect what the end result will be at the time of the next major release; therefore we try to keep each RFC document somewhat in sync with the language feature as planned, tracking such changes via followup pull requests to the document.

## Implementando uma RFC

O autor de uma RFC não é obrigado a implementá-la. Obviamente, o autor da RFC (como qualquer outro desenvolvedor) pode publicar uma implementação para revisão após a aceitação da RFC.

Se você estiver interessado em trabalhar na implementação de uma RFC 'ativa', mas não puder determinar se alguém já está trabalhando nela, não hesite em perguntar (por exemplo, deixando um comentário sobre o problema associado).

## Revisando RFCs

A cada semana, a equipe tenta revisar algum conjunto de _pull requests_ de RFC abertas.

Tentamos garantir que qualquer RFC que aceitamos seja aceito na reunião semanal da equipe. Todo recurso aceito deve ter um ("core team champion")(?), que irá representá-lo, bem como o seu progresso.

**O processo RFC de Gatsby deve sua inspiração ao [processo RFC do React], [processo RFC do Yarn], [processo RFC do Rust] e [processo RFC do Ember]**

[processo rfc do react]: https://github.com/reactjs/rfcs
[processo rfc do yarn]: https://github.com/yarnpkg/rfcs
[processo rfc do rust]: https://github.com/rust-lang/rfcs
[processo rfc do ember]: https://github.com/emberjs/rfcs
