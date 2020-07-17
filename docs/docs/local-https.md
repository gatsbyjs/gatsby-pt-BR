---
title: HTTPS Local
---
Gatsby fornece um jeito fácil de utilizar um servidor HTTPS local durante o desenvolvimento, graças ao [devcert](https://github.com/davewasmer/devcert). Quando você habilita a opção `https`, uma chave privada e um arquivo de certificado serão criados para o seu projeto e usados pelo servidor de desenvolvimento.

## Uso (HTTPS automático)

Comece o servidor de desenvolvimento usando `npm run develop` como usualmente, e adicione as flags `-S` ou `--https`.

    $ npm run develop -- --https

## Configuração

Quando você estiver configurando o certificado SSL pela primeira vez, você pode ser solicitado para digitar sua senha depois de iniciar o ambiente de desenvolvimento:

    informações de configuração do certificado SSL (pode necessitar do sudo)

    Password:

Isso é necessário _somente_ na primeira vez em que você usa o recurso HTTPS do Gatsby em seu computador. Depois disso, os certificados serão criados em tempo real.

Após digitar sua senha, o `devcert` tentará instalar algum software necessário para informar ao Firefox (e Chrome, somente no Linux) que confie nos seus certificados de desenvolvimento.

    Unable to automatically install SSL certificate - please follow the
    prompts at http://localhost:52175 in Firefox to trust the root certificate
    See https://github.com/davewasmer/devcert#how-it-works for more details
    -- Press <Enter> once you finish the Firefox prompts --

Se você deseja oferecer suporte ao Firefox (ou Chrome no Linux), visite `http://localhost:52175` no Firefox e siga as instruções do assistente. Aliás, você pode pressionar enter sem seguir as instruções. **Lembrete: você somente irá fazer isso uma vez por computador.**

Agora abra o servidor de desenvolvimento em `https://localhost:8000` e aproveite o HTTPS  ✨. Claro, você pode alterar a porta de acordo com suas configurações.

Saiba mais sobre [como o devcert funciona](https://github.com/davewasmer/devcert#how-it-works).

## Chaves e arquivos de certificados customizados

Você pode precisar de uma chave personalizada e um arquivo de certificado para HTTPS se usar várias máquinas para desenvolvimento (ou se o seu ambiente de desenvolvimento estiver em container no Docker).

Se você precisar usar uma configuração HTTPS customizada, você pode passar as flags `--https`, `--key-file` e
`--cert-file` no comando `npm run develop`.

- `--cert-file` [relativo ao caminho do arquivo de certificado SSL]
- `--key-file` [relativo ao caminho do arquivo de chave SSL]

Veja o comando de exemplo:

```shell
gatsby develop --https --key-file ../relative/path/to/key.key --cert-file ../relative/path/to/cert.crt
```

na maioria dos casos, o `--https` passado por si só é mais fácil e mais conveniente para obter o HTTPS local.

---
Tenha em mente que certificados automáticos marcados com a flag `--https` são emitidos unicamente para o `localhost` e serão aceitos somente lá. Usá-lo junto com a opção `--host` provavelmente resultará em avisos do navegador.
