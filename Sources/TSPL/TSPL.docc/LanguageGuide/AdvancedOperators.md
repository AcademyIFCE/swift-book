

# Operadores Avançados

Além dos operadores descritos no tópico <doc:OperadoresBasicos>,
a linguagem Swift oferece o tópico Operadores Avançados que fazem manipulação de valores mais complexa. 
Lá são incluídos operadores bit a bit e operadores com deslocamento que estamos familiarizados em C e Objective-C.


Ao contrário dos operadores aritméticos em C,
os operadores aritméticos em Swift não possuem overflow por padrão.
O overflow é interceptado e relatado como um erro.
Para ativar o overflow,
use o segundo conjunto de operadores aritméticos de Swift,
como o operador de adição de overflow (`&+`).
Todos esses operadores de overflow começam com um e comercial (`&`).

Quando você define suas próprias estruturas, classes, e enumerações,
pode ser útil fornecer suas próprias implementações dos
operadores padrão do Swift para esses tipos personalizados.
O Swift facilita o fornecimento de implementações personalizadas desses operadores
e determina exatamente qual deve ser o comportamento deles para cada tipo criado.

Você não está limitado a operadores predefinidos.
A linguagem Swift dá liberdade de definir a forma como personaliza
operadores de infixo, prefixo, pós-fixo, e atribuição,
com precedência personalizada e valores associativos.
Esses operadores podem ser usados e adotados no código como qualquer um dos operadores predefinidos,
e você pode até estender os tipos existentes para suporte de operadores personalizados que você definir.

## Operadores Bit a bit

*Operadores bit a bit* permitem que você manipule 
os bits de dados brutos individuais, dentro de uma estrutura de dados.
Eles são frequentemente usados em programação de baixo-nível,
como em programação gráfica e criação de driver de dispositivo.
Operadores bit a bit podem ser úteis quando você trabalha com dados brutos para fontes externas,
como codificação e decodificação de dados para comunicação por meio de um protocolo personalizado.

O Swift suporta todos os operadores bit a bit encontrados em C, como descrito abaixo.

### Operador _Bitwise NOT_

O *operador _bitwise NOT_* (`~`) inverte todos os bits em um número:

![](bitwiseNOT)


O operador _bitwise NOT_ é um operador de pré-fixo 
e aparece imediatamente antes do valor a qual opera,
sem nenhum espaço em branco:

```swift
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits  // igual a 11110000
```




O inteiro `UInt8` tem oito bits
e cada um pode armazenar qualquer valor entre `0` e `255`.
Este exemplo inicializa um inteiro `UInt8` com o valor binário `00001111`
que tem `0` nos primeiros quatro bits,
e `1` nos seu segundo conjunto de quatro bits.
Isso equivale ao decimal de valor `15`.



O operador _bitwise NOT_ é então usado para criar uma nova constante chamada `invertedBits`,
que é igual ao `initialBits`,
mas com todos os bits invertidos.
Zeros viram uns e uns viram zeros.
O valor de `invertedBits` é `11110000`,
que equivale a um decimal não atribuido de valor `240`.

### Operador Bit a bit AND

O *operador bit a bit AND* (`&`) combina os bits de dois números. 
Ele retorna um novo número cujo os bits são definitos como  `1`
somente se os bits forem igual a `1` em ambos os numeros de entrada: 

![](bitwiseAND)

No exemplo abaixo,
os valores de `firstSixBits` e `lastSixBits`
ambos têm quatro bit no meio igual a `1`.
O operador bit a bit AND combina os dois para formar o número `00111100`,
que é igual ao decinal não atribuído de valor `60`:


```swift
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8  = 0b00111111
let middleFourBits = firstSixBits & lastSixBits  // equals 00111100
```




### Operador bit a bit OR

O *operador bit a bit OR* (`|`) compara os bits de dois números.
O operador retorna um novo número cujo os bits são definidos como  `1`
se os bits forem iguais a `1` em *nenhum* dos números de entrada. 

![](bitwiseOR)




