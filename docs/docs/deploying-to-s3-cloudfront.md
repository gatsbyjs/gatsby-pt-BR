---
title: Publicando no S3/Cloudfront
---

Esse guia lhe mostrará como hospedar e publicar o seu próximo site Gastby na AWS(Amazon Web Service) usando [S3](https://aws.amazon.com/s3/).
Algo opcional, mas muito recomendado, é que você pode adicionar a CloudFront, uma CDN global que torna o seu site _ainda mais rápido_.

## Começando: AWS CLI

Crie uma [Conta IAM](https://console.aws.amazon.com/iam/home?#) usando permissões administrativas e crie um id de acesso e uma senha para ele.
Você precisará deles para o próximo passos.

Instale o AWS CLI e o configure (Tenha certeza que o Python está instalado na sua máquina antes de rodar esses próximos comandos):

```shell
pip install awscli
aws configure
```

O AWS CLI pedirá uma chave de acesso e uma senha, você só precisa adicionar as que você criou anteriormente.

## Configurando: S3

Agora que seu site Gatsby já está no ar e rodando e o seu acesso à AWS já foi resolvido, você precisará adicionar uma hospedagem e colocar seu site no ar na AWS.

Primeiramente, install o plugin S3 do Gatsby:

```shell
npm i gatsby-plugin-s3
```

Adicione o plugin ao seu `gatsby-config.js`, através do seguinte código: 

> Obs: Não esqueça de mudar o nome do bucket (A propriedade bucketName). 

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-plugin-s3`,
    options: {
      bucketName: "bucket-do-meu-website",
    },
  },
]
```
E finalmente, adicione o script de publicação ao seu `package.json`:

```json:title=package.json
"scripts": {
   ...
   "deploy": "gatsby-plugin-s3 deploy"
}
```

E é só isso!
Rode o comando `npm run build && npm run deploy` para fazer o build e tê-lo imediatamente publicado no S3!

## Publicando com variáveis do `.env`

Algumas publicações precisam que sejam utilizadas variáveis de ambiente. Para fazer a publicação por meio de variáveis 
de ambiente, atualize o script de publicação no seu `package.json`:

```json:title=package.json
"scripts" : {
    ...
    "deploy": "npm run -n \"-r dotenv/config\" && npm run build && gatsby-plugin-s3 deploy"
}
```

Esse comando requer que seja feitos três passos: O `dotenv` primeiro, a execução do build e finalmente a publicação no S3. O `dotenv`, uma dependência do Gastsby que não precisa ser instalada diretamente, carrega as variáveis de ambiente e as torna disponíveis globalmente.

Caso você tenha vários perfis do AWS na sua máquina, é possível fazer a publicação declarando o seu `AWS_PROFILE` (o perfil na AWS) antes do script de publicação:

```shell
AWS_PROFILE=seuNomeDeUsuario npm run deploy
```

## Configurando: ClouFront

O CloudFront é uma CDN global e pode ser usado para tornar o seu site Gatsby super rápido carregar _ainda mais rápido_, especialmente para visitantes de primeira viagem. Além disso, O CloudFront provê uma forma super fácil de fornecer ao seu bucket do S3 um nome de domínio customizado e também suporte HTTPS.
 
Existem algumas coisas que você precisa levar em consideração ao usar o gatsby-plugin-s3 para fazer a publicação de um site que usa CloudFront. 

Existem duas maneira de você conectar o CloudFront a uma origem de um S3. A maneira mais óbvia, que é a que o Console da AWS sugere, é digitar o nome do bucket no campo de Nome de Domínio da Origem. Isso configura uma origem de um S3 e permite que você configure o CloudFront para que ele use o IAM para acessar o seu bucket. Infelizmente, isso também torna impossível que sejam feitos redirecionamento por parte do servidor (301/302), isso significa que os indexes dos diretórios (Ter _index.html_ aparecendo quando alguém tenta acessar o diretório) só funcionarão em diretórios raiz. Talvez você não note esses problemas de primeira, por que o JavaScript da parte do cliente Gatsby compensa pelo lado do cliente e plugins como `gatsby-plugin-meta-redirect` compensam pela parte do servidor. Só por que você não consegue ver esses problemas não significa que eles não vão afetar mecanismos de busca negativamente.

Para que todas as características do seu site funcionem corretamente, você deve usar o ponto de acesso para sites de hospedagem estática do bucket do S3 como ponto de partida do CloudFront. Isso significa que infelizmente o seu bucket terá que ser configurado para que ele seja public-read, já que quando o CLoudFront estiver usando um ponto de acesso para sites de hospedagem estática S3 como ponto de partida, ele fica incapaz de fazer a autenticação via IAM.

### Configurando o gatsby-plugin-s3

No arquivo de configuração do gatsby-plugin-s3 existem dois parâmetros opcionais que você normalmente pode deixar em branco, o `protocol` e o `hostname`. Todavia, quando você estiver usando o CloudFront, esses parâmetros são **vitais** para assegurar que o redirecionamento aconteça de forma correta. Caso você omita esse parâmetros, o redirecionamento acontecerá relativa ao seu ponto de acesso para sites de hospedagem estática do S3. Isso significa que se os usuários visitarem o seu site através da URL do CloudFront e clicarem em redirecionar, eles irão ser redirecionados para o seu ponto de acesso para sites de hospedagem estática do S3. Isso irá desabilitar o HTTPS e (mais importante) irá mostrar uma URl feia e não profissional na barra de endereço do usuário.

Ao especificar os parâmetros `protocol` e o `hostname` você pode fazer com que os redirecionamentos sejam aplicados relativos a um domínio de sua escolha. 

```javascript:title=gatsby-config.js
{
    resolve: `gatsby-plugin-s3`,
    options: {
        bucketName: "my-example-bucket",
        protocol: "https",
        hostname: "www.example.com",
    },
}
```

Se você usar a URL do seu site em outro lugar no gatsby-config.js você pode definir uma variável que recebe a URL no topo desse arquivo de configuração:

```javascript:title=gatsby-config.js
const siteAddress = new URL("https://www.example.com")
```

e então nas configurações Gatsby você pode referenciar essa variável da seguinte forma:

```javascript:title=gatsby-config.js
{
    resolve: `gatsby-plugin-s3`,
    options: {
        bucketName: "my-example-bucket",
        protocol: siteAddress.protocol.slice(0, -1),
        hostname: siteAddress.hostname,
    },
}
```

Caso você precise do endereço completo em outro lugar da sua configuração é possível acessa-lo usando `siteAddress.href`.

## Referências

- [Gatsby na AWS, a forma correta](https://blog.joshwalsh.me/aws-gatsby/)
- [Usando CloudFront com gatsby-plugin-s3](https://github.com/jariz/gatsby-plugin-s3/blob/master/recipes/with-cloudfront.md)
- [Publicando o seu próximo site Gatsby na AWS com o AWS amplify](/blog/2018-08-24-gatsby-aws-hosting/)
- [Escalade Sports: De $5000 para \$5/mês hospedando com Gatsby](/blog/2018-06-14-escalade-sports-from-5000-to-5-in-hosting/)
- [Publicando o seu site Gatsby.js no AWS S3](https://benenewton.com/deploy-your-gatsby-js-site-to-aws-s-3)