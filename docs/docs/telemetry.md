---
title: Telemetria
---

O Gatsby contém um recurso de telemetria que coleta informações de uso anônimas usadas para ajudar a melhorar o Gatsby para todos os usuários.
A base de usuários do Gatsby está crescendo muito rapidamente. É importante que nossa pequena equipe e a grande comunidade entendam melhor os padrões de uso, para que possamos decidir como projetar recursos futuros e priorizar o trabalho atual.

Você será notificado ao instalar o Gatsby e ao executá-lo pela primeira vez.

## Como optar por não participar

Os usuários sempre podem optar pela exclusão da telemetria com `gatsby telemetry --disable` ou configurando a variável de ambiente `GATSBY_TELEMETRY_DISABLED` para `1`

## Por quê?

A análise de usuários **anônima** agregada nos permite priorizar correções e recursos com base em como e quando as pessoas usam o Gatsby.
Como grande parte da funções do Gatsby gira em torno de plugins e starters, queremos coletar informações sobre o uso e confiabilidade, para que possamos garantir um ecossistema de alta qualidade.

Isso levanta uma questão: como usaremos esses dados de telemetria para melhorar o ecossistema? Alguns exemplos úteis são:

- Poderemos entender quais plugins normalmente são usados juntos. Isso nos permitirá exibir essas informações em nossa biblioteca pública de plug-ins e criar starters e tutoriais mais relevantes com base nesses dados.
- Poderemos mostrar a popularidade de diferentes starters na página do showcase.
- Poderemos obter mais detalhes sobre os tipos de erros que os usuários estão enfrentando em _cada_ estágio do processo de build (por exemplo, desenvolvimento, build etc.). Isso nos permitirá melhorar a qualidade de nossa ferramenta e focar melhor nosso tempo na solução de problemas mais comuns e frustrantes.
- Poderemos demonstrar a confiabilidade de diferentes plugins e starters e detectar quais deles tendem a errar com mais frequência. Podemos usar esses dados para exibir métricas de qualidade e melhorar a qualidade de nossos plugins e starters.
- Poderemos ver o momento para os diferentes estágios do processo de build para nos guiar onde devemos focar no trabalho de otimização.

## O que rastreamos?

Nós rastreamos detalhes gerais de uso, incluindo chamada de comando, atualizações de status do processo de build, medições de desempenho e erros.
Usamos essas métricas para entender melhor os padrões de uso. Essas métricas nos permitirão decidir melhor como projetar recursos futuros e priorizar o trabalho atual.

Especificamente, coletamos as seguintes informações para _todos_ eventos de telemetria:

- Registro de data e hora da ocorrência
- Comando invocado (por exemplo, `build` ou `develop`)
- ID da máquina Gatsby. Isso é gerado com o UUID e armazenado na configuração global do gatsby em ~/.config/gatsby/config.json.
- ID da sessão exclusivo. Isso é gerado em cada execução com o UUID.
- Hash unidirecional do diretório de trabalho atual ou um hash do git remote
- Informações gerais no nível do sistema operacional (sistema operacional, versão, arquitetura da CPU e se o comando é executado dentro de um IC)
- Versão atual do Gatsby

O acesso aos dados brutos é altamente controlado e não podemos identificar usuários individuais do conjunto de dados. É anonimizado e não rastreável de volta ao usuário.

## E os dados sensíveis? (ex. segredos)

Realizamos etapas adicionais para garantir que dados sigilosos (por exemplo, variáveis de ambiente usadas para armazenar segredos para o processo de build) **não** cheguem as nossas análises. [Retiramos logs, mensagens de erro etc.](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-telemetry/src/error-helpers.js) desses dados confidenciais para garantir que nunca obtenhamos acesso a esses dados confidenciais.

Você pode visualizar todas as informações enviadas pela telemetria do Gatsby, definindo a variável de ambiente `GATSBY_TELEMETRY_DEBUG` como `1` para imprimir os dados de telemetria em vez de enviá-los.