No exemplo abaixo, 
os valores de `someBits` e `moreBits` têm diferentes bits definidos como `1`.
O operador bit a bit OR os combina para formar o número `11111110`,
que é equivalente ao decimal não atribuído de valor `254`:


```swift
let someBits: UInt8 = 0b10110010
let moreBits: UInt8 = 0b01011110
let combinedbits = someBits | moreBits  // é igual a 11111110
```




### Bitwise XOR Operator

The *bitwise XOR operator*, or “exclusive OR operator” (`^`),
compares the bits of two numbers.
The operator returns a new number whose bits are set to `1`
where the input bits are different
and are set to `0` where the input bits are the same:

![](bitwiseXOR)


In the example below,
the values of `firstBits` and `otherBits` each have a bit set to `1`
in a location that the other does not.
The bitwise XOR operator sets both of these bits to `1` in its output value.
All of the other bits in `firstBits` and `otherBits` match
and are set to `0` in the output value:

```swift
let firstBits: UInt8 = 0b00010100
let otherBits: UInt8 = 0b00000101
let outputBits = firstBits ^ otherBits  // equals 00010001
```



### Deslocamento à esquerda e à direita

O *operador com deslocamento à esquerda* (`<<`)
e o *operador com deslocamento à direita* (`>>`)
move todos os bits em um número para a esquerda ou para a direita considerando um certo número de espaços,
de acordo com as regras definidas abaixo.

Deslocamentos bit a bit à esquerda e à direita têm um efeito de
multiplicador ou divisor de um número inteiro pelo fator dois.
Deslocar bits de um inteiro à esquerda em uma posição dobra seu valor,
enquanto que deslocá-lo para a direita em uma posição reduz pela metade o seu valor.



#### Comportamento de deslocamento de bits para inteiros não sinalizados

O comportamento de descolamento de bits para inteiros não sinalizados é o seguinte:

- Bits existentes são deslocado para a esquerda ou direita pelo número de posições solicitadas.
- Quaisquer bits que são deslocamento além dos limites do armazenamento dos inteiros são descartados.
- Os zeros são inseridos em espaços deixados para trás depois que os bits originais foram deslocados para a esquerda ou direita.

Essa abordagem é conhecida como *d lógica*.

A ilustração abaixo mostra os resultados de ‘11111111 << 1’
(o qual '11111111' é movido para a direita por ‘1’ posição),
e '11111111 >> 1'
(o qual '11111111' é movido para a direita por ‘1’ posição).
Os números azuis são movidos,
os números cinzas são descartados,
e os zeros laranjas são inseridos.

![](bitshiftUnsigned)

Confira como o bit movido aparece na Swift:

'''swift
let shiftBits: UInt8 = 4   // 00000100 in binary
shiftBits << 1             // 00001000
shiftBits << 2             // 00010000
shiftBits << 5             // 10000000
shiftBits << 6             // 00000000
shiftBits >> 2             // 00000001
'''

Você pode usar o deslocamento de bit para codificar e descodificar valores com outros tipos de dados:

'''swift
let pink: UInt32 = 0xCC6699
let redComponent = (pink & 0xFF0000) >> 16    // redComponent is 0xCC, or 204
let greenComponent = (pink & 0x00FF00) >> 8   // greenComponent is 0x66, or 102
let blueComponent = pink & 0x0000FF           // blueComponent is 0x99, or 153
'''

#### Comportamento de Deslocamento para Inteiros com Sinal

O comportamento de deslocamento é mais complicado para inteiros com sinal do que para inteiros sem sinal,
por conta da maneira que são representados em modo binário.
(Os exemplos a seguir são baseados em inteiros com sinal de 8-bits para simplificar,
mas os mesmos princípios podem ser aplicados para inteiros com sinal de qualquer tamanho.)

Inteiros com sinal usam o primeiro bit (conhecido como *bit de sinal*)
para indicar que o inteiro é positivo ou negativo.
O sinal para o bit `0`siginifica positivo, e o sinal para bit `1` significa negativo. 

