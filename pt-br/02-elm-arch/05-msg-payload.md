> Esta página cobre Elm 0.18

# Mensagens com payload

Você pode enviar dados na sua mensagem:

```elm
module Main exposing (..)

import Html exposing (Html, button, div, text, program)
import Html.Events exposing (onClick)


-- MODEL


type alias Model =
    Int


init : ( Model, Cmd Msg )
init =
    ( 0, Cmd.none )



-- MESSAGES


type Msg
    = Increment Int



-- VIEW


view : Model -> Html Msg
view model =
    div []
        [ button [ onClick (Increment 2) ] [ text "+" ]
        , text (toString model)
        ]



-- UPDATE


update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        Increment howMuch ->
            ( model + howMuch, Cmd.none )



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

Perceba como a mensagem `Increment` requer um inteiro:

```elm
type Msg
    = Increment Int
```

Depois na view acionamos aquela mensagem com dados:

```elm
onClick (Increment 2)
```

E finalmente na função update usamos __pattern matching__ para extrair os dados:

```elm
update msg model =
    case msg of
        Increment howMuch ->
            ( model + howMuch, Cmd.none )
```
