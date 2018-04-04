# Hello World

## Instalando Elm

Va para http://elm-lang.org/install e baixe o instalador apropriado para o seu sistema.

## Nosso primeiro aplicativo em Elm

Vamos escrever nosso primeiro aplicativo Elm. Crie uma pasta para seu aplicativo. Nesta pasta, execute o seguinte comando no terminal:

```bash
elm-package install elm-lang/html
```

Isso informará que pacotes adicionais são necessários, mostrarão o plano de upgrade proposto e solicitarão que você confirme o plano de upgrade. Se você estiver executando o elm 0.18.0, o plano de atualização incluirá os pacotes elm-lang / core, elm-lang / html e elm-lang / virtual-dom.

Isso criará um arquivo elm-package.json e um diretório elm-stuff no mesmo diretório do projeto e, em seguida, instalará os módulos especificados. Seus módulos são salvos no diretório elm-stuff , enquanto suas especificações são salvas no arquivo elm-package.json .

Adicione um arquivo `Hello.elm` com o seguinte codigo:

```elm
module Hello exposing (..)

import Html exposing (text)


main =
    text "Hello"
```

Vá para a pasta do projeto no terminal e digite:

```bash
elm reactor
```

Isso deve mostrar a você:

```
elm reactor 0.18.0
Listening on http://0.0.0.0:8000/
```

Visite `http://0.0.0.0:8000/` num navegador. E clique em `Hello.elm`. Você deve ver `Hello` no seu navegador.

Observe que você podera ver um aviso sobre uma anotação de tipo ausente para `main`. Ignore isso por enquanto, nós iremos digitar anotações depois.

Vamos rever o que está acontecendo aqui:

### Declaração do módulo

```
module Hello exposing (..)
```

Cada módulo em Elm deve iniciar com uma declaração do módulo, neste caso o nome do módulo é chamado `Hello`. É uma convenção nomear o arquivo e o módulo com mesmo nome, por exemplo, `Hello.elm` contém `module Hello`.

A parte `exposing (..)` da declaração especifica quais funções e tipos esse módulo expõe aos outros módulos que importam isso. Neste caso, expomos tudo `(..)`.

### Importações

```
import Html exposing (text)
```

Em Elm, você precisa importar os __módulos__ que deseja usar explicitamente. Neste caso, queremos usar o módulo __Html__ .

Este módulo tem muitas funções para trabalhar com html. Nós estaremos usando `.text`, assim nós importamos esta função no namespace atual usando `exposing`.

### Main

```
main =
    text "Hello"
```

Aplicações front end em Elm começam em uma função chamada `main`. `main` é uma função que retorna um elemento para renderizar na página. Neste caso, ela retorna um elemento Html (criado usando `text`).

### Elm reactor

Elm __reactor__ cria um servidor que compila o código Elm em tempo real. __reactor__ é útil para desenvolver aplicativos sem se preocupar muito com a configuração de um processo de construção (build process). No entanto __reactor__ tem limitações, por isso, será necessário mudar para um processo de construção mais tarde.