Os bits restantes (conhecidos como *bits de valor*) armazenam o valor atual.
Os números positivos são armazenados exatamente da mesma maneira que os inteiros sem sinal,
adicionando o `0` à posição inicial.
Veja como os bits dentro do `Int8` buscam o número `4`:


![](bitshiftSignedFour)


O bit de sinal é `0`(significa "positivo")
e os sete bits de valor são o número `4`
escrito em notação binária.

Números negativos, no entanto, são armazenados de forma diferente.
Eles são armazenados subtraindo de seu valor absoluto `2` à potência de `n`,
onde `n` é o número de bits de valor.
Um número de oito bits tem sete bits de valor,
então isso significa `2` elevado a potência `7`, ou `128`.

Veja como os bits dentro de um `Int8` buscam o número `-4`:


![](bitshiftSignedMinusFour)


Desta vez, o bit de sinal é `1` (significando “negativo”),
e os sete bits de valor têm um valor binário de `124` (que é `128 - 4`):


![](bitshiftSignedMinusFourValue)


Essa codificação para números negativos é uma representação conhecida como *complemento de dois*.
Pode parecer uma maneira incomum de representar números negativos,
mas tem várias vantagens.

Primeiro, você pode adicionar `-1` a `-4`,
simplesmente executando uma adição binária padrão de todos os oito bits
(incluindo o bit de sinal),
e descartando qualquer coisa que não se encaixe nos oito bits quando terminar:


![](bitshiftSignedAddition)

Segundo, a representação do complemento de dois também permite que você
desloque os bits de números negativos para a esquerda e para a direita como números positivos,
e ainda acabam dobrando-os para cada deslocamento que você faz para a esquerda,
ou reduzi-los pela metade para cada mudança que você faz para a direita.
Para conseguir isso, uma regra extra é usada quando os inteiros com sinal são deslocados para a direita:
Quando você desloca inteiros com sinal para a direita,
aplique as mesmas regras que para inteiros sem sinal,
mas preencha quaisquer bits vazios à esquerda com o *bit de sinal*,
ao invés de um zero.


![](bitshiftSigned)


Essa ação garante que os inteiros com sinal tenham o mesmo sinal depois de serem deslocados para a direita,
conhecido como *deslocamento aritmético*.

Por causa da maneira especial que os números positivos e negativos são armazenados,
deslocar qualquer um deles para a direita os aproxima de zero.
Manter o bit de sinal o mesmo durante este deslocamento significa que
inteiros negativos permanecem negativos à medida que seu valor se aproxima de zero.

## Overflow Operators


Se você tentar inserir um número em uma constante ou variável inteira que não pode manter esse valor,
por padrão o Swift relata um erro em vez de permitir que um valor inválido seja criado.
Este comportamento oferece segurança extra ao trabalhar com números muito grandes ou muito pequenos.

Por examplo, o tipo inteiro `Int16` pode conter qualquer inteiro assinado entre `-32768` e `32767`.
Tentando definir uma constante ou variável `Int16` para um número fora desse intervalo causa um erro:

```swift
var potentialOverflow = Int16.max
// potentialOverflow igual a 32767, que é o valor máximo que um Int16 pode manter
potentialOverflow += 1
// isso causa um erro
```




Fornecendo tratamento de erros quando os valores ficam muito grandes ou muito pequenos oferece muito mais flexibilidade quando codificar para condições de valor limite.

No entanto, quando você quer especificamente uma condição de overflow para truncar o número de bits disponíveis, você pode optar  por este comportamente em vez de desencadear um erro.
Swift fornece três *operadores de overflow* aritméticos que optam pelo comportamento de overflow para cálculos inteiros.
Todos esse operadores começam com um `e` comercial (`&`)
These operators all begin with an ampersand (`&`):

- Overflow de adição (`&+`)
- Overflow de subtração (`&-`)
- Overflow de multiplicação (`&*`)

### Valor de Overflow

Números podem transbordar tanto em direções positivas como em negativas.

Aqui está um exemplo do que acontece quando
um inteiro sem sinal é permitido estourar um sentido positivo,
usando um operador de adição de overflow.

 ('&+'):

