---
title: Trabalhando com o Netlify CMS
---

Nesse guia, você irá configurar um site para que use o [NetlifyCMS](https://github.com/netlify/netlify-cms) como gerenciador de conteúdo.

O Netlify CMS é um single page app, open-source, escrito em React, que é responsável por permitir que você edite o conteúdo e dados dos seus arquivos de um repositório Git. Armazenar conteúdo puro diretamente no repositório do site estático é a abordagem ideal, permitindo que o conteúdo e o código sejam versionados juntos, mas isso requer que editores não técnicos interajam com serviços como o Github. O Netlify CMS foi criado especificamente para eliminar esse impedimento, ao prover uma sólida interface que funciona bem tanto para usuários técnicos quanto para usuários não técnicos, ele interage com o repositório do seu site estático por meio de uma API, para que quaisquer alterações resultem em um novo commit.

O foco primário do Netlify CMS é para que ele funcione bem com geradores de site modernos, como o Gatsby. A instalação normalmente requer somente um arquivo index.html e uma configuração YAML, porém você irá aproveitar o plugin do Gatsby do Netlify CMS para automáticamente instalar e aos poucos construir o CMS com um site estático.

_Nota: esse guia usa o Gatsby Hello World starter para prover um entendimento básico de como o Netlify CMS funciona com seu site Gatsby. Se você estiver travado, compare seu código com o [projeto exemplo](https://github.com/erquhart/gatsby-netlify-cms-example). Caso queira iniciar com um template completo, confira [gatsby-starter-netlify-cms][1]._

## Configuração

Primeiro, abra uma nova janela de terminal e rode o seguinte comando para criar um novo site. Isso irá criar um novo diretório chamado `netlify-cms-tutorial`, que irá conter o site inicial, porém você pode mudar o "netlify-cms-tutorial" no comando abaixo para o que quiser que seja.

```shell
gatsby new netlify-cms-tutorial https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Agora entre no novo diretório criado e instale o plugin do Gatsby para o Netlify CMS:

```shell
cd netlify-cms-tutorial && npm install --save netlify-cms-app gatsby-plugin-netlify-cms
```

Os plugins do Gatsby são registrados em um arquivo chamado `gatsby-config.js`, presente na raiz do site. Crie o arquivo caso ele não exista, e adicione o seguinte para registar o plugin Netlify CMS:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-netlify-cms`],
}
```

Finalmente, você precisará adicionar a o arquivo de configuração do CMS. O plugin que você acabou de instalar ficará responsavél por criar o app do Netlify CMS e emití-lo para "/admin/index.html", por isso você precisará que o arquivo de configuração esteja no mesmo diretório. O Gatsby irá copiar tudo que estiver na pasta static para o ambiente de produção, então será necessário gravar o arquivo de configuração do Netlify CMS como `static/admin/config.yml`. Vamos criar uma configuração teste agora - adicione isso ao seu novo `config.yml`:

```yaml:title=static/admin/config.yml
backend:
  name: teste-repositorio

media_folder: static/assets
public_folder: /assets

collections:
  - name: blog
    label: Blog
    folder: blog
    create: true
    fields:
      - { name: path, label: Caminho }
      - { name: date, label: Data, widget: datetime }
      - { name: title, label: Título }
      - { name: body, label: Corpo, widget: markdown }
```

Em seguida, no seu terminal, rode o comando `gatsby develop` para iniciar o servidor de desenvolvimento Gatsby. Assim que o servidor estiver rodando, será mostrado no terminal o endereço para visualização. Tipicamente é `http://localhost:8000`. Abra esse endereço no seu browser e você deverá ver o texto "Hello World" no canto superior esquerdo. Agora navegue para `/admin/` - então, se seu site estiver em `http://localhost:8000`, vá para `http://localhost:8000/admin/`. **A barra é obrigatória!**

Você agora estará vendo sua instância do Netlify CMS. Você definiu a coleção "blog" na configuração acima, para que você possa criar blogs, mas o Netlify CMS somente os armazena em memória - se você recarregar a página, suas mudanças não surtirão efeito.

## Salvando em um repositório Git

