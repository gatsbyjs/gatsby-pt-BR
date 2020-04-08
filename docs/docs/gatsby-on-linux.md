---
title: Gatsby no Linux
---

This guide assumes you already have a native installation of Linux on your machine. The following steps walk through how to install Node.js and associated dependencies.

> Isto é um TODO. Ajude a nossa comunidade a expandi-lo.

> Por favor utilize o [Guia de Estilo do Gatsby](/contributing/gatsby-style-guide/) para garantir que seu Pull Request seja aceito.

## Windows Subsystem Linux (WSL)

A partir de 17 de outubro de 2017, o Windows 10 vem com WSL e distribuições Linux estarão disponíveis através da [Windows Store], as quais podem ser configuradas através do `wslconfig` caso haja mais de uma distribuição instalada.

```shell
# definir a distribuição padrão para o Ubuntu
wslconfig /setdefault ubuntu
```

### Utilizando Windows Subsystem Linux: Ubuntu

Se você tem uma instalação limpa do Ubuntu, atualize-o:

```shell
sudo apt update
sudo apt -y upgrade
```

> Só utilize `-y` se você quiser atualizar para a última versão do software.

**Ferramentas de build**

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

Additional dependencies need to be installed as well. `build-essential` is a package that allows other packages to compile to a Debian package. `git` installs a package to work with version control. `linbpng-dev` installs a package that allows the project to manipulate images.

```shell
sudo apt install build-essential
sudo apt install git
sudo apt install libpng-dev
```

Ou para instalar todos ao mesmo tempo e aprovar `(y)` em todas as instalações:

```shell
sudo apt update && sudo apt -y upgrade && sudo apt install build-essential && sudo apt install git && sudo apt install libpng-dev
```

### Additional links and resources

- [Super detailed guide to making VSCode work with ESL from VSCode's docs website](https://code.visualstudio.com/docs/remote/wsl)
- [Microsoft Store page for downloading Ubuntu on Windows](https://www.microsoft.com/en-us/store/p/ubuntu/9nblggh4msv6)
- [n](https://github.com/tj/n)
- [nvm](https://github.com/creationix/nvm)
- [n-install](https://github.com/mklement0/n-install)
- [bash startup](https://github.com/Microsoft/WSL/issues/776#issuecomment-266112578)