'''swift
var unsignedOverflow = UInt8.max
// O unsignedOverflow é igual a 255, que é o valor máximo que UInt8 pode conterunsignedOverflow = unsignedOverflow &+ 1
// Agora, o unsignedOverflow é igual a 0.
'''





A variável 'unsignedOverflow' é inicializada com o valor máximo que um 'UInt8' pode conter
('255' ou '11111111' em binário).
É então incrementado por '1' usando o operador de adição de overflow('&+').
Isso empurra sua representação binária um pouco acima do tamanho que um 'UInt8' pode conter,
fazendo com que ele transborde além de seus limites,
como mostrado no diagrama abaixo.
O valor que permanece dentro dos limites do 'UInt8'
após a adição de overlow é '00000000', ou zero.

![](overflowAddition)


Algo parecido acontece quando
um inteiro sem sinal é permitido estourar em um sentido negativo.
Aqui está um exemplo usando um operador de subtração de overflow ('&-'):

'''swift
var unsignedOverflow = UInt8.min
// O unsignedOverflow é igual a 0, que é o valor mínimo que uma UInt8 pode conter
unsignedOverflow = unsignedOverflow &- 1
// Agora, o unseignedOverflow é igual a 255
'''




O valor mínimo que 'UInt8' pode conter é zero,
ou '00000000' em binário.
Se você subtrair ‘1’ de ‘00000000’ usando um operador de subtração de overflow ('&-'),
o número vai estourar e envolver com ‘11111111’
ou com ‘255’ em decimal. 

![](overflowUnsignedSubtraction)


O overflow também ocorre para inteiros com sinal.
Todas as somas e subtrações para inteiros com sinal são executadas de forma bit a bit,
com o bit de sinal incluído como parte dos números sendo adicionados ou subtraídos,
conforme descrito em <doc:AdvancedOperators#Bitwise-Left-and-Right-Shift-Operators>.

'''swift
var signedOverflow = Int8.min
// O signedOverflow é igual a -128, que é o valor mínimo que uma UInt8 pode conter
signedOverflow = signedOverflow &- 1
// O signedOverflow agora é igual a 127
'''




O valor mínimo que um ‘Int8’ pode conter é ‘-128’
ou ‘10000000’ em binário,
Subtraindo ‘1’ de seu número binário com o operador de overflow
resulta no valor binário ‘01111111’,
que alterna o bit de sinal e resulta em positivo ‘127’
o valor positivo máximo que um ‘Int8’ pode conter.

![](overflowSignedSubtraction)


Para inteiros com e sem sinal,
o overflow na direção positiva
envolve do valor inteiro válido máximo de volta ao mínimo,
e o overflow na direção negativa
envolve do valor mínimo ao máximo.

## Precedência e Associatividade

A *precedência* do operador dá a alguns operadores prioridade mais alta do que a outros;
esses operadores são aplicados primeiro.

A *associatividade* do operador define como os operadores de mesma precedência
estão agrupados ---
agrupados à esquerda ou à direita.
Pense nisso como significando “eles associam com a expressão à sua esquerda”,
ou “associam-se à expressão à sua direita”.

É importante considerar
a precedência e associatividade de cada operador
ao calcular a ordem na qual uma expressão composta será executada.
Por exemplo,
a precedência do operador explica por que a seguinte expressão é igual a `17`.

```swift
2 + 3 % 4 * 5
// isso é igual a 17
```






Se você ler estritamente da esquerda para a direita,
você pode esperar que a expressão seja calculada da seguinte forma:

- `2` mais `3` é igual a `5`
- `5` módulo `4` é igual a `1`
- `1` vezes `5` é igual a `5`

No entanto, a resposta certa é `17`, não `5`.
Os operadores de maior precedência são avaliados antes dos de menor precedência.
Em Swift, como em C,
o operador de módulo (`%`) e o operador de multiplicação (`*`)
têm uma precedência maior do que o operador de adição (`+`).
Como resultado, ambos são avaliados antes que a adição seja considerada.

