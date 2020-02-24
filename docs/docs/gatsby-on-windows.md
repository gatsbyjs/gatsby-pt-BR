---
title: Gatsby no Windows
---

## Configurando seu ambiente para criar módulos nativos do Node.js.

Muitos plugins e temas do Gatsby exigem a criação de módulos nativos do Node.js, e.g.
[Sharp (uma dependência comum de Gatsby usada para processamento de imagem)](/packages/gatsby-plugin-sharp/).
Para fazer isso, você precisa de um ambiente de construção funcional (Python e Visual C ++ Build Tools).

A maneira mais fácil de configurar seu ambiente de compilação no Windows é instalar o pacote
[`windows-build-tools`](https://github.com/felixrieseberg/windows-build-tools)
rodando `npm install windows-build-tools -g` no console PowerShell como administrador.


Ao instalar este pacote, ele baixa e instala o Visual C++ Build Tools 2015, fornecido gratuitamente pela Microsoft. Essas ferramentas são necessárias para compilar módulos nativos populares. Ele também instalará o Python 2.7, configurando sua máquina e npm adequadamente.

Se sua instalação do `windows-build-tools` trava após a conclusão do Visual Studio Build Tools, [esta solução](https://github.com/felixrieseberg/windows-build-tools/issues/47#issuecomment-296881488) pode ajudar.

### Se `npm install` continua falhando...

Às vezes, o `windows-build-tools` não instala corretamente as
bibliotecas. Isso é verdade se você já possui um ambiente de desenvolvimento .NET
apropriado. Isso foi relatado no Windows 10 x64 (e possivelmente em outras
arquiteturas ou versões do Windows).

Esse pode ser o seu problema se, depois de executar o `npm install` em um site do Gatsby, você tenha visto erros de compilação como `node-gyp` ou` sharp` ou `binding.gyp not found`.

Se você suspeitar que este é seu problema, baixe o
[Pacote da Comunidade do Visual Studio 2015](https://www.visualstudio.com/vs/older-downloads/) (também disponível neste [link de download direto](https://go.microsoft.com/fwlink/?LinkId=532606&clcid=0x409))
e instale apenas a parte do pacote que nos interessa: `Linguagens de programação> Visual C ++ > Ferramentas comuns para o Visual Studio 2015`. Tenha certeza de
fazer o download da versão 2015 da Comunidade VS. Para o Visual Studio 2017, consulte as instruções abaixo. Você pode desmarcar todo o resto. Você não precisa instalar o pacote completo VS2015 Express no seu sistema e isso não atrapalhará a instalação existente do VS201x.

![Ferramentas comuns para o Visual Studio 2015 dentro do pacote da comunidade VS 2015](https://i.stack.imgur.com/J1aet.png)

Em seguida, execute os comandos no Gatsby:

```powershell
npm uninstall node-gyp -g
npm config set python python2.7
npm config set msvs_version 2015
npm cache clean -f
npm install
```

Para o Visual Studio 2017, baixe [Visual Studio Community 2017](https://visualstudio.microsoft.com/vs/community/) e instale o _Desktop Development with C++ workflow_. Você pode desmarcar todo o resto.

![Desktop Development with C++ workflow.](https://i.imgur.com/dPknorD.png)

Caso você já tenha instalado o Visual Studio 2017, execute o Instalador do Visual Studio.

![Instalador do Visual Studio](https://i.imgur.com/H5PVEbu.png)

Na lista de produtos, selecione o menu suspenso "Mais" ao lado do Visual Studio 2017 e selecione a opção Modificar. Na próxima tela, selecione o _Desktop Development with C++ workflow_.

![Instalador do Visual Studio](https://i.imgur.com/7SFsS99.png)

Em seguida, execute os comandos no Gatsby:

```powershell
npm uninstall node-gyp -g
npm config set python python2.7
npm config set msvs_version 2017
npm cache clean -f
npm install
```

Você deve estar com tudo pronto.

Se isso ainda não funcionar, consulte a
[página inicial do pacote`node-gyp` npm](https://www.npmjs.com/package/node-gyp) para
instruções adicionais e entre em contato com a equipe `node-gyp` em
[GitHub](https://github.com/nodejs/node-gyp/issues).

## gatsby-plugin-sharp precisa do Node x64

Alguns plugins que dependem de dependências nativas do NPM requerem a compilação Node x64 do Node.js. Se você estiver com dificuldades para instalar o gatsby-plugin-sharp, tente instalar o Node x64 e remover o `node_modules` e executar o` npm install`.

## gatsby-plugin-sharp requer libvips

Sharp usa uma biblioteca C, libvips. Se você estiver tendo problemas ao instalar o Sharp, tente remover `C:\Users\[usuário]\AppData\Roaming\npm-cache\_libvips`.

## Subsistema do Windows para Linux

Se a instalação de dependências ou o desenvolvimento no Windows em geral causar dores de cabeça, o Windows 10 oferece uma ótima alternativa: [Subsistema do Windows para Linux](https://docs.microsoft.com/en-us/windows/wsl/about). Permite executar a maioria das ferramentas, utilitários e aplicativos de linha de comando em um ambiente GNU/Linux diretamente no Windows, sem modificação, sem a sobrecarga de uma máquina virtual. No cenário acima, você faria o download, por exemplo. Ubuntu, abra o terminal, [instale o Node](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions) e execute `sudo apt-get install build -essencial` no terminal - e a compilação funciona de forma muito mais confiável. Observe que você deve excluir qualquer pasta `node_modules` existente no seu projeto e reinstalar as dependências no seu ambiente WSL.

Você também pode visitar o [Gatsby no Linux](/docs/gatsby-on-linux/) para saber mais.
