# Mais sobre funções

## Tipo Variável (Type Variable)

Considere uma função com uma assinatura de tipo como:

```elm
indexOf : String -> List String -> Int
```

Esta função hipotética pega uma string e uma lista de strings e retorna o índice onde a string foi encontrada na lista ou -1 se não for encontrada.

Mas se, em vez disso, tivermos uma lista de inteiros? Nós não poderíamos usar essa função. No entanto, podemos fazer esta função __genérica__ , utilizando __tipo variável__ ou __stand-ins__ em vez de tipos específicos.

```elm
indexOf : a -> List a -> Int
```

Substituindo `String` por `a`, a assinatura agora diz que `indexOf` assume um valor de qualquer tipo `a` e uma lista desse mesmo tipo `a` e retorna um inteiro. Contanto que os tipos coincidam, o compilador ficará feliz. Você pode chamar `indexOf` com um `String` e uma lista de `String`, ou uma `Int` e uma lista `Int`, e isso funcionará.

Desta forma, as funções podem ser mais genéricas. Você pode ter várias __tipo variável ​​de tipo__ também:

```elm
switch : ( a, b ) -> ( b, a )
switch ( x, y ) =
  ( y, x )
```

Esta função recebe uma tupla de tipos `a`, `b` e retorna uma tupla de tipos `b`, `a`. Todas estas são chamadas válidas:

```elm
switch (1, 2)
switch ("A", 2)
switch (1, ["B"])
```

Observe que qualquer identificador de letras minúsculas pode ser usado para tipo variável, `a` e `b` são apenas uma convenção comum. Por exemplo, a seguinte assinatura é perfeitamente válida:

```
indexOf : thing -> List thing -> Int
```

## Funções como argumentos

Considere esta assinatura:

```elm
map : (Int -> String) -> List Int -> List String
```

Esta função:

- recebe uma função: a `(Int -> String)` parte
- uma lista de inteiros
- e retorna uma lista de strings

A parte interessante é o fragmento `(Int -> String)`. Isto diz que uma função deve ser dada em conformidade com a assinatura de `(Int -> String)`.

Por exemplo, `toString` (da biblioteca central) tem esta assinatura. Então você poderia chamar essa função `map` como:

```elm
map toString [1, 2, 3]
```

Mas `Int` e `String` são tipos muito específicos. Então, na maior parte do tempo, você verá assinaturas usando stand-ins (variáveis de tipo):

```elm
map : (a -> b) -> List a -> List b
```

Esta função mapeia uma lista `a` para uma lista de `b`. Nós não nos importamos com o que `a` e `b` representam desde que a função dada no primeiro argumento use os mesmos tipos.

Por exemplo, dadas funções com estas assinaturas:

```elm
convertStringToInt : String -> Int
convertIntToString : Int -> String
convertBoolToInt : Bool -> Int
```

Podemos chamar o `map` genérico como:

```elm
map convertStringToInt ["Hello", "1"]
map convertIntToString [1, 2]
map convertBoolToInt [True, False]
```