No entanto, módulo e multiplicação têm a *mesma* precedência.
Para descobrir a ordem exata de avaliação a ser usada,
você também precisa considerar sua associatividade.
O módulo e a multiplicação associam-se à expressão à sua esquerda.
Pense nisso como adicionar parênteses implícitos em torno dessas partes da expressão,
começando pela esquerda:

```swift
2 + ((3 % 4) * 5)
```






`(3 % 4)` é `3`, então isso é equivalente a:

```swift
2 + (3 * 5)
```






`(3 * 5)` é `15`, então isso é equivalente a:

```swift
2 + 15
```






Este cálculo produz a resposta final de `17`.

Para obter informações sobre os operadores fornecidos pela biblioteca padrão do Swift,
incluindo uma lista completa dos grupos de precedência do operador e configurações de associatividade,
Veja [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).

> Nota: as precedências de operadores e as regras de associatividade do Swift são mais simples e previsíveis
> do que os encontrados em C e Objective-C.
> No entanto, isso significa que eles não são exatamente os mesmos que em linguagens baseadas em C.
> Tenha cuidado em garantir que as interações dos operadores ainda se comportem da maneira esperada
> ao portar um código para o Swift.

## Operator Methods

Classes and structures can provide their own implementations of existing operators.
This is known as *overloading* the existing operators.

The example below shows how to implement
the arithmetic addition operator (`+`) for a custom structure.
The arithmetic addition operator is a binary operator
because it operates on two targets
and it's an infix operator because it appears between those two targets.

The example defines a `Vector2D` structure for
a two-dimensional position vector `(x, y)`,
followed by a definition of an *operator method*
to add together instances of the `Vector2D` structure:

```swift
struct Vector2D {
   var x = 0.0, y = 0.0
}

extension Vector2D {
    static func + (left: Vector2D, right: Vector2D) -> Vector2D {
       return Vector2D(x: left.x + right.x, y: left.y + right.y)
    }
}
```




The operator method is defined as a type method on `Vector2D`,
with a method name that matches the operator to be overloaded (`+`).
Because addition isn't part of the essential behavior for a vector,
the type method is defined in an extension of `Vector2D`
rather than in the main structure declaration of `Vector2D`.
Because the arithmetic addition operator is a binary operator,
this operator method takes two input parameters of type `Vector2D`
and returns a single output value, also of type `Vector2D`.

In this implementation, the input parameters are named `left` and `right`
to represent the `Vector2D` instances that will be on
the left side and right side of the `+` operator.
The method returns a new `Vector2D` instance,
whose `x` and `y` properties are
initialized with the sum of the `x` and `y` properties from
the two `Vector2D` instances that are added together.

The type method
can be used as an infix operator between existing `Vector2D` instances:

```swift
let vector = Vector2D(x: 3.0, y: 1.0)
let anotherVector = Vector2D(x: 2.0, y: 4.0)
let combinedVector = vector + anotherVector
// combinedVector is a Vector2D instance with values of (5.0, 5.0)
```




This example adds together the vectors `(3.0, 1.0)` and `(2.0, 4.0)`
to make the vector `(5.0, 5.0)`, as illustrated below.

![](vectorAddition)


### Prefix and Postfix Operators

The example shown above demonstrates a custom implementation of a binary infix operator.
Classes and structures can also provide implementations
of the standard *unary operators*.
Unary operators operate on a single target.
They're *prefix* if they precede their target (such as `-a`)
and *postfix* operators if they follow their target (such as `b!`).

You implement a prefix or postfix unary operator by writing
the `prefix` or `postfix` modifier
before the `func` keyword when declaring the operator method:

```swift
extension Vector2D {
    static prefix func - (vector: Vector2D) -> Vector2D {
        return Vector2D(x: -vector.x, y: -vector.y)
    }
}
```




The example above implements the unary minus operator
(`-a`) for `Vector2D` instances.
The unary minus operator is a prefix operator,
and so this method has to be qualified with the `prefix` modifier.

For simple numeric values, the unary minus operator converts
positive numbers into their negative equivalent and vice versa.
The corresponding implementation for `Vector2D` instances
performs this operation on both the `x` and `y` properties:

```swift
let positive = Vector2D(x: 3.0, y: 4.0)
let negative = -positive
// negative is a Vector2D instance with values of (-3.0, -4.0)
let alsoPositive = -negative
// alsoPositive is a Vector2D instance with values of (3.0, 4.0)
```




### Operadores de Atribuição Composta

*Operadores de atribuição composta* combinam atribuição ('=') com outra operação.
Por exemplo, o operador de atribuição de adição ('+=')
combina adição e atribuição em uma única operação
Você marca o tipo de parâmetro de entrada esquerdo de um operador de atribuição composto como 'inout',
pois o valor do parâmetro será modificado diretamente de dentro do método o operador.

O exemplo abaixo implementa
um operador de atribuição de adição para instâncias 'Vector2D':

'''swift
extension Vector2D {
    static func += (left: inout Vector2D, right: Vector2D) {
        left = left + right
    }
}
'''




Como um operador de adição foi definido anteriormente,
você não precisa reimplementar o processo de adição aqui.
Nesse caso, o método do operador de atribuição de adição
aproveita do método de operador de adição existente,
e o uso para definir o valor esquerdo como o valor esquerdo somado ao valor direito:

'''swift
var original = Vector2D(x: 1.0, y: 2.0)
let vectorToAdd = Vector2D(x: 3.0, y: 4.0)
original += vectorToAdd
// agora, original tem os valores de (4.0, 6.0)
'''




> Nota: Não é possível sobrecarregar o padrão
> operador de atribuição (‘=‘)
> Somente os operadores de tribuição compostos podem ser sobrecarregados.
> Igualmente, o operador condicional ternário
> ('a ? b : c') não podem ser sobrecarregados.



### Operadores de Equivalência

Por padrão , classes customizadas e structures não possuem uma implementação dos *operadores de equivalência*, conhecidos como os operadores *igual a* (`==`) e *diferente de* (`!=`). Normalmente se implementa o operador `==` e se usa a implementação padrão do operador (`!=`) da biblioteca padrão que nega o resultado do operador `==`. Existem duas maneiras de se implementar o operador `==`: Você pode implementar por conta própria ou, em muitos casos, você pode pedir ao Swift para que sintetize a implementação por você. Em ambos os casos, você adiciona conformidade ao protocolo `Equatable` da biblioteca padrão.

Você pode fornecer a implementação do operador `==` da mesma maneira que implementa outros operadores infixos:

```swift
extension Vector2D: Equatable {
    static func == (left: Vector2D, right: Vector2D) -> Bool {
       return (left.x == right.x) && (left.y == right.y)
    }
}
```




O exemplo acima implementa um operador `==` para verificar se duas instancias de `Vector2D` tem valores equivalentes. No contexto de `Vector2D`, faz sentido considerar que "igual" significa que "ambas as instâncias tem os mesmos valores de `x` e `y`", sendo essa a lógica usada pela implementação  do operador.

Agora você pode usar esse operador para verificar se duas instâncias de `Vector2D` são equivalentes:

```swift
let twoThree = Vector2D(x: 2.0, y: 3.0)
let anotherTwoThree = Vector2D(x: 2.0, y: 3.0)
if twoThree == anotherTwoThree {
   print("These two vectors are equivalent.")
}
// Prints "These two vectors are equivalent."
```




Em muitos casos simples, você pode pedir que o Swift sintetize a implementação dos operadores de equivalência , como descrito em <doc:Protocols#Adopting-a-Protocol-Using-a-Synthesized-Implementation>.

## Custom Operators

You can declare and implement your own *custom operators* in addition to
the standard operators provided by Swift.
For a list of characters that can be used to define custom operators,
see <doc:LexicalStructure#Operators>.

New operators are declared at a global level using the `operator` keyword,
and are marked with the `prefix`, `infix` or `postfix` modifiers:

```swift
prefix operator +++
```




