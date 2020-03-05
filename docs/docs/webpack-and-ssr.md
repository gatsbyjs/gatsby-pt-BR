---
title: Webpack e SSR
---

O bootstrap está concluído! E nós [salvamos as páginas resultantes](/docs/write-pages/) em disco. O próximo passo é renderizar cada página em HTML. Além disso, precisamos criar um tempo de execução JavaScript que assuma o controle assim que o HTML for carregado, para que as futuras navegações da página sejam carregadas instantaneamente.

Os próximos estágios da construção dependem fortemente do webpack para otimização e divisão de código. Se você ainda não o fez, vale a pena mergulhar nos [documentos do webpack](https://webpack.js.org/guides/) para saber como funciona.

## /.cache/

Todos os arquivos exigidos pelo webpack estão no diretório `.cache` do seu site. Isso fica vazio quando você inicializa um novo projeto e pode ser excluído com segurança. Gatsby cria e preenche ao longo de uma compilação.

No início da compilação, o Gatsby [copia todos os arquivos](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/bootstrap/index.js#L191) em [gatsby/cache-dir](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby/cache-dir) no diretório `.cache`. Isso inclui coisas como [static-entry.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/cache-dir/static-entry.js) e [production-app.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/cache-dir/production-app.js) sobre o qual você lerá nas próximas seções. Essencialmente, todos os arquivos necessários ao Gatsby para serem executados no navegador ou para gerar HTML estão incluídos no `cache-dir`.

Como o Webpack não conhece o Redux, também precisamos criar arquivos que contenham todos os dados da página, criados durante a inicialização. E todos esses itens também precisam ser colocados no `.cache`. É com isso que a seção anterior [Salvar Páginas](/docs/write-pages/) tratou.

