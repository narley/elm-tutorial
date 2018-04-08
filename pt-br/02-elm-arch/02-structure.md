> Esta página cobre Elm 0,18

# Estrutura do Html.program

### Importações (import)

```elm
import Html exposing (Html, div, text, program)
```

- Nós usaremos o tipo `Html` do módulo `Html`, além de algumas funções `div`, `text` e `program`.

### Modelo (Model)

```elm
type alias Model =
    String


init : ( Model, Cmd Msg )
init =
    ( "Hello", Cmd.none )
```

- Primeiro, definimos nosso modelo do aplicativo como um type alias do tipo `String`.
- Depois nós definimos uma função `init`. Esta função fornece o dado inicial para o aplicativo.

__Html.program__ espera uma tupla com `(model, command)`. O primeiro elemento desta tupla é o nosso estado inicial, por exemplo, "Hello". O segundo elemento é um comando inicial a ser executado. Mais sobre comandos depois.

Ao usar a arquitetura elm, compomos todos os componentes de modelos em uma única árvore de estados. Mais sobre isso mais tarde também.

### Mensagens (Msg)

```elm
type Msg
    = NoOp
```

Mensagens são coisas que acontecem em nossos aplicativos aos quais nosso componente responde. Neste caso, o aplicativo não faz nada, por isso só temos uma mensagem chamada `NoOp`.

Outros exemplos de mensagens podem ser `Expand` ou `Collapse` para mostrar e ocultar um widget. Usamos union types para mensagens:

```elm
type Msg
    = Expand
    | Collapse
```

### Visão (View)

```elm
view : Model -> Html Msg
view model =
    div []
        [ text model ]
```

A função `view` renderiza um elemento Html usando nosso modelo do aplicativo. Observe que a assinatura do tipo é `Html Msg`. Isso significa que esse elemento Html pode produzir mensagens marcadas com Msg. Nós veremos isso quando introduzirmos interações.

### Atualização (Update)

```elm
update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        NoOp ->
            ( model, Cmd.none )
```

Depois definimos uma função `update`, esta função será chamada pelo `Html.program` cada vez que uma mensagem é recebida. Esta função de atualização responde às mensagens(Msg) atualizando o modelo(Model) e retornando comandos(Cmd) conforme necessário.

Neste exemplo, apenas respondemos `NoOp` e retornamos o modelo inalterado e `Cmd.none` (ou seja, nenhum comando para executar).

### Assinaturas (Subscriptions)

```elm
subscriptions : Model -> Sub Msg
subscriptions model =
    Sub.none
```

Usamos assinaturas para escutar atividates externa que chegam em nosso aplicativo. Alguns exemplos de assinaturas são:

- Movimentos do mouse
- Eventos de teclado
- Alterações na localização do navegador

No exemplo acima não estamos interessados ​​em nenhuma atividade externa, portanto, usamos `Sub.none`.

### Função Principal (Main)

```elm
main : Program Never Model Msg
main =
    program
        { init = init
        , view = view
        , update = update
        , subscriptions = subscriptions
        }
```

Finalmente, `Html.program` liga tudo e retorna um elemento html que podemos renderizar na página. `program` recebe as nossas funções `init`, `view`, `update` e `subscriptions`.