The example above defines a new prefix operator called `+++`.
This operator doesn't have an existing meaning in Swift,
and so it's given its own custom meaning below in the specific context of
working with `Vector2D` instances. For the purposes of this example,
`+++` is treated as a new “prefix doubling” operator.
It doubles the `x` and `y` values of a `Vector2D` instance,
by adding the vector to itself with the addition assignment operator defined earlier.
To implement the `+++` operator,
you add a type method called `+++` to `Vector2D` as follows:

```swift
extension Vector2D {
   static prefix func +++ (vector: inout Vector2D) -> Vector2D {
      vector += vector
      return vector
   }
}

var toBeDoubled = Vector2D(x: 1.0, y: 4.0)
let afterDoubling = +++toBeDoubled
// toBeDoubled now has values of (2.0, 8.0)
// afterDoubling also has values of (2.0, 8.0)
```




### Precedence for Custom Infix Operators

Custom infix operators each belong to a precedence group.
A precedence group specifies an operator's precedence relative
to other infix operators, as well as the operator's associativity.
See <doc:AdvancedOperators#Precedence-and-Associativity> for an explanation of
how these characteristics affect an infix operator's interaction
with other infix operators.

A custom infix operator that isn't explicitly placed into a precedence group is
given a default precedence group with a precedence immediately higher
than the precedence of the ternary conditional operator.

The following example defines a new custom infix operator called `+-`,
which belongs to the precedence group `AdditionPrecedence`:

```swift
infix operator +-: AdditionPrecedence
extension Vector2D {
   static func +- (left: Vector2D, right: Vector2D) -> Vector2D {
      return Vector2D(x: left.x + right.x, y: left.y - right.y)
   }
}
let firstVector = Vector2D(x: 1.0, y: 2.0)
let secondVector = Vector2D(x: 3.0, y: 4.0)
let plusMinusVector = firstVector +- secondVector
// plusMinusVector is a Vector2D instance with values of (4.0, -2.0)
```




This operator adds together the `x` values of two vectors,
and subtracts the `y` value of the second vector from the first.
Because it's in essence an “additive” operator,
it has been given the same precedence group
as additive infix operators such as `+` and `-`.
For information about the operators provided by the Swift standard library,
including a complete list of the operator precedence groups and associativity settings,
see [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).
For more information about precedence groups and to see the syntax for
defining your own operators and precedence groups,
see <doc:Declarations#Operator-Declaration>.

> Note: You don't specify a precedence when defining a prefix or postfix operator.
> However, if you apply both a prefix and a postfix operator to the same operand,
> the postfix operator is applied first.



## Result Builders

A *result builder* is a type you define
that adds syntax for creating nested data,
like a list or tree,
in a natural, declarative way.
The code that uses the result builder
can include ordinary Swift syntax, like `if`  and `for`,
to handle conditional or repeated pieces of data.

The code below defines a few types for drawing on a single line
using stars and text.

```swift
protocol Drawable {
    func draw() -> String
}
struct Line: Drawable {
    var elements: [Drawable]
    func draw() -> String {
        return elements.map { $0.draw() }.joined(separator: "")
    }
}
struct Text: Drawable {
    var content: String
    init(_ content: String) { self.content = content }
    func draw() -> String { return content }
}
struct Space: Drawable {
    func draw() -> String { return " " }
}
struct Stars: Drawable {
    var length: Int
    func draw() -> String { return String(repeating: "*", count: length) }
}
struct AllCaps: Drawable {
    var content: Drawable
    func draw() -> String { return content.draw().uppercased() }
}
```




The `Drawable` protocol defines the requirement
for something that can be drawn, like a line or shape:
The type must implement a `draw()` method.
The `Line` structure represents a single-line drawing,
and it serves the top-level container for most drawings.
To draw a `Line`,
the structure calls `draw()` on each of the line's components,
and then concatenates the resulting strings into a single string.
The `Text` structure wraps a string to make it part of a drawing.
The `AllCaps` structure wraps and modifies another drawing,
converting any text in the drawing to uppercase.

It's possible to make a drawing with these types
by calling their initializers:

```swift
let name: String? = "Ravi Patel"
let manualDrawing = Line(elements: [
     Stars(length: 3),
     Text("Hello"),
     Space(),
     AllCaps(content: Text((name ?? "World") + "!")),
     Stars(length: 2),
])
print(manualDrawing.draw())
// Prints "***Hello RAVI PATEL!**"
```




