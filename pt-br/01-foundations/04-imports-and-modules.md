# Importações e módulos

Em Elm você importa um módulo usando a palavra chave `import`, por exemplo

```elm
import Html
```

Este código importa o módulo `Html`. Em seguida, você pode usar funções e tipos dentro deste módulo usando seu caminho completo:

```elm
Html.div [] []
```

Você também pode importar um módulo e expor funções e tipos específicos dele:

```elm
import Html exposing (div)
```

`div` é misturado no escopo atual. Então você pode usá-lo diretamente:

```elm
div [] []
```

Você pode até mesmo expor tudo em um módulo usando (..):

```elm
import Html exposing (..)
```

Desta maneira você pode usar todas as funções e tipos deste módulo diretamente. Mas isso não é recomendado na maioria das vezes por causa de ambigüidade e possíveis conflitos entre os módulos.

## Módulos e tipos com o mesmo nome

Muitos módulos exportam tipos com o mesmo nome do módulo. Por exemplo, o módulo `Html` tem um tipo `Html` e o módulo `Task`tem um tipo `Task`.

Então esta função que retorna um elemento `Html`:

```elm
import Html

myFunction : Html.Html
myFunction =
    ...
```

É equivalente a:

```elm
import Html exposing (Html)

myFunction : Html
myFunction =
    ...
```

No primeiro bloco, apenas importamos o módulo `Html` e usamos o caminho completo `Html.Html`.

No segundo bloco, expomos o tipo `Html` do módulo `Html`. E use o tipo `Html` diretamente.

## Declarações de módulo

Quando você cria um módulo em Elm, você adiciona a declaração `module` no topo do arquivo:

```elm
module Main exposing (..)
```

`Main` é o nome do módulo. `exposing (..)` significa que você deseja expor todas as funções e tipos deste módulo. Elm espera encontrar este módulo em um arquivo chamado __Main.elm__ , ou seja, um arquivo com o mesmo nome do módulo.

Você pode ter estruturas de arquivos mais profundas em um aplicativo. Por exemplo, o arquivo __Players / Utils.elm__ deve ter a declaração:

```elm
module Players.Utils exposing (..)
```

Você poderá importar este módulo de qualquer lugar em seu aplicativo:

```elm
import Players.Utils
```
