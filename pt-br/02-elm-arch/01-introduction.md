> Esta página cobre Elm 0.18

# Introdução

Ao criar aplicativos front-end em Elm, usamos o padrão conhecido como arquitetura Elm. Esse padrão fornece uma maneira de criar componentes autônomos que podem ser reutilizados, combinados e compostos em infinitas variedades.

Elm fornece o módulo `Html` para isso. Para facilitar o entendimento, vamos crirar um pequeno aplicativo.

Instale o elm-html:

```elm
elm-package install elm-lang/html
```

Crie um arquivo chamado __App.elm__ :

```elm
module App exposing (..)

import Html exposing (Html, div, text, program)


-- MODEL


type alias Model =
    String


init : ( Model, Cmd Msg )
init =
    ( "Hello", Cmd.none )



-- MESSAGES


type Msg
    = NoOp



-- VIEW


view : Model -> Html Msg
view model =
    div []
        [ text model ]



-- UPDATE


update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        NoOp ->
            ( model, Cmd.none )



-- SUBSCRIPTIONS


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

Você pode rodar este programa executando:

```bash
elm reactor
```

E abrindo http://localhost:8000/App.elm

Este exemplo possui um monte de código para apenas mostrar "Hello", mas isso nos ajudará a entender a estrutura de aplicativos muito mais complexos em Elm.