This code works, but it's a little awkward.
The deeply nested parentheses after `AllCaps` are hard to read.
The fallback logic to use "World" when `name` is `nil`
has to be done inline using the `??` operator,
which would be difficult with anything more complex.
If you needed to include switches or `for` loops
to build up part of the drawing, there's no way to do that.
A result builder lets you rewrite code like this
so that it looks like normal Swift code.

To define a result builder,
you write the `@resultBuilder` attribute on a type declaration.
For example, this code defines a result builder called `DrawingBuilder`,
which lets you use a declarative syntax to describe a drawing:

```swift
@resultBuilder
struct DrawingBuilder {
    static func buildBlock(_ components: Drawable...) -> Drawable {
        return Line(elements: components)
    }
    static func buildEither(first: Drawable) -> Drawable {
        return first
    }
    static func buildEither(second: Drawable) -> Drawable {
        return second
    }
}
```




The `DrawingBuilder` structure defines three methods
that implement parts of the result builder syntax.
The `buildBlock(_:)` method adds support for
writing a series of lines in a block of code.
It combines the components in that block into a `Line`.
The `buildEither(first:)` and `buildEither(second:)` methods
add support for `if`-`else`.

You can apply the `@DrawingBuilder` attribute to a function's parameter,
which turns a closure passed to the function
into the value that the result builder creates from that closure.
For example:

```swift
func draw(@DrawingBuilder content: () -> Drawable) -> Drawable {
    return content()
}
func caps(@DrawingBuilder content: () -> Drawable) -> Drawable {
    return AllCaps(content: content())
}

func makeGreeting(for name: String? = nil) -> Drawable {
    let greeting = draw {
        Stars(length: 3)
        Text("Hello")
        Space()
        caps {
            if let name = name {
                Text(name + "!")
            } else {
                Text("World!")
            }
        }
        Stars(length: 2)
    }
    return greeting
}
let genericGreeting = makeGreeting()
print(genericGreeting.draw())
// Prints "***Hello WORLD!**"

let personalGreeting = makeGreeting(for: "Ravi Patel")
print(personalGreeting.draw())
// Prints "***Hello RAVI PATEL!**"
```




The `makeGreeting(for:)` function takes a `name` parameter
and uses it to draw a personalized greeting.
The `draw(_:)` and `caps(_:)` functions
both take a single closure as their argument,
which is marked with the `@DrawingBuilder` attribute.
When you call those functions,
you use the special syntax that `DrawingBuilder` defines.
Swift transforms that declarative description of a drawing
into a series of calls to the methods on `DrawingBuilder`
to build up the value that's passed as the function argument.
For example,
Swift transforms the call to `caps(_:)` in that example
into code like the following:

```swift
let capsDrawing = caps {
    let partialDrawing: Drawable
    if let name = name {
        let text = Text(name + "!")
        partialDrawing = DrawingBuilder.buildEither(first: text)
    } else {
        let text = Text("World!")
        partialDrawing = DrawingBuilder.buildEither(second: text)
    }
    return partialDrawing
}
```




Swift transforms the `if`-`else` block into
calls to the `buildEither(first:)` and `buildEither(second:)` methods.
Although you don't call these methods in your own code,
showing the result of the transformation
makes it easier to see how Swift transforms your code
when you use the `DrawingBuilder` syntax.

To add support for writing `for` loops in the special drawing syntax,
add a `buildArray(_:)` method.

```swift
extension DrawingBuilder {
    static func buildArray(_ components: [Drawable]) -> Drawable {
        return Line(elements: components)
    }
}
let manyStars = draw {
    Text("Stars:")
    for length in 1...3 {
        Space()
        Stars(length: length)
    }
}
```




In the code above, the `for` loop creates an array of drawings,
and the `buildArray(_:)` method turns that array into a `Line`.

For a complete list of how Swift transforms builder syntax
into calls to the builder type's methods,
see <doc:Attributes#resultBuilder>.











