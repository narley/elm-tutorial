> Esta página cobre o Tutorial v2. Elm 0.18.

# Back-end

Vamos precisar de um backend para nossa aplicação, podemos usar o __json-server__ para isso.

[json-server](https://github.com/typicode/json-server) é um pacote npm que fornece uma maneira rápida de criar APIs falsas.

Inicie um novo projeto de Node:

```bash
yarn init
```

Aceite todos os padrões.

Instale o __json-server__ :

```bash
yarn add json-server@0.9.5
```

Crie __api.js__ na raiz do projeto:

```js
var jsonServer = require('json-server')

// Retorna um servidor Express
var server = jsonServer.create()

// Define um middlewares padrao (logger, static, cors e no-cache)
server.use(jsonServer.defaults())

var router = jsonServer.router('db.json')
server.use(router)

console.log('Listening at 4000')
server.listen(4000)
```

Crie __db.json__ na raiz:

```json
{
  "players": [
    { "id": "1", "name": "Sally", "level": 2 },
    { "id": "2", "name": "Lance", "level": 1 },
    { "id": "3", "name": "Aki", "level": 3 },
    { "id": "4", "name": "Maria", "level": 4 },
    { "id": "5", "name": "Julian", "level": 1 },
    { "id": "6", "name": "Jaime", "level": 1 }
  ]
}
```

Inicie o servidor executando:

```bash
node api.js
```

Teste esta API falsa acessando:

- <http://localhost:4000/players>
