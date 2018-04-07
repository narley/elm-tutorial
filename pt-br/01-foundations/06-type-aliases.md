# Type aliases(pseudônimo)

Um __type alias__ em Elm é, como o próprio nome diz, um pseudônimo para alguma outra coisa. Por exemplo, em Elm você tem os tipos `Int` e `String`. Você pode criar pseudônimo para eles:

```elm
type alias PlayerId = Int

type alias PlayerName = String
```

Aqui nós criamos um par de type alias que simplesmente apontam para outros tipos. Isso é útil porque, em vez de ter uma função como:

```elm
label: Int -> String
```

Você pode escrever como:

```elm
label: PlayerId -> PlayerName
```

Desta forma, é muito mais claro o que a função está pedindo.

## Registros(Records)

Uma definição de registro em Elm se parece com:

```elm
{ id : Int
, name : String
}
```

Se você tivesse uma função que recebe um registro, você teria que escrever uma assinatura como:

```elm
label: { id : Int, name : String } -> String
```

Bastante detalhado, mas os type aliases (pseudônimo) ajudam muito com isso:

```elm
type alias Player =
    { id : Int
    , name : String
    }

label: Player -> String
```

Aqui nós criamos um type alias `Player` que aponta para uma definição de registro. Então usamos esse tipo de alias em nossa assinatura de função.

## Construtores

Type aliases(pseudônimos) podem ser usados ​​como funções construtoras . Isso significa que podemos criar um registro real usando o type alias como uma função.

```elm
type alias Player =
    { id : Int
    , name : String
    }

Player 1 "Sam"
==> { id = 1, name = "Sam" }
```

Aqui nós criamos um type alias `Player`. Então, chamamos `Player` como uma função com dois parâmetros. Isso nos retorna um registro com os atributos apropriados. Observe que a ordem dos argumentos determina quais valores serão atribuídos a quais atributos.
