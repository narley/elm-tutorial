# Noções básicas da função

Este capítulo aborda a sintaxe básica em Elm que é importante para se familiarizar: funções, assinaturas de funções, aplicação parcial e o operador pipe.

## Funções

Elm suporta dois tipos de funções:

- funções anônimas
- funções nomeadas

## Função anônima

Uma função anônima, como o próprio nome indica, é uma função que criamos sem um nome:

```elm
\x -> x + 1

\x y -> x + y
```

Entre a contrabarra e a seta, você lista os argumentos da função e, à direita da seta, você diz o que fazer com esses argumentos.


### Funções nomeadas

Uma função nomeada em Elm se parece com isso:

```elm
addOne : Int -> Int
addOne x =
  x + 1
```

- A primeira linha no exemplo é a assinatura da função. Essa assinatura é opcional em Elm, mas recomendada porque torna a intenção da sua função mais clara.
- O resto é a implementação da função. A implementação deve seguir a assinatura definida acima.

Nesse caso, a assinatura está dizendo: Dado um inteiro (Int) como argumento, retorne outro inteiro.

Você chama a função assim:

```
addOne 3
```

Em Elm usamos *espaço em branco* para denotar a aplicação da função (em vez de usar parênteses).

Aqui está outra função nomeada:

```elm
add : Int -> Int -> Int
add x y =
  x + y
```

Esta função recebe dois argumentos (ambos Int) e retorna outro Int. Você chama essa função assim:

```elm
add 2 3
```

### Sem argumentos

Uma função que não aceita argumentos é uma constante em Elm:

```elm
name =
  "Sam"
```

### Como as funções são aplicadas

Como mostrado acima, uma função que aceita dois argumentos pode ser semelhante a:

```elm
divide : Float -> Float -> Float
divide x y =
    x / y
```

Podemos pensar nessa assinatura como uma função que pega dois floats e retorna outro float:

```elm
divide 5 2 == 2.5
```

No entanto, isso não é bem verdade, em Elm todas as funções levam exatamente um argumento e retornam um resultado. Este resultado pode ser outra função.
Vamos explicar isso usando a função acima.

```elm
-- Quando fazemos:

divide 5 2

-- Isto é avalidado como:

((divide 5) 2)

-- Primeiro `divide 5` é avaliado.
-- O argumento `5` é aplicado ao `divide`, resultando numa função intermediaria.

divide 5 -- -> função intermediaria

-- Vamos chamar esta função intermediaria `divide5`.
-- Se pudessemos ver a assinatura e corpo desta função intermediaria, se pareceria com:

divide5 : Float -> Float
divide5 y =
  5 / y

-- Entao temos uma função que ja possui `5` aplicado a ela.

-- Depois o proximo arguemnto é aplicado, por exemplo, `2`

divide5 2

-- E isto retorna o resultado final
```

A razão pela qual podemos evitar de escrever os parênteses é porque a aplicação da função se **associa à esquerda** .

### Agrupando com parênteses

Quando você quiser chamar uma função com o resultado de outra função, você precisa usar parênteses para agrupar as chamadas:

```elm
add 1 (divide 12 3)
```

Aqui, o resultado de `divide 12 3` é passado para `add` como o segundo parâmetro.

Em contraste, em muitas outras linguagens, seria escrito:

```js
add(1, divide(12, 3))
```

## Aplicação parcial

Como explicado acima, toda função leva apenas um argumento e retorna outra função ou um resultado. Isso significa que você pode chamar uma função como `add` acima com apenas um argumento, por exemplo, `add 2` e obter uma função *parcialmente aplicada* de volta.
Esta função resultante possui uma assinatura `Int -> Int`.

`add 2` retorna outra função com o valor `2` ligado como o primeiro parâmetro. Chamar a função retornada com um segundo valor retorna `2 +` o segundo valor:

```elm
add2 = add 2
add2 3 -- result 5
```

A aplicação parcial é incrivelmente útil em Elm para tornar seu código mais legível e passar dados entre funções em sua aplicação.

## O operador pipe (|>)

Como mostrado acima, você pode encaixar funções umas nas outras como:

```elm
add 1 (multiply 2 3)
```

Este é um exemplo trivial, mas considere um exemplo mais complexo:

```elm
sum (filter (isOver 100) (map getCost records))
```

Esse código é difícil de ler, porque é resolvido de dentro para fora. O operador pipe(|>) nos permite escrever essas expressões de uma maneira mais legível:

```elm
3
    |> multiply 2
    |> add 1
```

Isso depende muito da aplicação parcial, conforme explicado anteriormente. Neste exemplo, o valor `3` é passado para uma função parcialmente aplicada `multiply 2`. Seu resultado, por sua vez, é passado para outra função parcialmente aplicada `add 1`.

Usando o operador pipe(|>), o exemplo complexo acima seria escrito como:

```elm
records
    |> map getCost
    |> filter (isOver 100)
    |> sum
```
