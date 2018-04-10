> Esta página cobre Elm 0.18

# Assinaturas (subscriptions)

Em Elm, para lidar com eventos externos faz-se o uso de __subscriptions__. Alguns exemplos são:

- [Eventos de teclado](http://package.elm-lang.org/packages/elm-lang/keyboard/latest/Keyboard)
- [Movimentos do mouse](http://package.elm-lang.org/packages/elm-lang/mouse/latest/Mouse)
- Mudanças no historico do navegador
- [Eventos do Websocket](http://package.elm-lang.org/packages/elm-lang/websocket/latest/WebSocket)


Para ilustrar isso, vamos criar um aplicativo que responda a eventos de teclado e mouse.

Primeiro, instale as bibliotecas necessárias:

```bash
elm-package install elm-lang/mouse
elm-package install elm-lang/keyboard
```

Em seguida, crie este programa:

```elm
module Main exposing (..)

import Html exposing (Html, div, text, program)
import Mouse
import Keyboard


-- MODEL


type alias Model =
    Int


init : ( Model, Cmd Msg )
init =
    ( 0, Cmd.none )



-- MESSAGES


type Msg
    = MouseMsg Mouse.Position
    | KeyMsg Keyboard.KeyCode



-- VIEW


view : Model -> Html Msg
view model =
    div []
        [ text (toString model) ]



-- UPDATE


update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        MouseMsg position ->
            ( model + 1, Cmd.none )

        KeyMsg code ->
            ( model + 2, Cmd.none )



-- SUBSCRIPTIONS


subscriptions : Model -> Sub Msg
subscriptions model =
    Sub.batch
        [ Mouse.clicks MouseMsg
        , Keyboard.downs KeyMsg
        ]



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

Execute este programa com Elm reactor. Cada vez que você clicar no mouse, verá o contador aumentando em um; cada vez que você pressionar uma tecla, verá o contador aumentar em 2.

---

Vamos rever as partes importantes relevantes para assinaturas neste programa.

### Mensagens (Messages)

```elm
type Msg
    = MouseMsg Mouse.Position
    | KeyMsg Keyboard.KeyCode
```

Nós temos duas mensagens possíveis: `MouseMsg` e `KeyMsg`. Estas serão acionadas quando o mouse ou o teclado forem pressionados, de acordo.

### Atualização (Update)

```elm
update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        MouseMsg position ->
            ( model + 1, Cmd.none )

        KeyMsg code ->
            ( model + 2, Cmd.none )
```

Nossa função `update` responde a cada mensagem de maneira diferente, então adiciona 1 ao contador quando pressionamos o mouse ou adiciona 2 quando pressionamos uma tecla.

### Assinaturas (Subscriptions)

```elm
subscriptions : Model -> Sub Msg
subscriptions model =
    Sub.batch ➌
        [ Mouse.clicks MouseMsg ➊
        , Keyboard.downs KeyMsg ➋
        ]
```

Aqui nós declaramos os eventos que queremos lidar. Queremos lidar com `Mouse.clicks` ➊ e `Keyboard.downs` ➋. Ambas funções usam um construtor de mensagem e retornam uma assinatura.

Nós usamos `Sub.batch` ➌ para que possamos ouvir os dois. `batch` recebe uma lista de assinaturas e retorna uma assinatura que inclui todas elas.

Observe também que neste exemplo nossas assinaturas são estáticas, elas não mudam durante a execução da nossa aplicação. Mas elas não precisam ser assim. Eles podem mudar dependendo do que está no `model`, é por isso que nós passamos o `model`' para `subscriptions`.
