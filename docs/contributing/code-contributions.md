---
title: Contribuições de Código
---

A beleza em contribuir com o _open source_ é que você pode dar _clone_ em seu projeto favorito, rodá-lo localmente e fazer experimentos e mudanças em tempo real! A sensação é como se você fosse um mago.

Esta página contém os seguintes tópicos:

- [Configurando o repositório](#configurando-o-repositório)
- [Criando seus próprios plugins e loaders](#criando-seus-próprios-plugins-e-loaders)
- [Fazendo mudanças na biblioteca starter](#fazendo-mudanças-na-biblioteca-starter)
- [Contribuindo com sites exemplo](#contribuindo-com-sites-exemplo)
- [Usando Docker para configurar um ambiente de teste](#usando-docker-para-configurar-um-ambiente-de-teste)
- [Ferramentas de desenvolvimento](#ferramentas-de-desenvolvimento)

## Configurando o repositório

Esta página inclui detalhes específicos de códigos base do ecossistema e do núcleo do Gatsby.

Para começar a configurar o repositório Gatsby em sua máquina usando git, Yarn e Gabsty-CLI,  recomendamos a leitura deste documento: [configurando o seu ambiente local de desenvolvimento](/contributing/setting-up-your-local-dev-environment/).


Caso queira, você pode pular a configuração local e optar pelo [ambiente de desenvolvimento online](/contributing/using-an-online-dev-environment/).

Para contribuir com o blog ou o site do Gatsby, siga os passos descritos em [contribuições do blog e site](/contributing/blog-and-website-contributions/). Para instruções de como contribuir com a documentação, visite a [página de contribuição da documentação](/contributing/docs-contributions/).

## Criando seus próprios _plugins_ e _loaders_

Caso você já tenha criado um _loader_ ou _plugin_, nós adoraríamos que você o compartilhasse e publicasse no npm. Para mais informações em como criar _plugins_ customizáveis, recomendamos a leitura da documentação dos [plugins](/docs/plugins/) e a da [especificação da API](/docs/api-specification/).

## Fazendo mudanças na biblioteca _starter_

Nota: Você não precisa seguir esses passos para poder submeter para a biblioteca _starter_. Isso é apenas necessário caso você quisesse contribuir com alguma funcionalidade da _starter_. Você pode submeter para a biblioteca [seguindo estes passos](/contributing/submit-to-starter-library/).

Caso você queira desenvolver na biblioteca _starter_, será necessário fornecer um _token_ de acesso pessoal do Github.

1. Crie um _token_ de acesso pessoal acessando as suas [Configurações de Desenvolvedor](https://github.com/settings/tokens) do Github.
2. Ao configurar o novo _token_, certifique-se de selecionar o escopo "public_repo".
3. Crie um arquivo na raiz de `www` chamado `.env.development`, em seguida, adicione o _token_ seguindo o modelo abaixo:

```text:title=.env.development
GITHUB_API_TOKEN=SEU_TOKEN_AQUI
```

O arquivo `.env.development` é ignorado pelo git. Seu _token_ nunca deve ser "comitado".

## Contribuindo com sites exemplo

A política do Gatsby é de que o "uso" de sites exemplo (como os presentes na [pasta de exemplos do repositório](https://github.com/gatsbyjs/gatsby/tree/master/examples)) devem estar em torno apenas da utilização de _plugins_ mantidos pela equipe principal, uma vez que seria difícil manter as coisas atualizadas de outra forma.

Para contribuir com sites exemplo, é recomendado criar seu próprio repositório no Github e vinculá-lo a partir de seu _plugin_ de origem, etc.

## Usando Docker para configurar um ambiente de teste

Com todas essas possibilidades de integração com o Gatsby, talvez ajude subir um contêiner Docker com as aplicações que você precisa testar. Isso torna a instalação muito mais simples, além de permitir que você foque menos na configuração e mais nos detalhes de integração que são mais importantes para você.

> Você tem alguma configuração (_setup_) que não está listado aqui? Compartilhe conosco adicionando sua configuração neste arquivo e abrindo uma PR.

### Docker, WordPress e Gatsby

Para instalar o WordPress e usar junto com o Gatsby, recomendamos o uso do arquivo `docker-compose.yml`:  

```yaml:title=docker-compose.yml
version: "2"

services:
  db:
    image: mysql:5.6
    container_name: sessions_db
    ports:
      - "3306:3306"
    volumes:
      - "./.data/db:/var/lib/mysql"
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    image: wordpress:latest
    container_name: sessions_wordpress
    depends_on:
      - db
    links:
      - db
    ports:
      - "7000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_PASSWORD: wordpress
    volumes:
      - ./wp-content:/var/www/html/wp-content
      - ./wp-app:/var/www/html

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: sessions_phpmyadmin
    environment:
      - PMA_ARBITRARY=1
      - PMA_HOST=sessions_db
      - PMA_USER=wordpress
      - PMA_PASSWORD=wordpress
    restart: always
    ports:
      - 8080:80
    volumes:
      - /sessions
```

Use esse arquivo acima enquanto estiver seguindo o tutorial de instalação do WordPress do Docker: https://docs.docker.com/compose/wordpress/

Ao usar o Docker Compose, você tem a opção de iniciar e pausar instâncias do WordPress, além de poder integrá-las com o [Gatsby WordPress source plugin](/docs/sourcing-from-wordpress/).

## Ferramentas de desenvolvimento

### Depurando o processo de _build_

Confira a página [Depurando o processo de _build_](/docs/debugging-the-build-process/) para aprender a como depurar em Gatsby.

<!-- ## _Feedback_

At any point during the contributing process the Gatsby team would love to help! For help with a specific problem you can [open an issue on GitHub](/contributing/how-to-file-an-issue/). Or drop in to [our Discord server](https://gatsby.dev/discord) for general community discussion and support. -->
