> Esta página cobre o Tutorial v2. Elm 0.18.

# Webpack 2

## index.html

Como não estamos mais usando o __Elm reactor__, precisaremos criar nosso próprio HTML para conter o aplicativo. Crie __src/index.html__ :

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Elm SPA example</title>
  </head>
  <body>
    <div id="main"></div>
    <script src="/app.js"></script>
  </body>
</html>
```

## index.js

Este é o ponto de entrada que o Webpack irá procurar ao criar o pacote. Adicione __src/index.js__ :

```js
'use strict';

require('ace-css/css/ace.css');
require('font-awesome/css/font-awesome.css');

// Importa index.html para que possa ser copiado ao dist
require('./index.html');

var Elm = require('./Main.elm');
var mountNode = document.getElementById('main');

// .embed() pode receber um segundo argumento opcional. Este argumento pode ser um objecto descrevendo os dados que precisaremos para iniciar o programa, por exemplo, um userID ou algum token
var app = Elm.Main.embed(mountNode);
```

## Instalar pacotes Elm

Execute:

```bash
elm-package install elm-lang/html
```

Depois de fazer isso, deve haver um arquivo chamado __elm-package.json__ na raiz do seu projeto.

## Diretório src

Nós estaremos adicionando todo o nosso código-fonte na pasta `src`, então precisamos informar ao Elm onde procurar por dependências. No arquivo __elm-package.json__ faça a seguinte mudança:

```json
...
"source-directories": [
    "src"
],
...
```

Sem isso, o compilador Elm tentará encontrar as importações na raiz do nosso projeto e falhará.
