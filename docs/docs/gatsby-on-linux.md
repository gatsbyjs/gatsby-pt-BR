---
title: Gatsby no Linux
---

Este guia assume que você já possui uma instalação nativa do Linux em sua máquina. As etapas a seguir mostram como instalar o Node.js e dependências associadas.

## Ubuntu, Debian, e outras distros baseadas no `apt`

Comece atualizando os pacotes do sistema operacional já existentes.

```shell
sudo apt update
sudo apt -y upgrade
```

Instale o cURL que permite transferência de dados e o download de dependências adicionais.

```shell
sudo apt install curl
```

Agora você pode usar o `curl` para instalar o `nvm`, que irá gerenciar a instalação do `node` e todas suas versões associadas.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Observe que esta é a versão estável atual do nvm. A instalação completa e resolução de problemas podem ser encontradas na [página do nvm no GitHub](https://github.com/nvm-sh/nvm)

O `nvm` não instala uma versão do `node`. Então você precisa instalar a versão que você deseja e fornecer ao `nvm` as instruções para utilizá-la como padrão. Este exemplo usa o último lançamento da versão `10`, mas novas versões podem ser usadas também.

```shell
nvm install 10
nvm use 10
```

Para ter certeza que a instalação foi bem sucedida, use o seguinte comando.

```shell
node -v
```

> Observe que `npm` vem no mesmo pacote que o `node`

Por último, instale o `git` que vai ser necessário para criar seu primeiro projeto do Gatsby baseado em template `starter`

```shell
sudo apt install git
```

## Fedora, RedHat e outras distros baseadas no `dnf`

Estas distros já vem com o `curl` instalado, então já podemos usá-lo para baixar o `nvm`

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Observe que esta é a versão estável atual do nvm. A instalação completa e resolução de problemas podem ser encontradas na [página do nvm no GitHub](https://github.com/nvm-sh/nvm)

O `nvm` não instala uma versão do `node`. Então você precisa instalar a versão uma versão e fornecer ao `nvm` as instruções para utilizá-lo. Este exemplo usa o último lançamento da versão `10`, mas novas versões podem ser usadas também.


```shell
nvm install 10
nvm use 10
```

Para ter certeza que a instalação foi bem sucedida, use o seguinte comando.

```shell
node -v
```

> Observe que `npm` vem no mesmo pacote que o `node`

Por último, instale o `git` que vai ser necessário para criar seu primeiro projeto do Gatsby baseado em template `starter`

```shell
sudo dnf install git
```

## Archlinux e outras distros baseadas em `pacman`

Comece atualizando os pacotes já existentes

```shell
sudo pacman -Sy
```

Estas distros já vem com o `curl` instalado, então já podemos usá-lo para baixar o `nvm`.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Observe que esta é a versão estável atual do nvm. A instalação completa e resolução de problemas podem ser encontradas na [página do nvm no GitHub](https://github.com/nvm-sh/nvm)

Antes de usar o `nvm`, você precisa instalar as dependências adicionais.

```shell
sudo pacman -S grep awk tar git
```

O `nvm` não instala uma versão do `node`. Então você precisa instalar a versão uma versão e fornecer ao `nvm` as instruções para utilizá-lo. Este exemplo usa o último lançamento da versão `10`, mas novas versões podem ser usadas também.

```shell
nvm install 10
nvm use 10
```

Para ter certeza que a instalação foi bem sucedida, use o seguinte comando.

```shell
node -v
```

> Observe que `npm` vem no mesmo pacote que o `node`

## Windows Subsystem Linux (WSL)

Este guia pressupõe que você já possui o WSL instalado com uma distribuição Linux em funcionamento. Caso não possua, siga as instruções [deste guia da Microsoft](https://docs.microsoft.com/pt-br/windows/wsl/install-win10) para instalar o WSL e uma distro linux de sua escolha.

A partir de 17 de outubro de 2017, o Windows 10 é fornecido com distribuições WSL e Linux disponíveis na Microsoft Store, existem várias distribuições diferentes para usar que podem ser configuradas via `wslconfig` se você tiver mais de uma distribuição instalada.

```shell
# definir a distribuição padrão para o Ubuntu
wslconfig /setdefault ubuntu
```

> Observe que, se você usou a configuração do [Gatsby no Windows](/docs/gatsby-on-windows/) sem o WSL, então você tem que pagar qualquer pasta `node_modules` do seu projeto e reinstalar usando as dependências  no seu ambiente WSL.

### Usando o WSL: Ubuntu

Se você tem uma instalação limpa do Ubuntu, atualize-o:

```shell
sudo apt update
sudo apt -y upgrade
```

**Build tools**

Para compilar e instalar addons nativos do npm, talvez você precise instalar ferramentas nativas para `node-gyp`:

```shell
sudo apt install -y build-essential
```

**Instalando o node**

Seguir as instruções de instalação do nodejs.org pode resultar em uma instalação ligeiramente quebrada (e.g erros de permissão quando tenta executar `npm install`). Ao invés disso, tente instalar versões do node utilizando [n] que você pode instalar com [n-install]:

```shell
curl -L https://git.io/n-install | bash
```

Existem outras alternativas para gerenciar as versões do node, como o [nvm], contudo sabe-se que o uso desse gerenciador é lento [bash startup] no WSL.

### Utilizando Windows Subsystem Linux: Debian

A configuração do Debian é aproximadamente idêntica ao Ubuntu, com exceção da instalação adicional do `git` e do `libpng-dev`.

Begin by updating and upgrading.

```shell
sudo apt update
sudo apt -y upgrade
```

É necessário instalar dependências adicionais, como: `build-essential`  é um pacote que permite outros pacotes compilar em pacotes Debian; `git` instala os pacotes para funcionar com o sistema de controle de versão e `linbpng-dev` instala um pacote que permite o projeto manipular imagens.

```shell
sudo apt install build-essential
sudo apt install git
sudo apt install libpng-dev
```

Ou para instalar todos ao mesmo tempo e aprovar `(y)` em todas as instalações:

```shell
sudo apt update && sudo apt -y upgrade && sudo apt install build-essential && sudo apt install git && sudo apt install libpng-dev
```

### Links e recursos adicionais

- [Guia super detalhado para fazer o VSCode funcionar com ESL no site de documentos da VSCode](https://code.visualstudio.com/docs/remote/wsl)
- [Página da Microsoft Store para baixar o Ubuntu no Windows](https://www.microsoft.com/pt-br/store/p/ubuntu/9nblggh4msv6)
- [n](https://github.com/tj/n)
- [nvm](https://github.com/creationix/nvm)
- [n-install](https://github.com/mklement0/n-install)
- [bash startup](https://github.com/Microsoft/WSL/issues/776#issuecomment-266112578)
