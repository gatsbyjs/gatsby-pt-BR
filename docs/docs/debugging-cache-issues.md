---
title: Depurando Problemas de Cache
---

Pode haver certas situações nas quais o mecanismo de cache do Gatsby parece falhar, o que pode levar a problemas como:

- Conteúdo não aparecendo quando deveria
- Alterações no código do plugin nativo que não parecem ser chamadas adequadamente

e mais! Se você se perceber escrevendo um script da seguinte forma:

```json:title=package.json
{
  "scripts": {
    "clean": "rm -rf .cache"
  }
}
```

considere usar o comando `gatsby clean` que pode ajudar a resolver os seus problemas de cache.

Primeiro certifique-se que a versão do `gatsby` especificada nas dependências do seu `package.json` é _no mínimo_ a `2.1.1`, e então faça a seguinte alteração no `package.json`:

```json:title=package.json
{
  "scripts": {
    "clean": "gatsby clean"
  }
}
```

Agora, quando surgirem problemas relacionados a cache, você pode usar `npm run clean` para limpar o cache e começar do zero.

_Observação: Se você perceber que está usando o comando constantemente, considere nos ajudar [respondendo nosso Github Issue][github-issue] com uma descrição clara de como reproduzir o problema._

[github-issue]: https://github.com/gatsbyjs/gatsby/issues/11747
