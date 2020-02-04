---
title: Gerenciando Pull Requests
---

Se você deseja ajudar a gerenciar PRs no repositório Gatsby no Github, este documento é para você. Abordaremos as convenções preferidas pela equipe, o que foi verificado em diversos tipos de pull requests, permissões, e orientações de como deixar um comentário. 

Temos mais de 2.000 colaboradores e muito do que torna o Gatsby excelente é contribuído por pessoas como você.

Será desnecessário dizer, temos muitos PRs e mergeamos mais de [100 contribuições](https://twitter.com/kylemathews/status/1111435640581689345) toda semana. Sim, _toda semana_.

Vamos conversar um pouco sobre como gerenciar pull requests no repositório Gatsby.

Para introduzir o que são Pull Requests e como abrir um, confira o documento de contribuição sobre [Como abrir um Pull Request](/contributing/how-to-open-a-pull-request).

## Verificando Pull Request

### Diretrizes Gerais

Algumas coisas gerais para serem verificadas em um pull request são:

<<<<<<< HEAD
- Os links devem ser relativos, em vez de absolutos, ao vincular documentos (`/docs/some-reference/` ao invés de `https://www.gatsbyjs.org/docs/some-reference/`)
- A linguagem deve ser inclusiva e acessível
- Issues e RFCs (se tiver) devem estar vinculados ao endereço deste PR 
=======
- Links ought to be relative instead of absolute when linking to docs (`/docs/some-reference/` instead of `https://www.gatsbyjs.org/docs/some-reference/`)
- Language ought to be inclusive and accessible
- Issues and Requests for Comments (RFCs) (if any) that this PR addresses ought to be linked to
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

> 💡 Ao olhar para um PR pela primeira vez, pode ser de grande ajuda ler sobre problemas vinculados ou [RFCs](/contributing/rfc-process/) (se houver) para entender o contexto sobre o que o PR pretende adicionar ou corrigir.

<<<<<<< HEAD
### Tipos Específicos de Diretrizes
=======
Note for Gatsby Core or Learning team members: if a PR has merge conflicts or needs a little help to push it across the finish line, contributing directly to a fork or branch can be a great way to resolve it. See notes on [pushing to a remote fork in Git](#pushing-changes-to-a-remote-fork).

### Type Specific Guidelines
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Cada tipo de PR também exige um conjunto diferente de verificações antes de serem mergeadas.

Vamos examiná-las abaixo.

#### Documentação

Normalmente, procuramos o seguinte em [PRs que adicionam documentação](/contributing/docs-contributions/): 

- Correção - se a documentação adicionada está tecnicamente correta
- Estilo - se a linguagem escrita segue o nosso [guia de estilo](/contributing/gatsby-style-guide/)
- Cabeçalhos – se os níveis de cabeçalho em um documento começam com h2 (`##` no Markdown) e crescem em ordem, estabelecendo uma hierarquia de conteúdo acessível
- Tipo e Formato - se os documentos e os materiais de aprendizagem estão alinhados com nossas recomendações e [modelos de documentos](/contributing/docs-templates/) 

<<<<<<< HEAD
#### Código
=======
If a PR includes code examples, tutorials, recipes, or actionable guides, the reviewer must test out the material to ensure accuracy. **No PRs should be approved or merged that haven't been vetted for errors or omissions.**

#### Code
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Para [PRs que adicionam código](/contributing/code-contributions/) (seja um recurso ou uma correção) procuramos o seguinte: 

- Corretude — se o código faz o que pensamos que faz
- Testes — ao corrigir um bug ou adicionar um novo recurso, pode ser muito valioso adicionar testes. Embora mergeamos alguns PRs pequenos sem teste, mais frequentemente do que não, é bom ter testes afirmando o comportamento. Pode ser uma combinação de testes unitários para um pacote específico, testes de captura instantânea e testes de ponta a ponta. O objetivo aqui é garantir que algo que está sendo corrigido ou adicionado _permanece_ corrigido ou funcione da maneira que é esperada. Bons testes garantem isso.
- Qualidade do código — concentre-se em alterações razoáveis que provavelmente melhorarão a manutenção, compreensão ou correção do código. Alterações estilísticas são tipicamente sugeridas pelo Prettier. Não escolha.
- Documentação no README do pacote se você estiver adicionando algo

#### Starters ou Mostruários de Site

Para PRs que adicionam um site ou um starter ao mostruário, devemos verificar:

- Verifique se o site ou o starter foi criado com Gatsby
- Links — verifique se os links estão acessíveis e funcionando
- Tags — verifique se as tags correspondem às tags existentes
- Status em destaque — novos sites não devem ser marcados em destaque. 
Os sites em destaque são ocasionalmente atualizados por um membro da equipe Gatsby.

#### Postagens no blog

Para PRs que adicionam postagens, devemos verificar: 

<<<<<<< HEAD
- Corretude — se a documentação adicionada está tecnicamente correta
- Estilo — se a linguagem escrita segue o nosso [guia de estilo](/contributing/gatsby-style-guide/)
- Assunto — as postagens do blog não devem ser puramente promocionais, com spam ou inapropriadas. Um autor deve verificar com um membro da equipe do Gatsby se sua postagem é apropriada para o blog antes de criar seu PR.
- Sensibilidade ao tempo — as postagens do blog levam mais tempo do que os documentos, especialmente porque são enterradas após a publicação de mais postagens. Se algo é continuamente relevante e mais próximo de um tutorial genérico, provavelmente deve estar na seção [Guias de referência](/docs/guides/) dos documentos.
=======
- Approval – has the [blog post been approved](/contributing/blog-and-website-contributions/) by marketing or another Gatsby internal team?
- Correctness — whether the added documentation is technically correct
- Style — whether the written language follows our [style guide](/contributing/gatsby-style-guide/)
- Subject matter — blog posts should not be purely promotional, spammy, or inappropriate. An author should check with a member of the Gatsby team that their post is appropriate for the blog before creating their PR.
- Time Sensitivity — blog posts are more time dependent than docs, especially since they get buried after more posts are published. If something is continually relevant and more of a general how-to, it should go in the [Reference Guides](/docs/guides/) or [Tutorials](/tutorial/) section of the docs.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

## Verificações automáticas

Nosso repositório no [GitHub](https://github.com/gatsbyjs/gatsby) possui várias verificações de _CI_ (Integração Contínua) automatizadas que são executadas automaticamente para todos os PRs. Isso inclui testes, _linting_ e até pré-visualizações para o [gatsbyjs.org](https://www.gatsbyjs.org).

Queremos que todas essas verificações passem. Embora seja bom revisar um PR em andamento com algumas verificações com falha, um PR está pronto para ser enviado quando todos os testes forem aprovados.

Vamos examinar alguns casos falhos comuns e como corrigi-los:

### Linting

Executamos o _lint_ em todo o código e documentação para obter consistência. Você pode acabar desconfiando que seu PR falhou na verificação do _linting_.

Caso o PR seja seu e você tiver o código em sua máquina, você pode executar:

```shell
npm run format
```

Isso reformatará automaticamente suas alterações para atender aos requisitos do _linting_. Não se esqueça de fazer git commit e push com suas novas alterações.

## Outras verificações

### Testando localmente

Embora tenhamos muitos e _muitos_ testes em nosso repositório (que são executados automaticamente em cada commit), pode haver momentos em que exista um caso específico (ou cinco) que não seja coberto por eles.

Nessas situações, testar a alteração localmente pode ser muito valioso.

> 💡 Caso seja a primeira vez que você faça isso, talvez seja necessário [configurar seu ambiente de desenvolvimento](/contributing/setting-up-your-local-dev-environment).

Testar pacotes não publicados localmente pode ser complicado. Felizmente temos a ferramenta certa para facilitar isso.

Diga olá para o seu novo melhor amigo, `gatsby-dev-cli`.

#### gatsby-dev-cli

`gatsby-dev-cli` é uma ferramenta de linha de comando para o desenvolvimento local do Gatsby. Ao fazer alterações nos pacotes gatsby, isso ajuda a copiar as alterações nos pacotes para um site do Gatsby no qual você pode testar suas alterações.

Confira o arquivo [`gatsby-dev-cli` README](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-dev-cli) para saber mais.

### Commit e Título do PR

É bom ter mensagens de commit descritivas para que outras pessoas possam entender o que seu commit está fazendo. Gostamos de [commits convencionais](https://www.conventionalcommits.org/en/v1.0.0-beta.3).

No entanto, os PRs são adicionados quando mergeados, de modo que as mensagens individuais de commit não são tão importantes quanto os títulos de PR.

Vejamos alguns exemplos de bons e ruins títulos de PR:

#### Bons títulos de PR ✅

- tarefa(documentos): Correção dos links na página de contribuições
- feat(gatsby): adição do suporte para manifestos por página
- correções(gatsby-plugin-sharp): Verificação das existência das imagens antes de tentar converter

Estes são bons títulos de PR porque são concisos, específicos e usam o formato [commit convencional](https://www.conventionalcommits.org/pt-br/v1.0.0-beta.4/).

#### Títulos ruins de PR ❌

- novos testes
- adicionar suporte para meus novos cms
- correção de bug no gatsby

Esses são títulos ruins de PR porque são genéricos, não comunicam a alteração corretamente e não usam o formato de commit convencional.

## Fornecer Feedback

- Seja _gentil_. Nos tornamos mais fortes a cada dia por causa da nossa comunidade, por isso a compaixão é importante. Queremos que todos os colaboradores se sintam bem-vindos. 
- Faça sugestões usando o [Recurso de sugestões do GitHub](https://help.github.com/en/articles/commenting-on-a-pull-request#adding-line-comments-to-a-pull-request), se possível. Isso facilita a aceitação de suas sugestões para o autor.
- Link para exemplos quando necessário.
- Tente não fazer [exageros](http://bikeshed.com/) demais.
- Observe quando uma sugestão é opcional (ao contrário de obrigatório)
- Seja objetivo e limite as remoções (alguns são bons se agregar valor ou melhorar a legibilidade do código)
- Não sugira nem espere mudanças fora do escopo que sejam melhor tratadas em um PR separado.

<<<<<<< HEAD
## Direitos e Permisões
=======
## Pushing changes to a remote fork

Sometimes the easiest way to unblock a stalled PR is to sort out merge conflicts or apply remaining suggestions. When the GitHub UI won't cut it, you can (often) apply changes directly to someone's remote fork with Git:

- Add their Gatsby fork as a remote:<br />`git remote add <forkname> git@github.com:<username>/gatsby.git`
- Fetch the branches:<br />`git fetch <forkname>`
- Check out their branch locally:<br />`git checkout -b <branch-name> <forkname>/<branch-name>`
- Make your changes, add some commits
- Push branch to the remote fork (also see [Gotchas](#gotchas) below):<br /> `git push <forkname> head:<branch-name>`

Alternatively, you can manage forks and branches with [hub](https://github.com/github/hub).

## Rights and Permissions
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

### Quem pode revisar um PR?

<<<<<<< HEAD
Se você é um membro da organização [gatsbyjs](http://github.com/gatsbyjs) no GitHub, pode revisar um PR.
=======
If you're a member of the [gatsbyjs](https://github.com/gatsbyjs) organization on GitHub, you can review **most** PRs. PRs with [`topic: internal`](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aopen+is%3Aissue+label%3A%22topic%3A+internal%22) are reserved for Core and Learning team members as they are typically part of an internal project or hiring process.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

> 💡 Ainda não é membro? Deseja [participar da contribuição](/contributing/how-to-contribute/) para projetos open source? Faça sua primeira contribuição e você será convidado automaticamente!

### Quem pode aprovar um PR?

<<<<<<< HEAD
Todo PR aberto no repositório precisa ser aprovado antes que possa ser mergeado. Embora qualquer pessoa que seja membro da organização [gatsbyjs](http://github.com/gatsbyjs) possa aprovar um PR, para ser mergeado, ele precisa ser revisado por um membro da equipe Gatsby.
=======
Every PR opened in the repository needs to be approved before it can be merged. While anyone who is a member of the [gatsbyjs](https://github.com/gatsbyjs) organization can approve a PR, to be merged in, it needs to be reviewed by a member of the team that owns that part of Gatsby.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Normalmente é isso:

<<<<<<< HEAD
- **gatsbyjs/core** para código
- **gatsbyjs/docs** para documentação
=======
- **gatsbyjs/core** for Code
- **gatsbyjs/learning** for Documentation
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

Também temos `CODEOWNERS` definidos em diferentes partes do repositório e uma aprovação por alguém do `CODEOWNERS` para o(s) arquivo(s) que o PR está mudando também pode ser suficiente.

### Quem pode mergear um PR?

Os PRs só podem ser mergeados por membros da equipe principal e pelo Gatsbot.

#### Gatsbot

O Gatsbot é nosso pequeno amigo android que mergea PRs automaticamente que estão prontos para serem usados. Se um PR for aprovado e todas as verificações estiverem passando, adicione a label `bot: merge on green` e o Gatsbot realizará o merge automaticamente.

## Gotchas

- Às vezes você pode querer corrigir algo no PR de outra pessoa. Isso é perfeitamente aceitável, desde que o author não se importe. No entanto, dependendo das configurações você pode achar que não é capaz de seguir com o push dentro do fork. Nesse caso, deixe suas alterações como sugestões.

## Perguntas frequentes

Não temos nenhuma no momento, mas caso você tenha, sinta-se à vontade para contribuir aqui.
