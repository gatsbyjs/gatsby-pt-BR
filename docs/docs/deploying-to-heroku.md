---
title: Publicando para o Heroku
---

Você pode usar o [_build_ estático do heroku](https://github.com/heroku/heroku-buildpack-static) para lidar com os arquivos estáticos do seu website.

Configure o `heroku/node.js` e o `heroku-buildpack-static` _buildpacks_ na sua aplicação.

```shell
heroku buildpacks:set heroku/nodejs
heroku buildpacks:add https://github.com/heroku/heroku-buildpack-static.git
```

Opcionalmente, você pode adicionar os _buildpacks_ ao seu `app.json` se quiser tirar proveito da [API do heroku](https://devcenter.heroku.com/articles/setting-up-apps-using-the-heroku-platform-api).

```json:title=app.json
{
  "buildpacks": [
    {
      "url": "heroku/nodejs"
    },
    {
      "url": "https://github.com/heroku/heroku-buildpack-static"
    }
  ]
}
```

Heroku automaticamente detectará e executará o _script_ de _`build`_ existente no seu `package.json`, que deve se parecer com isso:

```json:title=package.json
{
  "scripts": {
    "build": "gatsby build"
  }
}
```

Por fim, adicione um arquivo `static.json` na raiz do seu projeto para definir o diretório em que os seus _assets_ ficarão. Você pode checar todas as opções de configuração deste arquivo no guia [heroku-buildpack-static](https://github.com/heroku/heroku-buildpack-static#configuration).

As seguintes configurações darão a você um bom ponto de partida de acordo com a [estratégia de _caching_ sugerida](/docs/caching/) pelo Gatsby.

```json:title=static.json
{
  "root": "public/",
  "headers": {
    "/**": {
      "Cache-Control": "public, max-age=0, must-revalidate"
    },
    "/**.css": {
      "Cache-Control": "public, max-age=31536000, immutable"
    },
    "/**.js": {
      "Cache-Control": "public, max-age=31536000, immutable"
    },
    "/static/**": {
      "Cache-Control": "public, max-age=31536000, immutable"
    },
    "/icons/*.png": {
      "Cache-Control": "public, max-age=31536000, immutable"
    }
  },
  "https_only": true,
  "error_page": "404.html"
}
```
