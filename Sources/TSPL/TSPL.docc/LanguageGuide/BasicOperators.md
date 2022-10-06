

# Operadores básicos

Um operador é um símbolo ou frase que você pode usar para verificar, mudar ou combinar valores.
Por exemplo, o operador de adição (`+`) soma dois números,
como em `let i = 1 + 2`,
e o operador lógico E (*AND* - `&&`) combina dois valores booleanos,
como em `if enteredDoorCode && passedRetinaScan`.

Swift suporta os operadores que você já conhece de linguagens como C,
e melhora vários recursos para eliminar erros comuns de codificação.
O operador de atribuição (`=`) não retorna um valor,
para evitar que seja usado erroneamente quando
o operador igual a (`==`) é pretendido.
Operadores aritméticos (`+`, `-`, `*`, `/`, `%` e assim por diante)
detectam e desabilitam estouros de valor,
para evitar resultados inesperados quando estamos trabalhando com números que se tornam muito maiores ou muito menores do que o intervalo permitido nos tipos que os armazenam.
Você pode ativar o comportamento de estouro de valor
usando os operadores de estouro do Swift,
conforme descrito em <doc:OperadoresAvançados#Operadores-de-estouro>.

Swift também fornece operadores de intervalo que não são encontrados em C,
como `a..<b` e `a...b`, como um atalho para expressar um intervalo de valores.
Este capítulo descreve os operadores comuns em Swift.
<doc:OperadoresAvançados> abrange os operadores avançados do Swift,
e descreve como definir seus próprios operadores personalizados
e implementar os operadores padrão para seus próprios tipos personalizados.

## Terminology

Operators are unary, binary, or ternary:

- *Unary* operators operate on a single target (such as `-a`).
  Unary *prefix* operators appear immediately before their target (such as `!b`),
  and unary *postfix* operators appear immediately after their target (such as `c!`).
- *Binary* operators operate on two targets (such as `2 + 3`)
  and are *infix* because they appear in between their two targets.
- *Ternary* operators operate on three targets.
  Like C, Swift has only one ternary operator,
  the ternary conditional operator (`a ? b : c`).

The values that operators affect are *operands*.
In the expression `1 + 2`, the `+` symbol is an infix operator
and its two operands are the values `1` and `2`.

## Assignment Operator

The *assignment operator* (`a = b`)
initializes or updates the value of `a` with the value of `b`:

```swift
let b = 10
var a = 5
a = b
// a is now equal to 10
```




If the right side of the assignment is a tuple with multiple values,
its elements can be decomposed into multiple constants or variables at once:

```swift
let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2
```








Unlike the assignment operator in C and Objective-C,
the assignment operator in Swift doesn't itself return a value.
The following statement isn't valid:

```swift
if x = y {
   // This isn't valid, because x = y doesn't return a value.
}
```




This feature prevents the assignment operator (`=`) from being used by accident
when the equal to operator (`==`) is actually intended.
By making `if x = y` invalid,
Swift helps you to avoid these kinds of errors in your code.



## Arithmetic Operators

Swift supports the four standard *arithmetic operators* for all number types:

- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)

```swift
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0
```




Unlike the arithmetic operators in C and Objective-C,
the Swift arithmetic operators don't allow values to overflow by default.
You can opt in to value overflow behavior by using Swift's overflow operators
(such as `a &+ b`). See <doc:AdvancedOperators#Overflow-Operators>.

The addition operator is also supported for `String` concatenation:

```swift
"hello, " + "world"  // equals "hello, world"
```




### Operador de resto divisional

O *Operador de resto divisional* (`a % b`)
calcula quantos múltiplos de `b` caberão dentro de `a`
e retornará a sobra
(Conhecido como *resto*).

> Note: O operador de resto divisonal (`%`) também é conhecido como 
> *operador módulo* em outras linguagens.
> No entanto, seu comportamento em Swift para números negativos torna-o,
> estritamente falando, em um resto em vez de uma operação de módulo.



Aqui, veja como o operador de resto funciona
Para calcular `9 % 4`, você primeiro calcula quantos `4`s caberão dentro de `9`:

![](remainderInteger)


Você pode colocar dois `4`s dentro de `9`, e o restante é `1` (mostrado em laranja).

Em Swift, isso seria escrito como:

```swift
9 % 4    // equals 1
```




Para determinar a resposta para `a % b`,
o operador `%` calcula a seguinte equação
e retorna `resto` como a saída:

`a` = (`b` x `algum multiplo`) + `resto`

aonde `algum multiplo` é o maior número de múltiplos para `b`
que caberá dentro de `a`.

Colocando `9` e `4` nesta equação, produz:

`9` = (`4` x `2`) + `1`

O mesmo método é aplicado ao calcular o restante para um valor negativo de `a`:

```swift
-9 % 4   // igual -1
```




Colocando `-9` e `4` na equação, produz:

`-9` = (`4` x `-2`) + `-1`

dando um valor de resto de `-1`.

O sinal de `b` é ignorado para valores negativos de `b`.
Isso significa que `a % b` e `a % -b` sempre dão a mesma resposta.

### Operador Unário de Menos

O sinal de um valor numérico pode ser alternado usando um prefixo `-`,
conhecido como o *operador unário de menos* (`-`):

```swift
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
```




O operador unário de menos (`-`) é prefixado diretamente antes do valor em que opera,
sem nenhum espaço em branco.

### Operador unário de mais

