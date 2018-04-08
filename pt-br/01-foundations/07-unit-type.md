## O Tipo Unit (Unit Type)

A tupla vazia `()` é chamada de __unit type__ em Elm. É tão prevalecente que merece alguma explicação.

Considere um type alias com um __tipo variável__(representado por `a`):

```elm
type alias Message a =
    { code : String
    , body : a
    }
```

Você pode criar uma função que espera um `Message` com o `body` sendo um `String` como este:

```elm
readMessage : Message String -> String
readMessage message =
    ...
```

Ou uma função que espera um `Message` com o `body` sendo uma lista de inteiros:

```elm
readMessage : Message (List Int) -> String
readMessage message =
    ...
```

E se uma função que não precisa de um valor no `body`? Usamos o tipo unit para indicar que o corpo deve estar vazio:

```elm
readMessage : Message () -> String
readMessage message =
    ...
```

Essa função recebe `Message` com um __body vazio__ . Isto não é o mesmo que __qualquer valor__ , apenas um vazio .

Portanto, o tipo unity é comumente usado como um espaço reservado para um valor vazio.

## Task

Um exemplo real disso é o tipo `Task` tipo. Ao usar `Task`, você verá o tipo unit com muita frequência.

Um task típico tem um __error__ e um __result__:

```elm
Task error result
```

- Às vezes, queremos um task em que o erro possa ser ignorado com segurança: `Task () result`
- Ou o resultado é ignorado: `Task error ()`
- Ou ambos: `Task () ()`
