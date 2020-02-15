---
title: Cache de sites estáticos
---

Uma parte importante da criação de um site muito rápido é configurar o cache HTTP adequado. O cache HTTP permite que os navegadores armazenem recursos de um site em cache, para que quando o usuário retorne a ele, poucas partes tenham que ser baixadas novamente.

Diferentes tipos de recursos são armazenados em cache de maneira diferente. Vamos analisar como os diferentes tipos de arquivos criados em `public/` devem ser armazenados em cache.

## HTML

Os arquivos HTML nunca devem ser armazenados em cache pelo navegador. Ao recriar o site do Gatsby, você geralmente atualiza o conteúdo dos arquivos HTML. Por esse motivo, os navegadores devem ser instruídos a verificar todas as solicitações, caso precisem baixar uma versão mais recente do arquivo HTML.

O cabeçalho `cache-control` deve ser `cache-control: public, max-age=0, must-revalidate`<sup>1</sup>

## Dados da página

Assim como os arquivos HTML, os arquivos JSON no diretório `public/page-data/` nunca devem ser armazenados em cache pelo navegador. De fato, é possível que esses arquivos sejam atualizados mesmo sem a reimplantação do seu site. Por esse motivo, os navegadores devem ser instruídos a verificar todas as solicitações se os dados em seu aplicativo foram alterados.

O cabeçalho `cache-control` deve ser `cache-control: public, max-age=0, must-revalidate`<sup>1</sup>

## Arquivos estáticos

Todos os arquivos em `static/` devem ser armazenados em cache para sempre. Para os arquivos deste diretório, o Gatsby cria caminhos diretamente vinculados ao conteúdo do arquivo. Significando que, se o conteúdo do arquivo for alterado, o caminho do arquivo também será alterado. Esses caminhos parecem estranhos, por exemplo. `reactnext-gatsby-performance.001-a3e9d70183ff294e097c4319d0f8cff6-0b1ba.png` mas como o mesmo arquivo sempre será retornado quando esse caminho for solicitado, o Gatsby pode armazená-lo em cache para sempre.

O cabeçalho `cache-control` deve ser `cache-control: public, max-age=31536000, immutable`

## JavaScript e CSS

Os arquivos JavaScript e CSS _gerados pelo webpack_ também devem ser armazenados em cache para sempre. Como os arquivos estáticos, o Gatsby cria nomes de arquivos JS e CSS (como um hash) Com base no conteúdo do arquivo. Se o conteúdo do arquivo for alterado, o hash do arquivo será alterado, portanto, esses arquivos _gerados pelo webpack_ são seguros para armazenar em cache.

O cabeçalho `cache-control` deve ser `cache-control: public, max-age=31536000, immutable`

A única exceção é o arquivo `/sw.js`, que precisa ser revalidado a cada carregamento para verificar se uma nova versão do site está disponível. Este arquivo é gerado pelo `gatsby-plugin-offline` e por outros plugins de profissionais para veicular o conteúdo offline. Seu cabeçalho `cache-control` deve ser `cache-control: public, max-age = 0, must-revalidate`<sup>1</sup>

## Configurando o armazenamento em cache em diferentes hospedagens

Como você configura o cache dependendo de como você hospeda seu site, nós incentivamos as pessoas a criarem plugins do Gatsby por host para automatizar a criação de cabeçalhos referentes a cache.

Os seguintes plugins já foram criados:

- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify/)
- [gatsby-plugin-s3](https://github.com/jariz/gatsby-plugin-s3)

Ao implantar com o Now, siga as instruções na [documentação do Now](https://zeit.co/guides/deploying-gatsby-with-now#bonus:-cache-your-gatsby-assets).

---

<sup>1</sup> É importante que você use a combinação de `max-age=0` e `must-revalidate` em vez de usar `no-cache`. Isso permite que o CDN armazene cópias dos arquivos nos servidores mais próximos dos usuários, e só faça o download apenas de uma nova versão do servidor de origem caso os arquivos tenham sido alterados. O uso de 'no-cache`, por outro lado, diminui o desempenho porque força o CDN a baixar uma nova cópia do arquivo do servidor de origem em cada solicitação.
