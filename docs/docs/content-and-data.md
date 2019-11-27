---
title: Carregando Conteúdo e Dados
---

O principal benefício em usar a técnica **"dados de qualquer lugar"**, é que ela permite que times consigam gerenciar seu conteúdo no backend que preferirem. Isso é parte do que torna o Gatsby mais poderoso que os geradores de sites estáticos que são limitados a carregar conteúdo apenas de arquivos *Markdown*.

Um benefício essencial de usar a técnica "dados de qualquer lugar", é que isso permite que times consigam gerenciar seu conteúdo no [backend](/docs/glossary/#backend) que preferirem. 

O Gatsby usa *source plugins* (plugins de fonte de dados) para trazer os dados. [Existem inúmeros plugins de fonte de dados](/plugins/?=gatsby-source) para trazer os dados de diferentes APIs, CMSs, e banco de dados. Cada plugin carrega os dados de sua fonte, significando que o plugin de fonte de dados via sistema de arquivos sabe como obter dados do sistema de arquivos, o plugin do Wordpress sabe como obter dados da API do WordPress, etc. Ao incluir múltiplos plugins, você pode obter e combinar todos esses dados em uma única camada de dados.

Bônus: leia sobre [temas Gatsby e documentos distribuídos](/blog/2019-07-03-using-themes-for-distributed-docs/) trabalhando juntos no blog do Gatsby.

_(Caso não tenha um plugin para a sua opção favorita, considere [contribuir](/docs/creating-plugins) com um!)_

<GuideList slug={props.slug} />
