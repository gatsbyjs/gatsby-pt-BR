---
title: Configurando Certificados AC
---

Se você está usando um registro privado de pacote que requer um certificado de uma AC (autoridade de certificação), você provavelmente precisará configurar o certificado na sua configuração do `npm`, `yarn`, e `node`.

## Erros comuns por má configuração de certificados

Se você está vendo erros como `unable to get local issuer certificate` na saída do console enquanto você tenta instalar um plugin do Gatsby, uma má configuração de certificado provavelmente é o problema. Isso ocorre particularmente com plugins ou temas que precisam ser buildados em módulos nativos de Node.js (e.x. `gatsby-plugin-sharp`). Provavelmente isso acontecerá quando você estiver instalando pacotes com registro privado (via `npm install` ou `yarn install`) sem uma configuração apropriada do certficado.

## opção de configuração cafile

Ambos [npm](https://docs.npmjs.com/misc/config#cafile) e [yarn](https://yarnpkg.com/lang/en/docs/cli/config/) suportam a opção de configuração `cafile`. Vocẽ terá que adicionar `cafile` como a chave, e setar o caminho até o seu certificado como o valor.

### Usando npm para configurar o cafile

```shell
npm config set cafile "caminho-para-o-meu-certificado.pem"
```

Para checar o valor do caminho do seu certificado na chave do `cafile`, use o seguinte comando para listar todas as chaves presentes na configuração do seu npm:

```shell
npm config ls -l
```

### Utilizando yarn para configurar o cafile

```shell
yarn config set cafile "caminho-para-o-meu-certificado.pem"
```

Agora você pode verificar os valores na configuração do seu yarn com o seguinte comando:

```shell
yarn config list
```

### Utilizando Node.js


Como forma alternativa você também pode configurar isto para Node.js na sua máquina. Exporte o caminho para o seu certificado com a variável `NODE_EXTRA_CA_CERTS`:

```shell
export NODE_EXTRA_CA_CERTS=["caminho-para-o-meu-certificado.pem"]
```
