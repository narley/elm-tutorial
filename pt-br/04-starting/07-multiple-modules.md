> Esta página cobre o Tutorial v2. Elm 0.18.

# Vários módulos

Nosso aplicativo está crescendo, portanto, manter as coisas em um arquivo rapidamente se torna difícil de manter.

### Dependências circulares

Outra questão que provavelmente chegaremos em algum momento serão as dependências circulares. Por exemplo, podemos ter:

- Um `Main` módulo que tem um tipo `Player` nele.
- Um módulo `View` que importa o tipo `Player` declarado em `Main`.
- `Main` importando `View` para renderizar a tela.

Agora temos uma dependência circular:

```elm
Main --> View
View --> Main
```

#### Como acabar com isso?

Nesse caso, precisamos remover o tipo `Player` de `Main` e coloar num local onde ele pode ser importado por ambos `Main` e `View`.

Para lidar com dependências circulares em Elm, o mais fácil é dividir seu aplicativo em módulos menores. Neste exemplo em particular, podemos criar outro módulo que pode ser importado por ambos `Main` e `View`. Nós teremos três módulos:

- Main
- View
- Models (contém o tipo Player)

Agora as dependências serão:

```elm
Main --> Models
View --> Models
```

Não há mais dependência circular.

Tente criar módulos separados para coisas como __messages__ , __models__ , __commands__ e __utilities__ , que são módulos que geralmente são importados por muitos componentes.

---

Vamos dividir o aplicativo em módulos menores:

Primeiro, verifique seu elm-package.json. Certifique-se de `"source-directories"` apontar para o diretório onde nossos novos módulos estão. Neste exemplo, será o diretório src.

```json
    "source-directories": [
        "src"
    ],
```
Agora estamos prontos para criar os módulos

__src / Msgs.elm__

```elm
module Msgs exposing (..)


type Msg
    = NoOp
```

__src/Models.elm__

```elm
module Models exposing (..)


type alias Model =
    String
```

__src/Update.elm__

```elm
module Update exposing (..)

import Msgs exposing (Msg(..))
import Models exposing (Model)


update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        NoOp ->
            ( model, Cmd.none )
```

__src/View.elm__

```elm
module View exposing (..)

import Html exposing (Html, div, text)
import Msgs exposing (Msg)
import Models exposing (Model)


view : Model -> Html Msg
view model =
    div []
        [ text model ]
```

__src/Main.elm__

```elm
module Main exposing (..)

import Html exposing (program)
import Msgs exposing (Msg)
import Models exposing (Model)
import Update exposing (update)
import View exposing (view)


init : ( Model, Cmd Msg )
init =
    ( "Hello", Cmd.none )


subscriptions : Model -> Sub Msg
subscriptions model =
    Sub.none



-- MAIN


main : Program Never Model Msg
main =
    program
        { init = init
        , view = view
        , update = update
        , subscriptions = subscriptions
        }
```

Você pode encontrar o código aqui <https://github.com/sporto/elm-tutorial-app/tree/018-v02-03-multiple-modules>.

---

Existem varios módulos pequenos agora, o que é um exagero para uma aplicação trivial. Mas, para um aplicação maior, a utilização de módulos torna-se essencial.