O *operador unário de mais* (`+`) simplesmente retorna
o valor em que opera, sem qualquer alteração:

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
```




Embora o operador unário de mais (`+`) não faça nada,
você pode usá-lo para fornecer simetria em seu código para números positivos
ao usar também o operador unário de menos (`-`) para números negativos.

## Operadores de Atribuição Compostos

Assim como C, Swift fornece *operadores de atribuição compostos* que combinam atribuição (`=`) com outra operação.
Um exemplo é o *operador de atribuição de adição* (`+=`):

```swift
var a = 1
a += 2
// a is now equal to 3
```




A expressão `a += 2` é um atalho para `a = a + 2`.
Efetivamente, a adição e a atribuição são combinadas em um operador
que executa as duas tarefas ao mesmo tempo.

> Nota: Os operadores de atribuição compostos não retornam um valor.
> Por exemplo, você não pode escrever `let b = a += 2`.

Para obter informações sobre os operadores fornecidos pela biblioteca padrão Swift,
veja [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).

## Operadores de Comparação

Swift suporta os seguintes operadores de comparação:

- Igual a (`a == b`)
- Diferente de (`a != b`)
- Maior que (`a > b`)
- Menor que (`a < b`)
- Maior ou igual a (`a >= b`)
- Menor ou igual a (`a <= b`)

> Nota: Swift também fornece dois **operadores de referência** (`===` e `!==`),
> que você usa para testar se duas referências de objeto se referem à mesma instância de objeto.
> Para obter mais informações, consulte <doc:ClassesAndStructures#Identity-Operators>.

Cada um dos operadores de comparação retorna um valor `Bool` para indicar se a declaração é verdadeira ou não:

```swift
1 == 1   // true porque 1 é igual a 1
2 != 1   // true porque 2 não é igual a 1
2 > 1    // true porque 2 é maior que 1
1 < 2    // true porque 1 é menor que 2
1 >= 1   // true porque 1 é maior ou igual a 1
2 <= 1   // false porque 2 não é menor ou igual a 1
```




Operadores de comparação são frequentemente usados em declarações condicionais,
como a instrução `if`:

```swift
let name = "world"
if name == "world" {
   print("hello, world")
} else {
   print("I'm sorry \(name), but I don't recognize you")
}
// Imprime "hello, world", porque 'name' é, de fato, igual a "world".
```




Para saber mais sobre a instrução `if`, veja <doc:ControleDeFluxo>.

Você pode comparar
duas tuplas se elas tiverem o mesmo tipo e o mesmo número de valores.
As tuplas são comparadas da esquerda para a direita,
um valor de cada vez,
até que a comparação encontre dois valores
que não são iguais.
Esses dois valores são comparados,
e o resultado dessa comparação
determina o resultado geral da comparação de tuplas.
Se todos os elementos forem iguais,
então as próprias tuplas são iguais. 
Por exemplo:

```swift
(1, "zebra") < (2, "apple")   // true porque 1 é menor que 2; "zebra" e "apple" não são comparados
(3, "apple") < (3, "bird")    // true porque 3 é igual a 3 e "apple" é menor que "bird"
(4, "dog") == (4, "dog")      // true porque 4 é igual a 4 e "dog" é igual a "dog"
```


Comment {
  - test: `tuple-comparison-operators`
  
  ```swifttest
  >> let a =
  -> (1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" aren't compared
  >> let b =
  -> (3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
  >> let c =
  -> (4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
  >> print(a, b, c)
  << true true true
  ```
}

No exemplo acima,
você pode ver o comportamento de comparação da esquerda para a direita na primeira linha.
Como `1` é menor que `2`,
`(1, "zebra")` é considerado menor que `(2, "apple")`,
independentemente de quaisquer outros valores nas tuplas.
Não importa que `"zebra"` não seja menor que `"apple"`,
porque a comparação já é determinada pelos primeiros elementos das tuplas.
No entanto,
quando os primeiros elementos das tuplas são os mesmos,
seus segundos elementos **são** comparados ---
isso é o que acontece na segunda e terceira linha.

Tuplas podem ser comparadas com um determinado operador somente se o operador
pode ser aplicado a cada valor nas respectivas tuplas. Por exemplo,
conforme demonstrado no código abaixo, você pode comparar
duas tuplas do tipo `(String, Int)` porque
ambos os valores `String` e `Int` podem ser comparados
usando o operador `<`. Em contrapartida,
duas tuplas do tipo `(String, Bool)` não podem ser comparadas
com o operador `<` porque o operador `<` não pode ser aplicado a
valores `Bool`.

```swift
("blue", -1) < ("purple", 1)        // OK, avalia como true
("blue", false) < ("purple", true)  // Erro, pois < não pode ser usado para valores Booleanos

```






> Nota: A biblioteca padrão do Swift inclui operadores de comparação de tuplas
> para tuplas com menos de sete elementos.
> Para comparar tuplas com sete ou mais elementos,
> você mesmo deve implementar os operadores de comparação.



## Operador Condicional Ternário

O *operador condicional ternário* é um operador especial com três partes, no formato `question ? answer1 : answer2`. É uma abreviação para escolher uma de duas expressões baseado se `question` é verdadeiro ou falso. Se `question` for verdadeiro, ele escolhe `answer1` e retorna seu valor; caso contrário, ele escolhe `answer2` e retorna seu valor.

O operador condicional ternário é uma abreviação para o código abaixo:

```swift
if question {
   answer1
} else {
   answer2
}
```






Aqui está um exemplo, que calcula a altura da linha de uma tabela. A altura da linha deve ser 50 pontos mais alta que a altura do conteúdo se a linha tiver um cabeçalho. Caso contrário, a altura da linha deve ser 20 pontos mais alta:

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// `rowHeight` é igual a 90
```




O exemplo acima é uma abreviação para o código abaixo:

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight: Int
if hasHeader {
   rowHeight = contentHeight + 50
} else {
   rowHeight = contentHeight + 20
}
// rowHeight is equal to 90
```




O uso do operador condicional ternário no primeiro exemplo significa que `rowHeight` pode ser definido com o valor correto em uma única linha de código,
que é mais conciso que o código usado no segundo exemplo.

O operador condicional ternário fornece uma abreviação eficiente para decidir qual das duas expressões escolher. No entanto, use o operador condicional ternário com cuidado. Sua concisão pode levar a um código difícil de ler se usado em excesso. Evite combinar várias instâncias do operador condicional ternário em uma instrução composta.

## Nil-Coalescing Operator

The *nil-coalescing operator* (`a ?? b`)
unwraps an optional `a` if it contains a value,
or returns a default value `b` if `a` is `nil`.
The expression `a` is always of an optional type.
The expression `b` must match the type that's stored inside `a`.

The nil-coalescing operator is shorthand for the code below:

```swift
a != nil ? a! : b
```




The code above uses the ternary conditional operator and forced unwrapping (`a!`)
to access the value wrapped inside `a` when `a` isn't `nil`,
and to return `b` otherwise.
The nil-coalescing operator provides a more elegant way to encapsulate
this conditional checking and unwrapping in a concise and readable form.

> Note: If the value of `a` is non-`nil`,
> the value of `b` isn't evaluated.
> This is known as *short-circuit evaluation*.

The example below uses the nil-coalescing operator to choose between
a default color name and an optional user-defined color name:

```swift
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to the default of "red"
```




The `userDefinedColorName` variable is defined as an optional `String`,
with a default value of `nil`.
Because `userDefinedColorName` is of an optional type,
you can use the nil-coalescing operator to consider its value.
In the example above, the operator is used to determine
an initial value for a `String` variable called `colorNameToUse`.
Because `userDefinedColorName` is `nil`,
the expression `userDefinedColorName ?? defaultColorName` returns
the value of `defaultColorName`, or `"red"`.

If you assign a non-`nil` value to `userDefinedColorName`
and perform the nil-coalescing operator check again,
the value wrapped inside `userDefinedColorName` is used instead of the default:

```swift
userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName isn't nil, so colorNameToUse is set to "green"
```




## Range Operators

Swift includes several *range operators*,
which are shortcuts for expressing a range of values.

### Closed Range Operator

The *closed range operator* (`a...b`)
defines a range that runs from `a` to `b`,
and includes the values `a` and `b`.
The value of `a` must not be greater than `b`.







The closed range operator is useful when iterating over a range
in which you want all of the values to be used,
such as with a `for`-`in` loop:

```swift
for index in 1...5 {
   print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```




For more about `for`-`in` loops, see <doc:ControlFlow>.

### Operador de intervalo semiaberto

O *operador de intervalo semiaberto*
define o intervalo que percorre de ‘a’ até ‘b’,
mas não inclui ‘b’.
É definido como semiabeto
pois contém seu primeiro valor, mas não seu valor final.
Assim como o operador de intervalo fechado,
o valor de ‘a’ não deve ser maior que ‘b’.
Se o valor de ‘a’ é igual a ‘b’.
então o intervalo resultante será vazio.








Intervalos semiabertos são particularmente úteis quando você trabalha com
listas baseadas em zero como os _arrays_,
onde é útil contar até (mas sem incluir) o comprimento da lista:

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
   print("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```




Note que o _array_ contém quatro itens,
mas ‘0..<count’ somente conta até ‘3’
(o índice do último item no _array_),
pois é um intervalo semiaberto.
Para saber mais sobre _arrays_, veja: <doc:CollectionTypes#Arrays>.


### Intervalos unilaterais

O operador de intervalo fechado
tem uma forma alternativa para intervalos que continuam

o mais longe possível em uma direção ---
por exemplo,
um intervalo que inclui todos os elementos de um array
do index 2 até o fim do array.
Nesses casos, você pode omitir o valor
de um lado do operador de intervalo.
Esse tipo de intervalo é chamado de *intervalo unilateral* (one-sided range)
porque o operador possui valor em apenas um lado.
Por exemplo:

```swift
for name in names[2...] {
    print(name)
}
// Brian
// Jack

for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian
```




O intervalo meio-aberto também tem
uma forma unilateral que é escrita
com apenas seu valor final.
Da mesma forma que se inclui um valor em ambos os lados,
o valor final não é parte do intervalo.
Por exemplo:


```swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```




Intervalos unilaterais podem ser usados em outros contextos,
não apenas em subscritos.
Você não pode iterar sobre um intervalo unilateral
que omite o primeiro valor,
pois não é claro onde a iteração deve iniciar.
Voce *pode* iterar sobre um intervalo unilateral que omite seu valor final;
entretanto, por conta do intervalo continuar indefinidamente, 
certifique-se de adicionar uma condição explícita para finalizar o loop.
Voce pode também checar se um intervalo unilateral contém um valor particular,
como mostrado no código abaixo.


```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```




## Logical Operators

*Logical operators* modify or combine
the Boolean logic values `true` and `false`.
Swift supports the three standard logical operators found in C-based languages:

- Logical NOT (`!a`)
- Logical AND (`a && b`)
- Logical OR (`a || b`)

### Logical NOT Operator
O *operador lógico NOT* (`!a`) iverte o valor booleano para que `verdadeiro` vire `falso` e `falso` vire `verdadeiro`. 

O operador lógico NOT é um operador prefixo,
e aparece imediatamente antes do valor em que opera,
sem nenhum espaço em branco.

Ele pode ser lido como "not `a`", como no exemplo a seguir:

```swift
let allowedEntry = false
if !allowedEntry {
   print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```




A frase `if !entradaPermitida` pode ser lida como "if entrada não permitida."
A linha só é executada se "entrada não permitida" for verdadeira;
isto é, if `entradaPermitida` é `falsa`.

Como neste exemplo,
escolha cuidadosa de nomes de constantes e variáveis booleanas
pode ajudar a manter o código legível e conciso,
evitando duplas negativas ou declarações lógicas confusas.

### Operador Lógico AND

O *Operador Lógico AND* (`a && b`) cria expressões lógicas
onde ambos os valores devem ser `true` para que a expressão geral também seja `true`.

Se um dos valores for `falso`,
a expressao geral será tida como `false`.
Na verdade, se o *primeiro* valor for `falso`,
o segundo valor nem será avaliado,
porque não é possível que a expressão geral seja igual a `true`.
Isso é conhecido como *avaliação de curto-circuito*.

Este exemplo considera dois valores `Bool`
e só permite acesso se ambos os valores forem `true`:

```swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
   print("Welcome!")
} else {
   print("ACESS DENIED")
}
// Prints "ACESS DENIED"
```




### Operador Lógico OR

O *Operador Lógico OR*
(`a || b`) é um operador infixo feito de dois caracteres pipe adjacentes.
Você o usa para criar expressões lógicas nas quais
basta *um* dos dois valores deve ser `true`
para que a expressão geral seja `true`.

Como o operador lógico AND acima,
o operador lógico OR usa avaliação de curto-circuito para considerar suas expressões.
Se o lado esquerdo de uma expressão lógica OR for "true",
o lado direito não é avaliado,
porque não pode alterar o resultado da expressão geral.

No exemplo abaixo,
o primeiro valor `Bool` (`hasDoorKey`) é `false`,
mas o segundo valor (`knowsOverridePassword`) é `true`.
Como um valor é `true`,
a expressão geral também é avaliada como `true`,
e o acesso é permitido:

```swift
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "Welcome!"
```




### Combining Logical Operators

You can combine multiple logical operators to create longer compound expressions:

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "Welcome!"
```




This example uses multiple `&&` and `||` operators to create a longer compound expression.
However, the `&&` and `||` operators still operate on only two values,
so this is actually three smaller expressions chained together.
The example can be read as:

If we've entered the correct door code and passed the retina scan,
or if we have a valid door key,
or if we know the emergency override password,
then allow access.

Based on the values of `enteredDoorCode`, `passedRetinaScan`, and `hasDoorKey`,
the first two subexpressions are `false`.
However, the emergency override password is known,
so the overall compound expression still evaluates to `true`.

> Note: The Swift logical operators `&&` and `||` are left-associative,
> meaning that compound expressions with multiple logical operators
> evaluate the leftmost subexpression first.

### Explicit Parentheses

It's sometimes useful to include parentheses when they're not strictly needed,
to make the intention of a complex expression easier to read.
In the door access example above,
it's useful to add parentheses around the first part of the compound expression
to make its intent explicit:

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "Welcome!"
```




The parentheses make it clear that the first two values
are considered as part of a separate possible state in the overall logic.
The output of the compound expression doesn't change,
but the overall intention is clearer to the reader.
Readability is always preferred over brevity;
use parentheses where they help to make your intentions clear.



