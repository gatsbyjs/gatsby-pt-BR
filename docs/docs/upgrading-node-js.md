---
title: Atualizando sua versão do Node.js.
---

## Política de suporte do Node.js do Gatsby

O Gatsby tem como objetivo oferecer suporte a qualquer versão do Node que tenha um status de release de _Atual_, _Ativo_ ou _Manutenção_. Quando uma versão principal do Node atingir o status de _Fim-de-Vida_, o Gatsby deixará de oferecer suporte a essa versão.


Gatsby deixará de suportar releases _Fim-de-Vida_ do Node em uma versão menor.

Verifique o [documento de releases do Node](https://github.com/nodejs/Release#nodejs-release-working-group) para status das versões.

## Qual versão do Node.js eu tenho?

Execute `node -v` em um terminal para verificar qual sua versão do node instalada.

```shell
node -v
v10.18.0
```

Este exemplo mostra o Node.js. versão 10, especificamente v10.18.0.

## Fazendo upgrade do Node.js versão 8

O Node.js versão 8 atingiu o status _Fim-de-Vida_ em 31 de dezembro de 2019. Muitas dependências do Gatsby estão atualizando para o Node.js versão 10 e superior. O Gatsby também deve atualizar para fornecer novos recursos e correções de erros mais rapidamente.

Geralmente é recomendado você utilizar [a versão do node cujo o status seja o _Atual LTS_](https://github.com/nodejs/Release#nodejs-release-working-group) (Node 10 no momento da escrita). 

> E o Node.js 9? As versões estáveis do Node.js são versões com numeração par - Node.js 6, Node.js 8, Node.js 10 etc. Use apenas números de versão ímpar se desejar experimentar os recursos experimentais.


Existem várias maneiras de atualizar sua versão do Node.js, dependendo de como você a instalou originalmente. Leia para encontrar a melhor abordagem para você.

### Usando Homebrew

Esta é a maneira recomendada de instalar uma versão mais recente do Node.

Você terá o homebrew instalado no seu computador se [seguir a parte zero do tutorial do Gatsby](/tutorial/part-zero/#install-nodejs-for-your-appropriate-operating-system). O Homebrew é um programa que permite instalar versões específicas do Node.js (e outros softwares).

Para atualizar do Node.js 8 para o Node.js 10 usando o Homebrew, abra um terminal e execute os seguintes comandos:


```shell
brew search node
```

Você deve ver uma tela semelhante a esta:

```shell
brew search node
==> Formulae
heroku/brew/heroku-node ✔        llnode                           node@10                          nodebrew
leafnode                         node ✔                           node@8                           nodeenv
libbitcoin-node                  node-build                       node_exporter                    nodenv
```

Você está interessado na próxima versão estável do Node.js após o Node.js 8, que é o Node.js 10. O Homebrew torna isso disponível em um pacote chamado `node@10`. Execute:

```shell
brew install node@10
```

Quando completo, execute:

```shell
node -v
```

para confirmar que você atualizou do Node.js versão 8 para a versão 10.

### Usando um pacote de gerenciamento de versão do Node.js

Existem dois pacotes populares usados para gerenciar várias versões do Node.js no seu sistema. Use um destes para atualizar para uma versão mais recente do Node.js, se eles já estiverem disponíveis no seu computador.

Esses gerenciadores de pacotes são muito úteis para pessoas que trabalham regularmente com diferentes versões do Node.js.

#### nvm

Execute

```shell
nvm
```

em um terminal para ver se o nvm está instalado no seu sistema. Se estiver instalado, você pode executar:

```shell
nvm install 10
nvm alias default 10
```

para instalar e usar o Node.js versão 10.

[Consulte a documentação da nvm para obter mais instruções](https://github.com/nvm-sh/nvm).

#### n

Execute:

```shell
n
```

em um terminal para ver se n está instalado no seu sistema. Se estiver instalado, você pode executar o `n 10` para instalar e usar o Node.js versão 10.

[Consulte a documentação do n para obter mais instruções](https://github.com/tj/n).

### Instalando a partir do nodejs.org

Se você não estiver usando nenhum dos métodos de instalação listados anteriormente, poderá [baixar um instalador do Node.js. diretamente do nodejs.org](https://nodejs.org/en/).

A maneira recomendada pelo Gatsby de instalar o Node.js é usando o Homebrew. Consulte a seção anterior ["Usando Homebrew" deste documento](#usando-homebrew) para mais informações.

## Conclusão

O Gatsby leva a sério a compatibilidade com versões anteriores e visa oferecer suporte a versões mais antigas do Node.js pelo maior tempo possível. Entendemos que manipular diferentes versões de software não é uma maneira produtiva de passar o seu dia.

Gatsby também conta com um enorme ecossistema de dependências de JavaScript. À medida que o ecossistema se afasta das versões mais antigas e não suportadas do Node.js, precisamos acompanhar o ritmo para garantir que os bugs possam ser corrigidos e os novos recursos possam ser lançados.

Neste documento, você aprendeu como atualizar do Node.js versão 8 (que atingiu o status _Fim-de-Vida_), para o Node.js versão 10 (que atingiu o status de _Manutenção_).
