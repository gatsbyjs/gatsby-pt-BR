---
title: Filosofia central do Gatsby
---

A filosofia central de Gatsby pode ser dividida em três partes.

**Primeiro, [nossa visão](#a-visão-do-gatsby).** Nossa visão é _[construir novos alicerces da Web de alto nível](#construir-novos-alicerces-da-web-de-alto-nível)_, e _[criar um sistema de malha de conteúdo coeso](#crie-um-sistema-de-malha-de-conteúdo-coeso)_, para _[tornar a construção de sites divertida](#tornar-a-construção-de-sites-divertida)_ e _[criar uma web melhor](#crie-uma-web-melhor)_.

**Segundo, [nossa filosofia de ferramentas](#filosofia-de-ferramentas-de-gatsby).** Para tornar a construção de sites divertida, as ferramentas do Gatsby devem incorporar certas qualidades. Esses incluem:

- [agrupar o ecossistema de JavaScript moderno](#agrupe-o-ecossistema-de-javascript-moderno-para-o-conteúdo-da-web)
- [divulgação progressiva da complexidade](#divulgar-progressivamente-a-complexidade)

**Terceiro, [nossa filosofia comunitária](#filosofia-comunitária-do-gatsby).** Não podemos fazer isso sozinhos, por isso estamos nos esforçando para criar a comunidade mais inclusiva na web. Por esse motivo, nós _[trabalhamos abertamente](#trabalhe-abertamente)_. Em todos os momentos, acreditamos e nos esforçamos para comunicar que _[você pertence aqui](#você-pertence-aqui)_.

## A visão do Gatsby

### Construir novos alicerces da Web de alto nível

Os alicerces de hoje para a Web são componentes de HTML, CSS e JavaScript.

Acreditamos que em 5 ou 10 anos, olharemos para muitos desses blocos como para o código de máquina ou a linguagem assembly atualmente; idiomas de baixo nível que são ótimos destinos de compilação para idiomas de alto nível mais fáceis de escrever.

Usando abstrações como componentes React, `gatsby-image`, e `gatsby-link`, começamos a criar essa linguagem de alto nível. Mas estamos apenas começando. Gatsby é um playground para descobrir novos blocos de construção para a web.

Para [citar Alan Kay](https://www.youtube.com/watch?v=NdSD07U5uBs):

> “Você obtém simplicidade ao encontrar alicerces um pouco mais sofisticados“.

[Leia mais aqui](/blog/2017-10-16-making-website-building-fun/#find-the-right-building-blocks).

### Crie um "sistema de malha de conteúdo" coeso

Nos últimos anos, as equipes começaram a mudar de configurações integradas monolíticas de CMS para uma "malha de conteúdo" modular, puxando conteúdo e funcionalidade de várias fontes e APIs. O principal desafio: integrar pragmaticamente todas essas peças.

O objetivo de Gatsby é criar um "sistema de malha de conteúdo" que integre as melhores ferramentas modulares de modelagem de conteúdo, autenticação, pesquisa, análise, pagamentos, frameworks de interface do usuário etc. - em um todo unificado e de alta qualidade.

Leia mais em uma [jornada para a malha de conteúdo](/blog/2018-10-04-journey-to-the-content-mesh).

### Tornar a construção de sites divertida

A visão de Gatsby é tornar o desenvolvimento de sites divertido, simplificando-o.

Fred Brooks escreveu em _The Mythical Man-Month_:

> O programador, como o poeta, trabalha apenas um pouco afastado do puro pensamento. [Eles] constroem [seus] castelos no ar, do ar, criando pelo esforço da imaginação. Poucos meios de criação são tão flexíveis, fáceis de polir e retrabalhar, tão prontamente capazes de realizar grandes estruturas conceituais...

A tecnologia é incrivelmente divertida quando nós, como o mago da fantasia, podemos digitar um encantamento em nosso computador e uma nova criação ganha vida.

Quando esse encantamento é simples e leva segundos, podemos facilmente nos perder por horas na corrida da criação, tentando uma coisa após a outra, improvisando nosso caminho para um design eventual.

Desenvolvedores, designers, profissionais de marketing de demanda, redatores -- todas as partes interessadas em um projeto de site _podem_ sentir isso -- com as ferramentas adequadas.

Como Bret Victor sugeriu em _Inventing on Principle_, cada criador precisa "de uma conexão imediata com o que está criando".

Esses loops de feedback instantâneo geralmente são sentidos perto do início dos projetos. Mas eles podem ser rapidamente afogados pela complexidade do projeto.

Os desenvolvedores podem passar horas esperando implantações, rastreando bugs fantasmas de "ferramentas" e assim por diante.

Acreditamos que, com os blocos de construção certos e um sistema integrado de malha de conteúdo, os projetos de sites devem continuar a ser divertidos, independentemente do tamanho deles. Acreditamos que todo membro de uma equipe de sites merece a capacidade de ver facilmente como o trabalho deles se encaixa no todo.

Quando um redator edita uma manchete em seu CMS, um designer desenha um botão em seu aplicativo de ilustração ou um desenvolvedor adiciona uma instrução _if_ em seu editor de texto, eles não deveriam precisar imaginar como é a alteração no contexto. Eles deveriam vê-la imediatamente.

[Leia mais aqui](/blog/2017-10-16-making-website-building-fun/).

### Crie uma web melhor

Os sites podem ter ou não ter muitas qualidades. Eles podem ser rápidos, seguros, sustentáveis, bonitos, acessíveis e baratos (ou não). Eles podem ser fáceis de criar e interagir, ter um ótimo SEO e serem divertido de trabalhar (ou não).

Acreditamos que essas qualidades devem ser integradas em frameworks, para que sejam entregues _por padrão_ em vez de implementadas por site.

Quando recursos e qualidades estão disponíveis apenas se você os implementar, isso os torna um luxo -- disponível apenas para alguns sites.

Por outro lado, ao incorporar qualidades como desempenho e segurança por padrão, Gatsby torna a coisa certa, a coisa fácil.

Acreditamos que a maneira de maior impacto para melhorar a Web é torná-la de alta qualidade por padrão.

## Filosofia de ferramentas de Gatsby

### Agrupe o ecossistema de JavaScript moderno para o conteúdo da web

Uma maneira importante de o Gatsby tornar o conteúdo da web de alta qualidade por padrão é agrupar o ecossistema moderno do JavaScript.

Desenvolvimento tradicional de CMS [apresenta muitos desafios](https://www.gatsbyjs.org/blog/2018-10-11-rise-of-modern-web-development/#traditional-cms-development-presents-challenges) como o desenvolvimento em jardins murados, ambientes locais difíceis de manter e um ambiente-alvo desafiador.

Agrupadores de desenvolvimento web moderno [avançam](https://www.gatsbyjs.org/blog/2018-10-11-rise-of-modern-web-development/#modern-frameworks-offer-stability-and-faster-development) em **desempenho** (divisão de pacotes, pré-busca de assets, suporte offline, otimização de imagem ou renderização no servidor), **experiência do desenvolvedor** (componentização via React, transpilação via Babel, webpack, hot reloading), **acessibilidade**, e **segurança** juntos.

O objetivo do Gatsby é agrupar esses avanços em um pacote fácil de usar. Estamos abertos a todos e quaisquer avanços que estão sendo feitos no mundo moderno do JavaScript e gostaríamos de incorporá-los ao Gatsby!

Para mais informações, veja [os recursos que o Gatsby agrupa](/features).

### Divulgar progressivamente a complexidade

Um conceito que os designers de UX usam para tornar os aplicativos mais fáceis de aprender e menos propensos a erros é chamado de "divulgação progressiva".

Se você estava projetando uma interface do usuário, pode mover recursos avançados ou raramente usados ​​para uma tela secundária, como "configurações avançadas".

A divulgação progressiva simplifica a experiência para a maioria das pessoas, sem limitar as habilidades dos usuários mais avançados.

Divulgamos progressivamente a complexidade criando recursos como modificar a configuração do webpack / Babel, `gatsby-image`, e `gatsby-link` opcionais, opções de configuração únicas e simples. Evitamos cenários de "ejeção" do tipo tudo ou nada, nos quais, para adicionar mais personalização, você precisa deixar a ferramenta para trás e gerenciar toda a complexidade (por exemplo, dependências).

[Leia mais aqui](https://lengstorf.com/progressive-disclosure-of-complexity/).

## Filosofia comunitária do Gatsby

### Trabalhe abertamente

O open source está no centro do sucesso de Gatsby, e um dos princípios centrais do open source é que as coisas são feitas abertamente e sem fumaça e espelhos.

Dois dos principais pontos fortes de Gatsby são sua comunidade e ecossistema.

Estamos convencidos de que o caminho certo a seguir é continuar trabalhando abertamente com confiança e apoio de nossa comunidade.

Qualquer um pode [abrir uma issue](/contributing/how-to-file-an-issue/) e fazer uma pergunta, e nós responderemos. Qualquer pessoa pode enviar uma pull request e forneceremos um feedback honesto sobre ela. Qualquer pessoa pode [enviar uma RFC](/contributing/rfc-process/) para fazer uma grande mudança em Gatsby. E quando quisermos fazer isso, enviaremos uma RFC como proposta.

Muitos dos principais recursos de Gatsby surgiram da conversa entre colaboradores. Se você examinar as issues antigas do Gatsby, verá uma discussão sobre muitas das principais idéias que levaram ao Gatsby - do nosso sistema de plugins às otimizações de desempenho e assim por diante.

### Você pertence aqui

Open source é ótimo para desenvolvedores. Permite:

- criar um corpo de trabalho e experiência que pareça ótimo em um currículo ou CV
- construir uma rede de referência para trabalho remunerado
- transformá-lo em uma fonte sustentável de renda

#### Barreiras à contribuição para o open source

No entanto, existem barreiras significativas para começar no open source.

Primeiro, **começar em open source é assustador**. Projetos de OSS podem ser intimidantes. Eles geralmente têm milhares de linhas de código e toneladas de contexto e histórico necessários. Navegar no GitHub pode ser confuso. E pode haver uma dinâmica social embaraçosa: síndrome do impostor e falta de apoio.

Segundo, **open source é uma despesa que nem todos podem pagar**. Os contribuidores em potencial podem não ter tempo livre para trabalhar em open source e seus trabalhos podem não suportar a contribuição como parte de nossa carga de trabalho.

Terceiro, **muitas pessoas não se vêem representadas em open source.**

#### Superando esses obstáculos

Acreditamos que essas barreiras não são apenas obstáculos à contribuição, mas também obstáculos à criação de projetos prósperos. Quando essas barreiras persistem:

- projetos perdem tantas pessoas brilhantes que têm muito a contribuir
- projetos perdem a oportunidade de adicionar mais mantenedores
- mantenedores existentes perdem a oportunidade de construir redes de suporte

Nossa abordagem é ser proativo na criação de comunidade:

- ativamente contatando e acolhendo novos colaboradores
- lembrando o quão acentuada a curva de aprendizado pode ser
- investir na comunidade como medida primária de sucesso

#### Comunidade é tudo

Para Gatsby, a comunidade de open source é tudo. Queremos ser a comunidade de open source mais acolhedora, inclusiva e divertida do planeta.

Para isso, seguimos um valor fundamental: você pertence aqui.

Algumas coisas que fazemos para criar uma comunidade inclusiva e acolhedora incluem:

- Um [Código de conduta imposto](/contributing/code-of-conduct/)
- [Compromisso de acessibilidade](/blog/2019-04-18-gatsby-commitment-to-accessibility/)
- [Documentos abrangentes](/docs)
- Robôs mais amigáveis
- Confiança implícita
- Gratidão ativa
- [Mentoria ativa](/contributing/pair-programming/)

<<<<<<< HEAD
Criamos uma comunidade ativa com centenas de colaboradores e queremos viver o exemplo do que pode ser uma grande comunidade de open source.
=======
We’ve built an active community with thousands of contributors, and we want to live the example of what a great open source community can be.
>>>>>>> 39369653d2071db17c5edacfda90effe6cd5e96f

[Veja mais aqui](https://www.youtube.com/watch?v=8ARA7AD4yPs&feature=youtu.be&list=PLz8Iz-Fnk_eQGt4-VFFCXYuYcuKaw4F07)