Para salvar seu conteúdo em um repositório Git, o repositório deverá estar hospedado em um serviço como o Github, e você precisará autenticar-se para que o Netlify CMS possa fazer mudanças por meio da API. Para a maioria dos serviços, incluindo o Github, a autenticação requererá um servidor. [Netlify](https://www.netlify.com), a plataforma web da compania que começou o Netlify CMS, fornece uma solução bem simples (e gratuita) para isso.

Agora é uma ótima hora para considerar que o Netlify CMS é destinado para funcionar em ambiente de produção, como parte do seu site estático, e que o site idealmente deveria estar rodando com deploy contínuo (toda vez que o repositório muda, o site é reconstruído e entregue automáticamente). Quando usado em produção, o Netlify CMS e o seu site Gatsby estarão sincronizados, considerando que o site será reconstruído após qualquer mudança, enquanto que ao rodar o Netlify CMS localmente requer que você atualize seu repositório local toda vez que algo mudar no repositório remoto, para que essas mudanças reflitam no seu site em seu ambiente local.

### Publicando para o GitHub

Nós podemos verificar essa solução acima ao subir o nosso site-teste para o Github e publicá-lo no Netlify. Primeiro, inicialize seu projeto Gatsby como um repositório Git, e em seguida suba-o para o Github. Se você precisar de ajuda nessa parte, confira esse [guia](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) do GitHub.

### Realizando o Deploy no Netlify

Agora você pode publicar seu site Gatsby diretamente do Github para o Netlify com o [create site page](https://app.netlify.com/start) - o comando de build próprio do Gatsby será providenciado automáticamente, apenas selecione seu repositório do Github e siga com as opções padrão. Assim que você conectar seu repositório ao Netlify, a publicação do site irá iniciar. Note que a primeira publicação pode demorar mais, já que muitas coisas não estão salvas em cache ainda. Publicações subsequentes deverão ser mais rápidas.

Assim que a publicação estiver completa, você será capaz de ver seu site online, que irá assemelhar-se ao que foi visto localmente.

### Autenticando com o GitHub

O Netlify CMS precisará autenticar com o Github para salvar as alterações de conteúdo no seu repositório. Como foi mencionado acima, isso requer um servidor, e o Netlify toma conta desse aspecto para você. Primeiro, você precisará adicionar a publicação do seu site como uma aplicação OAuth em suas configurações do Github - apenas siga os passos do [Netlify docs](https://www.netlify.com/docs/authentication-providers/#using-an-authentication-provider). Isso irá permitir que scripts rodando na publicação do seu site, tais como Netlify CMS, para que ele possa acessar sua conta do Github por meio da API.

Por último, precisaremos modificar o seu arquivo de configuração do Netlify CMS com as informações do seu repositório, para que as alterações sejam salvas lá. Altere o valor de `backend` no seu `static/admin/config.yml` para que ele fique similar ao exemplo abaixo. Note que o valor `repo` deve ser composto do seu usuário do GitHub seguido de uma barra para a direita, e na sequência o nome do seu repositório. Se o seu usuário for "seu-usuario" e seu repositório for "repositorio-teste", você deverá inserir "seu-usuario/repositorio-teste".

```yaml:title=static/admin/config.yml
backend:
  name: seu-usuario
  repo: seu-usuario/repositorio-teste
```

Agora você pode salvar seu arquivo config.yml, dê commit dessa mudança, e push para seu repositório do Github.

### Autenticando com o GitLab

Confira no [GitLab Backend](https://www.netlifycms.org/docs/authentication-backends/#gitlab-backend) como configurar para autenticar-se com o GitLab.

Se você usa a opção [Client-Side Implicit Grant](https://www.netlifycms.org/docs/authentication-backends/#client-side-implicit-grant), desabilite o Netlify Identity service no seu `gatsby-config.js`:

```javascript:title=gatsby-config.js
{
  resolve: `gatsby-plugin-netlify-cms`,
  options: {
    enableIdentityWidget: false,
  }
}
```

### Realizando mudanças

Certo - você está preparado para fazer alterações no Netlify CMS e as ver como commits no seu repositório do GitHub! Abra o Netlify CMS no seu site publicado em `/admin/`, permita o acesso ao GitHub quando a janela aparecer (confira se não existem pop-ups bloqueados caso não os veja), e tente criar e publicar uma nova postagem. Quando tiver feito isso, você irá encontrar um novo diretório "blog" em seu repositório no GitHub, que irá conter um arquivo Markdown com o conteúdo da sua postagem!

Essa é a funcionalidade básica do Netlify CMS - prover uma confortavél experiência de edição e prover arquivos puros para o repositório Git. Você já deve ter percebido isso, apesar do arquivo ter sido criado em seu repositório, ele não aparece em lugar algum do seu site. A razão disso é que o Netlify CMS não vai além de criar contepudo puro - isto é, ele é capaz de trabalhar com quase qualquer gerador de site estático, pois ele permite que o gerador determine como será construído o conteúdo puro, tornando em algo útil, seja para um site, app mobile, ou outra coisa qualquer.

Neste momento, o Gatsby não sabe que a postagem está lá, e ele não está pronto para processar Markdown.
Vamos arrumar isso.

## Processando o output do Netlify CMS com Gatsby

O Gatsby pode ser configurado para processar Markdown ao seguir o guia [Adicionando Páginas Markdown](/docs/adding-markdown-pages/) presente na documentação. Nosso arquivo `config.yml` para o Netlify CMS está configurado para usar os mesmos campos que foram utilizados nesse guia, então você pode seguir as instruções ao pé da letra que elas deverão funcionar perfeitamente. **Nota:** Quando estiver configurando o plugin `gatsby-source-filesystem`, no guia Adicionando Páginas Markdown, o caminho para seus arquivos Markdown deverá ser `${__dirname}/blog`;.

Assim que isso estiver completo, faça commite e push de suas mudanças para o seu repositório Github e confira o seu site! A nova postagem do seu blog deverá estar no lugar que foi especificado no campo Caminho durante a criação da postagem no Netlify CMS. Se você seguiu o exemplo no guia do Gatsby, "Adicionando Páginas Markdown" e tiver utilizado o "/blog/my-first-blog", então sua postagem deverá estar em "your-site-name.netlify.com/blog/my-first-blog".

## Encerramento

Esse foi um exemplo bem básico, com o intuito de ajudar você a entender como o Netlify CMS trabalha com o Gatsby. Como mencionado no começo desse guia, se você se sentiu travado, você pode comparar seu código com o [repositório exemplo](https://github.com/erquhart/gatsby-netlify-cms-example), que é um exemplo funcional criado seguindo esse guia. Você também pode entrar em contato com a comunidade do Netlify CMS por meio do [Gitter](https://gitter.im/netlify/netlifycms). Por último, caso queira ir para um exemplo padrão mais completo de como usar o Gatsby e Netlify CMS, você pode clonar e publicar o [Starter inicial de Gatsby com Netlify CMS][1] para o Netlify com [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/netlify-templates/gatsby-starter-netlify-cms&stack=cms).

Você pode ver também o [postagens de blog usando Gatsby + Netlify CMS](/blog/tags/netlify-cms).

[1]: https://github.com/netlify-templates/gatsby-starter-netlify-cms
