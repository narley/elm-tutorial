> Esta página cobre o Tutorial v2. Elm 0.18.

# Webpack 4

## package.json

Finalmente, queremos adicionar alguns scripts npm para que possamos executar nossos servidores facilmente. Em __package.json__ adicione uma sseção `script`:

```json
{
  ...
  "scripts": {
      "api": "node api.js",
      "build": "webpack",
      "client": "webpack-dev-server --port 3000"
  },
  ...
}
```

- Então agora `yarn api` vai rodar nosso servidor falso.
- `yarn build` criará uma compilação de webpack e colocará os pacotes em `dist`.
- `yarn client` executa o servidor de desenvolvimento webpack.

## Node Foreman

Nós temos dois servidores para executar: o Api e o Frontend, nós precisaremos inicializar ambos manualmente para testar nosso aplicativo, isto é ok, mas existe uma maneira mais prática de iniciar os servidores usando um pacote chamado Foreman.

Instale o Node Foreman:

```
yarn add foreman
```

Em seguida, crie um arquivo chamado `Procfile` na raiz do projeto com:

```
api: yarn api
client: yarn client
```

Edite o __package.json__ para incluir um novo script:

```
"scripts": {
  ...,
  "start": "nf start"
}
```

## Teste

Vamos testar nossa configuração.

Em uma janela de terminal, execute:

```bash
yarn start
```

Acesse `http://localhost:3000/` e você deve ver o nosso aplicativo, que produz "Hello". Use `Ctrl-c` para parar os servidores.

O código do seu aplicativo deve ser semelhante a <https://github.com/sporto/elm-tutorial-app/tree/018-02-webpack>.
