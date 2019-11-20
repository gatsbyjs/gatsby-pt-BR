---
title: Como escrever um esboço
---

Ás vezes você pode ter uma ideia para uma página da documentação do Gatsby.js ou concordar com uma sugestão para um problema no GitHub, mas você não tem tempo ou recursos para escrever essa página. Ao invés de deixar sua ideia sumir no espaço, considere **criar um esboço de documentação** para servir como um inicio de conteúdo. Dessa maneira, outros membros da comunidade (e/ou você, no futuro) podem retornar a este esboço e preenchê-lo com detalhes.

Um **esboço** é um espaço temporário reservado na documentação do Gatsby.js atrelado a uma issue no GitHub, usando este formato (sinta-se livre para copiar e colar, mudando o título e número da issue):

```markdown:title=how-to-tame-dragons.md
---
title: How to Tame Dragons
issue: https://github.com/gatsbyjs/gatsby/issues/XXXX
---

Este é um esboço. Ajude nossa comunidade a expandi-lo.

Por favor use o [Guia de Estilo do Gatsby](/contributing/gatsby-style-guide/) para garantir que sua pull request será aceita.
```
Se você tiver qualquer pergunta sobre títulos ou outros detalhes relacionados a criação de esboços, sinta-se livre para nos perguntar em uma issue relevante do GitHub.

## Sessões de Programação Conjunta da Comunidade

Se você criou ou viu um esboço no Gatsby.js e sentiu-se interessado em adicionar o conteúdo, verifique o [Programa de Programação em Conjunto](/contributing/pair-programming/) do Gatsby.js. Nós adoraremos trabalhar com você em nossa jornada de contribuição para o open source.

## Convertendo um Esboço para uma Documentação

Para converter um esboço em uma documentação real, remova a palavra `issue` do frontmatter (palavra chique para dados Markdown) do esboço e substitua o modelo de conteúdo inicial com o seu texto e código. Salve o arquivo, commit no GitHub, abra um PR, receba comentários. Aprenda mais em nossa página sobre [contribuições com documentação](/contributing/docs-contributions/).

Se você deseja ver os esboços disponíveis, confira nossa [lista de esboços](/contributing/stub-list/).
