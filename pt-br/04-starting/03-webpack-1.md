> Esta página cobre o Tutorial v2. Elm 0.18.

# Webpack

__Elm reactor__ é ótimo para prototipar aplicativos simples, mas para um aplicativo maior ele fica aquém. Por enquanto o __reactor__ não suporta comunicacao com JavaScript externo ou importar CSS externo. Para superar esses problemas, usaremos o __Webpack__ para compilar nosso código Elm em vez do __Elm reactor__ .

O Webpack é um empacotador de código. Ele olha para a sua árvore de dependência e apenas empacota o código que é importado. O Webpack também pode importar CSS e outras dependencias dentro de um pacote. Leia mais sobre o Webpack [aqui](https://webpack.github.io/).

Existem muitas alternativas que você pode usar para obter o mesmo que o Webpack, por exemplo:

- [Browserify](http://browserify.org/)
- [Gulp](http://gulpjs.com/)
- [StealJS](http://stealjs.com/)
- [JSPM](http://jspm.io/)
- Ou, se estiver usando uma estrutura como Rails ou Phoenix, você pode agrupar o código Elm e o CSS usando estas estruturas.

## Requisitos

Você precisará do Node JS versão 5.1 ou superior para que essas bibliotecas funcionem conforme o esperado.

## Instalando o webpack e os carregadores

Instale o webpack e os pacotes associados:

```bash
yarn add webpack webpack-dev-server elm-webpack-loader file-loader style-loader css-loader url-loader
```

Este tutorial está usando o __webpack__ versão __2.2__ e o __elm-webpack-loader__ versão __4.2__ .

Carregadores são extensões que permitem que o webpack carregue diferentes formatos. Por exemplo, `css-loader` permite que o webpack carregue arquivos .css.

Também queremos usar algumas bibliotecas extras:

- [Basscss](http://www.basscss.com/) para CSS, `ace-css` é o pacote Npm que empacota estilos Basscss comuns
- [FontAwesome](https://fortawesome.github.io/Font-Awesome/) para ícones

```bash
yarn add ace-css@1.1 font-awesome@4
```

## Configuração do Webpack

Precisamos adicionar um __webpack.config.js__ na raiz:

```js
var path = require("path");

module.exports = {
  entry: {
    app: [
      './src/index.js'
    ]
  },

  output: {
    path: path.resolve(__dirname + '/dist'),
    filename: '[name].js',
  },

  module: {
    rules: [
      {
        test: /\.(css|scss)$/,
        use: [
          'style-loader',
          'css-loader',
        ]
      },
      {
        test:    /\.html$/,
        exclude: /node_modules/,
        loader:  'file-loader?name=[name].[ext]',
      },
      {
        test:    /\.elm$/,
        exclude: [/elm-stuff/, /node_modules/],
        loader:  'elm-webpack-loader?verbose=true&warn=true',
      },
      {
        test: /\.woff(2)?(\?v=[0-9]\.[0-9]\.[0-9])?$/,
        loader: 'url-loader?limit=10000&mimetype=application/font-woff',
      },
      {
        test: /\.(ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/,
        loader: 'file-loader',
      },
    ],

    noParse: /\.elm$/,
  },

  devServer: {
    inline: true,
    stats: { colors: true },
  },


};
```

#### Coisas para observar:

- Esta configuração cria um servidor de desenvolvimento Webpack, veja a chave `devServer`. Nós usaremos este servidor para desenvolvimento em vez do Elm reactor.
- O ponto de entrada para a nossa aplicação será `./src/index.js`, veja a chave `entry`.
