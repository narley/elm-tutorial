# Union types

Em Elm, os Union Types são usados ​​para muitas coisas, pois são incrivelmente flexíveis. Eles também são chamados de Tipos de Dados Algébricos (muitas vezes referidos pela sigla ADTs, do ingles Algebric Data Types) em outras linguagens. Um union type simples se parece com:

```elm
type Answer = Yes | No
```

O tipo `Answer` pode ser tanto `Yes` ou `No`.

## Tipo e Construtores

Um union type tem os seguintes componentes:

```elm
type State = Pending | Done | Failed
    ^----^   ^---------------------^
     type        constructors
```

Neste exemplo `State` é o `tipo`. E `Pending, Done and Failed` são construtores. Eles são chamados de construtores porque você constrói uma nova instância desse tipo usando-os. por exemplo

```elm
pendingState = Pending
```

## Examplo

Por exemplo, uma função que possui essa assinatura:

```elm
respond : Answer -> String
```

Pode receber `Yes` ou `No` como o primeiro argumento, por exemplo, `respond Yes` é uma chamada válida.

```
respond : Answer -> String
respond answer =
    case answer of
      Yes ->
        ...
      No ->
        ...
```

## Payload (Informações Associadas)

Os union types podem ter informações associadas a eles:

```elm
type Answer = Yes | No | Other String
```

Nesse caso, a tag `Other` terá uma string associada. Você pode chamar `respond` assim:

```elm
respond (Other "Hello")
```

Você precisa do parêntese, caso contrário Elm interpretará isso como passando dois argumentos para `respond`.

## Usado como funções

Observe como adicionamos um payload a `Other`:

```elm
Other "Hello"
```

Isto é como uma chamada de função onde `Other` é a função. Union types se comportam como funções. Por exemplo, dado um tipo:

```elm
type Answer = Message Int String
```

Você criará uma instância de `Message` desta maneira:

```elm
Message 1 "Hello"
```
Você pode fazer aplicações parciais como qualquer outra função.

## Aninhamento

É muito comum "aninhar" um tipo de união em outro.

```elm
type OtherAnswer = DontKnow | Perhaps | Undecided

type Answer = Yes | No | Other OtherAnswer
```

Depois você pode passar isso para a nossa função `respond` (que espera `Answer`) assim:

```elm
respond (Other Perhaps)
```

## Tipo Variável

Também é possível usar tipo variável ou stand-ins:

```elm
type Answer a = Yes | No | Other a
```
Este é um `Answer` que pode ser usado com diferentes tipos, por exemplo, Int, String.

Por exemplo, `respond` poderia ser assim:

```elm
respond : Answer Int -> String
respond answer =
    ...
```

Aqui estamos dizendo que o tipo variável `a` deve ser do tipo `Int` de acordo com a assinatura `Answer Int`.

Então, mais tarde, poderemos chamar `respond` com:

```elm
respond (Other 123)
```

Mas `respond (Other "Hello")` ira falhar porque `respond` espera um inteiro no lugar de `a`.

## Uso comum

Um uso típico de union types é passar valores em nosso programa, onde o valor pode ser um de um conjunto conhecido de valores possíveis.

Por exemplo, em um aplicativo da Web típico, podemos acionar mensagens para executar ações, por exemplo, carregar usuários, adicionar usuário, excluir usuário etc. Algumas dessas mensagens teriam um payload.

É comum usar union types para isso:

```elm
type Msg
    = LoadUsers
    | AddUser
    | EditUser UserId
    ...
```

## Alguns union types comuns

Existem alguns union types em Elm que você verá com muita frequência.

```
type Bool = True | False
```

Não há booleano em Elm, é apenas um union type.

```
type Maybe a
    = Nothing
    | Just a
```

`Maybe` representa a possibilidade de ter nada ou alguma coisa.

```
type Result error value
    = Ok value
    | Err error
```

`Result` representa a possibilidade de ter dois resultados de uma operação. `Ok` com o valor associado e `Err` com o erro associado.

---

Há muito mais sobre os Union Types. Se interessado, leia mais sobre eles [aqui](http://elm-lang.org/guide/model-the-problem).
