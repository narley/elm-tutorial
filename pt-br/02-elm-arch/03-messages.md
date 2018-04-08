> Esta página cobre Elm 0.18

# Mensagens

Na última seção, criamos um aplicativo usando o Html.program que era apenas Html estático. Agora vamos criar um aplicativo que responda à interação do usuário usando mensagens.

Agora, edite seu arquivo **App.elm** ou crie um novo (lembre-se de dar ao módulo o mesmo nome que o seu arquivo possui):

```elm
module App exposing (..)

import Html exposing (Html, button, div, text, program)
import Html.Events exposing (onClick)


-- MODEL


type alias Model =
    Bool


init : ( Model, Cmd Msg )
init =
    ( False, Cmd.none )



-- MESSAGES


type Msg
    = Expand
    | Collapse



-- VIEW


view : Model -> Html Msg
view model =
    if model then
        div []
            [ button [ onClick Collapse ] [ text "Collapse" ]
            , text "Widget"
            ]
    else
        div []
            [ button [ onClick Expand ] [ text "Expand" ] ]



-- UPDATE


update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        Expand ->
            ( True, Cmd.none )

        Collapse ->
            ( False, Cmd.none )



-- SUBSCRIPTIONS


subscriptions : Model -> Sub Msg
subscriptions model =
    Sub.none



-- MAIN


main =
    program
        { init = init
        , view = view
        , update = update
        , subscriptions = subscriptions
        }
```

Este programa é muito semelhante ao programa anterior que fizemos, mas agora temos duas mensagens: `Expand` e `Collapse`. Você pode rodar este programa copiando-o em um arquivo e abrindo-o usando o Elm reactor.

Vamos olhar mais de perto as funções `view` e `update`.

### View

```elm
view : Model -> Html Msg
view model =
    if model then
        div []
            [ button [ onClick Collapse ] [ text "Collapse" ]
            , text "Widget"
            ]
    else
        div []
            [ button [ onClick Expand ] [ text "Expand" ] ]
```

Dependendo do estado do modelo, mostramos a view recolhida ou expandida.

Observe a função `onClick`. Como essa view é do tipo `Html Msg`, podemos acionar mensagens desse tipo usando `onClick`. Recolher e expandir são do tipo `Msg`.

### Update

```elm
update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        Expand ->
            ( True, Cmd.none )

        Collapse ->
            ( False, Cmd.none )
```

`update` responde às possíveis mensagens. Dependendo da mensagem, retorna o estado desejado. Quando a mensagem é `Expand`, o novo estado será `True`(expandido).

Em seguida, vamos ver como o __Html.program__ orquestra essas partes juntas.
