# Strings e Characters

Armazene e manipule texto.

Uma *string* é uma série de caracteres,
tal como `"hello, world"` ou `"albatross"`.
_Strings_ em Swift são representadas pelo tipo `String`.
O conteúdo de uma `String` pode ser acessado de várias maneiras,
incluindo como uma coleção de valores `Character`.

Os tipos `String` e `Character` fornecem uma maneira 
rápida e compatível com Unicode de trabalhar com texto em seu código.
A sintaxe para criação e manipulação de _string_ é leve e legível,
com uma sintaxe literal de _string_ semelhante a C. 
A concatenação de _strings_ é tão simples como a combinação de duas 
_strings_ com o operador `+`,
e a mutabilidade é gerenciada escolhendo entre uma constante ou uma variável,
assim como qualquer outro valor em Swift.
Você também pode usar _strings_ para inserir constantes, variáveis, literais e 
expressões mais longas, em um processo conhecido como interpolação de _string_.
Isso facilita a criação de valores de _string_ personalizados para exibição, 
armazenamento e impressão.

Apesar desta simplicidade de sintaxe, 
o tipo `String` em Swift é uma implementação rápida e moderna.
Todas as _strings_ são compostas de caracteres Unicode independentes de codificação,
e fornece suporte para acessar esses caracteres em várias representações Unicode.

> Nota: O tipo `String` em Swift é conectado com a classe `NSString` da biblioteca Foundation.
> Foundation também extende `String` para expor métodos definidos por `NSString`.
> Isso significa que, se você importar a biblioteca Foundation,
> você pode acessar esses métodos de `NSString` em `String` sem conversão. Para mais informações sobre como usar `String` com Foundation e Cocoa,
> veja [Bridging Between String and NSString](https://developer.apple.com/documentation/swift/string#2919514).


## Strings Literais

Você pode incluir valores `String` predefinidos em seu código com **literais de string**.
Uma _string_ literal é uma sequência de caracteres entre aspas duplas (`"`).

Use uma _string_ literal como um valor inicial para uma constante ou variável:

```swift
let someString = "Some string literal value"
```

Note que Swift infere um tipo de `String` para a constante `someString` 
porque é inicializado com um valor literal de _string_.

### Strings Literais Multilinha

Se você precisar de uma _string_ que ocupe várias linhas,
use _string_ literal multilinha ---
uma sequência de caracteres
cercada por três aspas duplas:

```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

Uma _string_ literal multilinha inclui todas as linhas entre
a abertura e o fechamento das aspas.
A string começa na primeira linha após as aspas de abertura (`"""`)
e termina na linha anterior das aspas de fechamento,
o que significa que nenhuma das strings abaixo começa ou termina com a quebra de linha: 

```swift
let singleLineString = "These are the same."
let multilineString = """
These are the same.
"""
```

Quando seu código-fonte inclui uma quebra de linha
dentro de uma _string_ literal multilinha,
essa quebra de linha também aparece no valor da _string_.
Se você quiser usar quebras de linha
para fazer seu código-fonte mais fácil de ler,
mas não deseja que as quebras de linha façam parte do valor da _string_,
escreva uma barra invertida (`\`) no final dessas linhas:

```swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

Para fazer uma _string_ literal multilinha que comece ou termine com uma quebra de linha,
escreva uma linha em branco como a primeira ou a última linha.
Por exemplo:

```swift
let lineBreaks = """

This string starts with a line break.
It also ends with a line break.

"""
```

Uma _string_ multilinha pode ser indentada para alinhar com o código ao redor.
O espaço em branco antes das aspas de fechamento (`"""`)
informa ao Swift qual espaço em branco ignorar antes de todas as outras linhas.
No entanto, se você adiconar espaço em branco no começo de uma linha, 
além do que está antes das aspas de fechamento, 
esse espaço em branco *é* incluído.

![](multilineStringWhitespace)

No exemplo acima,
embora todo _string_ literal multilinha seja indentada,
as primeiras e as últimas linhas da _string_ não começam com nenhum espaço em branco.
A linha do meio tem mais indentação do que a linha das aspas de fechamento,
então ela começa com esses quatro espaços adicionais de indentação.

### Caracteres Especiais em Strings Literais 

_Strings_ literais podem incluir os seguintes caracteres especiais:

- Os caracteres especiais com escape `\0` (caracter nulo), `\\` (barra invertida),
  `\t` (tabulação horizontal), `\n` (quebra de linha), `\r` (_carriage return_), 
  `\"` (aspas duplas) and `\'` (aspas simples)
- Um valor escalar _Unicode_ arbitrário, escrito com `\\u{`*n*`}`,
  onde *n* é um número hexadecimal de 1 a 8 dígitos
  (_Unicode_ é discutido em <doc:StringsAndCharacters#Unicode>)

O código abaixo mostra quatro exemplos desses caracteres especiais.
A constante `wiseWords` contém duas aspas duplas com escape.
As contantes `dollarSign`, `blackHeart` e `sparklingHeart`
demonstram o formato escalar _Unicode_:

```swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode escalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode escalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode escalar U+1F496
```

Como _strings_ literais multilinhas usam três aspas duplas em vez de apenas uma,
você pode incluir uma aspa dupla (`"`) dentro de uma _string_ literal multilinha
sem precisar fazer o escape.
Para incluir o texto `"""` em uma _string_ multilinha,
faça o escape de pelo menos uma das aspas duplas.
Por exemplo: 

```swift
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
```

### Delimitadores de Strings Estendidos

Você pode colocar uma _string_ literal dentro de *delimitadores estendidos*
para incluir caracteres especiais em uma _string_
sem invocar seus efeitos.
Você coloca sua _string_ entre aspas duplas (`"`)
e cerca com o sinal númerico cerquilha (`#`).
Por exemplo, imprimir a _string_ literal `#"Line 1\nLine 2"#`
imprime a sequência de escape para quebra de linha (`\n`)
em vez de imprimir a _string_ em duas linhas.

Se você precisar dos efeitos de um caractere especial em uma _string_ literal,
combine o sinal numérico cerquilha dentro da _string_
após o caracter de escape (`\`).
Por exemplo, se a sua _string_ é `#"Line 1\nLine 2"#`
e você quer quebrar a linha,
pode substituir por `#"Line 1\#nLine 2"#`.
De maneira similar, `###"Line1\###nLine2"###` também quebra linha.

_Strings_ literias criadas usando delimitadores estendidos também podem ser _strings_ literais multilinha.
Você pode usar delimitadores estendidos para incluir o texto `"""` em uma _string_ multilinha,
substituindo o comportamento padrão que encerra o literal. Por exemplo:

```swift
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#
```

## Inicializando Uma String Vazia

Para criar uma `String` de valor vazio como ponto de partida para se construir uma string maior, você pode atribuir uma string vazia para uma variável ou inicializar uma nova instâncias de `String` com sintaxe de inicializador:

```swift
var emptyString = ""               // string literal vazia
var anotherEmptyString = String()  // sintaxe do inicializador
// Essas duas string estão ambas vazias, e são equivalentes uma com a outra
```

Descubra se uma `String` possui valor vazio verificando sua propriedade Booleana `isEmpty`:

```swift
if emptyString.isEmpty {
   print("Nothing to see here")
}
// Imprime "Nothing to see here"
```

## Mutabilidade de String

Você pode indicar se uma determinada `String` pode ser modificada (ou *mutável*)
atribuindo-a a uma variável (nesse caso, ela pode ser modificada),
ou a uma contante (nesse caso, ela não pode ser modificada):

```swift
var variableString = "Horse"
variableString += " and carriage"
// variableString é agora "Horse and carriage"

let constantString = "Highlander"
constantString += " and another Highlander"
// Isso gera um erro de compilação - uma string constante não pode ser modificada
```

> Nota: Essa abordagem é diferente da mutação de _strings_ em Obsective-C e Cocoa,
> onde você escolhe entre duas classes (`NSString` and `NSMutableString`)
> para indicar se uma _string_ pode ser mutável.

## Strings São Tipos de Valor

O tipo `String` de Swift é um *tipo de valor*.
Se você criar um novo valor `String`, esse valor 
`String` é *copiado* quando é passado para uma função ou método,
ou quando é atribuído a uma constante ou variável.
Em cada caso, uma nova cópia do valor `String` existente é criado,
e a nova cópia é passada ou atribuída, não a versão original.
Tipos de valor são descritos em <doc:ClassesAndStructures#Structures-and-Enumerations-Are-Value-Types>.

O comportamento de cópia de `String` por padrão do Swift grarante
que quando uma função ou método passa um valor `String`, é claro
que você terá o valor exato da `String`, independente de onde veio.
Você pode estar confiante que a string que você passou não será modificada
a não ser que você mesmo modifique.

Nos bastidores, o compilador do Swift otimiza o uso de strings 
para que a cópia realmente aconteça apenas quando for absolutamente necessário.
Isso significa que você sempre terá um ótimo desempenho
quando trabalhar com strings como tipos de valor.

## Trabalhando com Characteres

Você pode acessar os valores `Character` individuais de uma `String`
iterando sobre a string com um laço `for`-`in`:

```swift
for character in "Dog!🐶" {
   print(caracter)
}
// D
// o
// g
// !
// 🐶
```

O laço `for`-`in` está descrito em <doc:ControlFlow#For-In-Loops>.

Alternativamente, você pode criar uma constante ou variável autônoma `Character`
de um string literal de caractere único fornecendo uma notação do tipo `Character`:

```swift
let exclamationMark: Character = "!"
```

Valores `String` podem ser construídos passando um vetor de valores `Character` 
como um argumento para o inicializador:

```swift
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Imprime "Cat!🐱"
```

## Concatenando String e Caracteres

Valores `String` podem ser adicionados entre si (ou *concatenados*)
com o operador de adição (`+`) para criar um novo valor de `String`:

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome agora é igual a "hello there"
```

Você também pode adicionar um valor de `String` em uma variável `String` existente
com o operador de atribuição de adição (`+=`):

```swift
var instruction = "look over"
instruction += string2
// instruction agora é igual a "look over there"
```

Você pode adicionar um valor `Character` a uma váriavel `String`
com o método `append()` do tipo `String`:

```swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome agora é igual a "hello there!"
```

> Nota: Você não pode adicionar uma `String` ou `Character` a uma váriavel `Character` existente,
> pois um valor `Character` deve conter apenas um único caractere.

Se você está usando _strings_ literais multilinha
para construir as linhas de uma _string_ mais longa,
você deseja que toda linha da _string_ termine com uma quebra de linha,
incluindo a última linha.
Por exemplo:

```swift
let badStart = """
    one
    two
    """
let end = """
    three
    """
print(badStart + end)
// Imprime duas linhas:
// one
// twothree

let goodStart = """
    one
    two

    """
print(goodStart + end)
// Imprime três linhas:
// one
// two
// three
```

No código acima,
concatenar `badStart` com `end`
produz uma _string_ de duas linhas,
o que não é o resultado desejado.
Como a última linha de `badStart`
não termina com uma quebra de linha,
essa linha é combinada com a primeira linha de `end`.
Por outro lado,
as linhas de `goodStart` terminam com quebra de linha,
então, quando combinada com `end`
o resultado possui três linhas,
como esperado.

## Interpolação de Strings 

A *Interpolação de _strings_* é uma maneira de contruir um novo valor `String`
a partir de uma combinação de constantes, variáveis, literais e expressões
incluindo seus valores dentro de uma _string_ literal.
Você pode usar interpolação de _strings_
tanto em _string_ literais de uma única linha como de múltiplas linhas.
Cada item que você adiciona em uma _string_ literal é cercado
por um par de parênteses, precedido por uma barra invertida (`\`):

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message é "3 times 2.5 is 7.5"
```

No exemplo acima,
o valor de `multiplier` é adicionado dentro de uma _string_ literal como `\(multiplier)`.
Esse espaço reservado é substituído com o valor real de `multiplier`
quando a interpolação de _strings_ é processada para criar a _string_ real. 

O valor de `multiplier` é também parte de uma expressão mais adiante na _string_.
Essa expressão calcula o valor de `Double(multiplier) * 2.5`
e adiciona o resultado (`7.5`) dentro da _string_.
Nesse caso, a expressão é escrita como `\(Double(multiplier) * 2.5)`
quando incluída na _string_ literal.

Você pode usar delimitadores de _string_ estendidos para criar _strings_ contendo
caracteres que, de outra forma, seriam tratados como uma interpolação de _strings_.
Por exemplo:

```swift
print(#"Write an interpolated string in Swift using \(multiplier)."#)
// Imprime "Write an interpolated string in Swift using \(multiplier)."
```

Para usar interpolação de _strings_
dentro de uma _string_ que usa delimitadores estendidos,
combine o sinal numérico cerquilha após a barra invertida 
às cerquilhas no começo e no final da _string_.
Por exemplo:

```swift
print(#"6 times 7 is \#(6 * 7)."#)
// Imprime "6 times 7 is 42."
```

> Nota: As expressões que você escreve entre parênteses em uma _string_ interpolada
> não podem conter uma barra invertida escapada (`\`), um _carriage return_ ou uma quebra de linha.
> No entanto, elas podem conter outras _strings_ literais.

## Unicode

*Unicode* é um padrão internacional para
codificar, representar e processar texto em diferentes sistemas de escrita.
Isso permite que você represente quase qualquer caractere de qualquer idioma em uma forma padronizada,
e ler e escrever esses caracteres de e para uma fonte externa,
como um arquivo de texto ou uma página da web.
Os tipos `String` e `Character` em Swift são totalmente compatíveis com o Unicode,
conforme descrito nesta seção.

### Valores Escalares Unicode

Nos bastidores,
o tipo `String`nativo do Swift é contruído a partit de *valores escalares Unicode*.
Um valor escalar Unicode é um número único de 21 _bits_ para um caractere ou um modificador,
como `U+0061` para `LATIN SMALL LETTER A` (`"a"`),
ou `U+1F425` para `FRONT-FACING BABY CHICK` (`"🐥"`).

Note que nem todos os valores escalares Unicode de 21 _bits_ estão atribuídos a um caractere --
alguns escalares são reservados para atribuições futuras ou para uso na codificação UTF-16.
Os Valores escalares que foram atribuídos a um caractere normalmente também possuem um nome,
como `LATIN SMALL LETTER A` e `FRONT-FACING BABY CHICK` nos exemplos acima.

### Extended Grapheme Clusters

Every instance of Swift's `Character` type represents
a single *extended grapheme cluster*.
An extended grapheme cluster is a sequence of one or more Unicode scalars
that (when combined) produce a single human-readable character.

Here's an example.
The letter `é` can be represented as the single Unicode scalar `é`
(`LATIN SMALL LETTER E WITH ACUTE`, or `U+00E9`).
However, the same letter can also be represented as a *pair* of scalars ---
a standard letter `e` (`LATIN SMALL LETTER E`, or `U+0065`),
followed by the `COMBINING ACUTE ACCENT` scalar (`U+0301`).
The `COMBINING ACUTE ACCENT` scalar is graphically applied to the scalar that precedes it,
turning an `e` into an `é` when it's rendered by
a Unicode-aware text-rendering system.

In both cases, the letter `é` is represented as a single Swift `Character` value
that represents an extended grapheme cluster.
In the first case, the cluster contains a single scalar;
in the second case, it's a cluster of two scalars:

```swift
let eAcute: Character = "\u{E9}"                         // é
let combinedEAcute: Character = "\u{65}\u{301}"          // e followed by ́
// eAcute is é, combinedEAcute is é
```




Extended grapheme clusters are a flexible way to represent
many complex script characters as a single `Character` value.
For example, Hangul syllables from the Korean alphabet
can be represented as either a precomposed or decomposed sequence.
Both of these representations qualify as a single `Character` value in Swift:

```swift
let precomposed: Character = "\u{D55C}"                  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // ᄒ, ᅡ, ᆫ
// precomposed is 한, decomposed is 한
```




Extended grapheme clusters enable
scalars for enclosing marks (such as `COMBINING ENCLOSING CIRCLE`, or `U+20DD`)
to enclose other Unicode scalars as part of a single `Character` value:

```swift
let enclosedEAcute: Character = "\u{E9}\u{20DD}"
// enclosedEAcute is é⃝
```




Unicode scalars for regional indicator symbols
can be combined in pairs to make a single `Character` value,
such as this combination of `REGIONAL INDICATOR SYMBOL LETTER U` (`U+1F1FA`)
and `REGIONAL INDICATOR SYMBOL LETTER S` (`U+1F1F8`):

```swift
let regionalIndicatorForUS: Character = "\u{1F1FA}\u{1F1F8}"
// regionalIndicatorForUS is 🇺🇸
```




## Counting Characters

To retrieve a count of the `Character` values in a string,
use the `count` property of the string:

```swift
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.count) characters")
// Prints "unusualMenagerie has 40 characters"
```




Note that Swift's use of extended grapheme clusters for `Character` values
means that string concatenation and modification may not always affect
a string's character count.

For example, if you initialize a new string with the four-character word `cafe`,
and then append a `COMBINING ACUTE ACCENT` (`U+0301`) to the end of the string,
the resulting string will still have a character count of `4`,
with a fourth character of `é`, not `e`:

```swift
var word = "cafe"
print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in cafe is 4"

word += "\u{301}"    // COMBINING ACUTE ACCENT, U+0301

print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in café is 4"
```




> Note: Extended grapheme clusters can be composed of multiple Unicode scalars.
> This means that different characters—
> and different representations of the same character—
> can require different amounts of memory to store.
> Because of this, characters in Swift don't each take up
> the same amount of memory within a string's representation.
> As a result, the number of characters in a string can't be calculated
> without iterating through the string to determine
> its extended grapheme cluster boundaries.
> If you are working with particularly long string values,
> be aware that the `count` property
> must iterate over the Unicode scalars in the entire string
> in order to determine the characters for that string.The count of the characters returned by the `count` property
> isn't always the same as the `length` property of
> an `NSString` that contains the same characters.
> The length of an `NSString` is based on
> the number of 16-bit code units within the string's UTF-16 representation
> and not the number of Unicode extended grapheme clusters within the string.

## Accessing and Modifying a String

You access and modify a string through its methods and properties,
or by using subscript syntax.

### String Indices

Each `String` value has an associated *index type*,
`String.Index`,
which corresponds to the position of each `Character` in the string.

As mentioned above,
different characters can require different amounts of memory to store,
so in order to determine which `Character` is at a particular position,
you must iterate over each Unicode scalar from the start or end of that `String`.
For this reason, Swift strings can't be indexed by integer values.

Use the `startIndex` property to access
the position of the first `Character` of a `String`.
The `endIndex` property is the position after the last character in a `String`.
As a result,
the `endIndex` property isn't a valid argument to a string's subscript.
If a `String` is empty, `startIndex` and `endIndex` are equal.

You access the indices before and after a given index
using the `index(before:)` and `index(after:)` methods of `String`.
To access an index farther away from the given index,
you can use the `index(_:offsetBy:)` method
instead of calling one of these methods multiple times.

You can use subscript syntax to access
the `Character` at a particular `String` index.

```swift
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
```




Attempting to access an index outside of a string's range
or a `Character` at an index outside of a string's range
will trigger a runtime error.

```swift
greeting[greeting.endIndex] // Error
greeting.index(after: greeting.endIndex) // Error
```






Use the `indices` property to access all of the
indices of individual characters in a string.

```swift
for index in greeting.indices {
   print("\(greeting[index]) ", terminator: "")
}
// Prints "G u t e n   T a g ! "
```






> Note: You can use the `startIndex` and `endIndex` properties
> and the `index(before:)`, `index(after:)`, and `index(_:offsetBy:)` methods
> on any type that conforms to the `Collection` protocol.
> This includes `String`, as shown here,
> as well as collection types such as `Array`, `Dictionary`, and `Set`.

### Inserting and Removing

To insert a single character into a string at a specified index,
use the `insert(_:at:)` method,
and to insert the contents of another string at a specified index,
use the `insert(contentsOf:at:)` method.

```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
```




To remove a single character from a string at a specified index,
use the `remove(at:)` method,
and to remove a substring at a specified range,
use the `removeSubrange(_:)` method:

```swift
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"
```






> Note: You can use the `insert(_:at:)`, `insert(contentsOf:at:)`,
> `remove(at:)`, and `removeSubrange(_:)` methods
> on any type that conforms to the `RangeReplaceableCollection` protocol.
> This includes `String`, as shown here,
> as well as collection types such as `Array`, `Dictionary`, and `Set`.

## Substrings

When you get a substring from a string ---
for example, using a subscript or a method like `prefix(_:)` ---
the result is an instance
of [Substring](https://developer.apple.com/documentation/swift/substring),
not another string.
Substrings in Swift have most of the same methods as strings,
which means you can work with substrings
the same way you work with strings.
However, unlike strings,
you use substrings for only a short amount of time
while performing actions on a string.
When you're ready to store the result for a longer time,
you convert the substring to an instance of `String`.
For example:

```swift
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
```




Like strings, each substring has a region of memory
where the characters that make up the substring are stored.
The difference between strings and substrings
is that, as a performance optimization,
a substring can reuse part of the memory
that's used to store the original string,
or part of the memory that's used to store another substring.
(Strings have a similar optimization,
but if two strings share memory, they're equal.)
This performance optimization means
you don't have to pay the performance cost of copying memory
until you modify either the string or substring.
As mentioned above,
substrings aren't suitable for long-term storage ---
because they reuse the storage of the original string,
the entire original string must be kept in memory
as long as any of its substrings are being used.

In the example above,
`greeting` is a string,
which means it has a region of memory
where the characters that make up the string are stored.
Because
`beginning` is a substring of `greeting`,
it reuses the memory that `greeting` uses.
In contrast,
`newString` is a string ---
when it's created from the substring,
it has its own storage.
The figure below shows these relationships:



![](stringSubstring)


> Note: Both `String` and `Substring` conform to the
> [StringProtocol](https://developer.apple.com/documentation/swift/stringprotocol) protocol,
> which means it's often convenient for string-manipulation functions
> to accept a `StringProtocol` value.
> You can call such functions with either a `String` or `Substring` value.

## Comparing Strings

Swift provides three ways to compare textual values:
string and character equality, prefix equality, and suffix equality.

### String and Character Equality

String and character equality is checked with the “equal to” operator (`==`)
and the “not equal to” operator (`!=`),
as described in <doc:BasicOperators#Comparison-Operators>:

```swift
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
   print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```




Two `String` values (or two `Character` values) are considered equal if
their extended grapheme clusters are *canonically equivalent*.
Extended grapheme clusters are canonically equivalent if they have
the same linguistic meaning and appearance,
even if they're composed from different Unicode scalars behind the scenes.





For example, `LATIN SMALL LETTER E WITH ACUTE` (`U+00E9`)
is canonically equivalent to `LATIN SMALL LETTER E` (`U+0065`)
followed by `COMBINING ACUTE ACCENT` (`U+0301`).
Both of these extended grapheme clusters are valid ways to represent the character `é`,
and so they're considered to be canonically equivalent:

```swift
// "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"

// "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"

if eAcuteQuestion == combinedEAcuteQuestion {
   print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```




Conversely, `LATIN CAPITAL LETTER A` (`U+0041`, or `"A"`),
as used in English, is *not* equivalent to
`CYRILLIC CAPITAL LETTER A` (`U+0410`, or `"А"`),
as used in Russian.
The characters are visually similar,
but don't have the same linguistic meaning:

```swift
let latinCapitalLetterA: Character = "\u{41}"

let cyrillicCapitalLetterA: Character = "\u{0410}"

if latinCapitalLetterA != cyrillicCapitalLetterA {
   print("These two characters aren't equivalent.")
}
// Prints "These two characters aren't equivalent."
```




> Note: String and character comparisons in Swift aren't locale-sensitive.



### Prefix and Suffix Equality

To check whether a string has a particular string prefix or suffix,
call the string's `hasPrefix(_:)` and `hasSuffix(_:)` methods,
both of which take a single argument of type `String` and return a Boolean value.





The examples below consider an array of strings representing
the scene locations from the first two acts of Shakespeare's *Romeo and Juliet*:

```swift
let romeoAndJuliet = [
   "Act 1 Scene 1: Verona, A public place",
   "Act 1 Scene 2: Capulet's mansion",
   "Act 1 Scene 3: A room in Capulet's mansion",
   "Act 1 Scene 4: A street outside Capulet's mansion",
   "Act 1 Scene 5: The Great Hall in Capulet's mansion",
   "Act 2 Scene 1: Outside Capulet's mansion",
   "Act 2 Scene 2: Capulet's orchard",
   "Act 2 Scene 3: Outside Friar Lawrence's cell",
   "Act 2 Scene 4: A street in Verona",
   "Act 2 Scene 5: Capulet's mansion",
   "Act 2 Scene 6: Friar Lawrence's cell"
]
```




You can use the `hasPrefix(_:)` method with the `romeoAndJuliet` array
to count the number of scenes in Act 1 of the play:

```swift
var act1SceneCount = 0
for scene in romeoAndJuliet {
   if scene.hasPrefix("Act 1 ") {
      act1SceneCount += 1
   }
}
print("There are \(act1SceneCount) scenes in Act 1")
// Prints "There are 5 scenes in Act 1"
```




Similarly, use the `hasSuffix(_:)` method to count the number of scenes
that take place in or around Capulet's mansion and Friar Lawrence's cell:

```swift
var mansionCount = 0
var cellCount = 0
for scene in romeoAndJuliet {
   if scene.hasSuffix("Capulet's mansion") {
      mansionCount += 1
   } else if scene.hasSuffix("Friar Lawrence's cell") {
      cellCount += 1
   }
}
print("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
// Prints "6 mansion scenes; 2 cell scenes"
```




> Note: The `hasPrefix(_:)` and `hasSuffix(_:)` methods
> perform a character-by-character canonical equivalence comparison between
> the extended grapheme clusters in each string,
> as described in <doc:StringsAndCharacters#String-and-Character-Equality>.

## Unicode Representations of Strings

When a Unicode string is written to a text file or some other storage,
the Unicode scalars in that string are encoded in one of
several Unicode-defined *encoding forms*.
Each form encodes the string in small chunks known as *code units*.
These include the UTF-8 encoding form (which encodes a string as 8-bit code units),
the UTF-16 encoding form (which encodes a string as 16-bit code units),
and the UTF-32 encoding form (which encodes a string as 32-bit code units).

Swift provides several different ways to access Unicode representations of strings.
You can iterate over the string with a `for`-`in` statement,
to access its individual `Character` values as Unicode extended grapheme clusters.
This process is described in <doc:StringsAndCharacters#Working-with-Characters>.

Alternatively, access a `String` value
in one of three other Unicode-compliant representations:

- A collection of UTF-8 code units (accessed with the string's `utf8` property)
- A collection of UTF-16 code units (accessed with the string's `utf16` property)
- A collection of 21-bit Unicode scalar values,
  equivalent to the string's UTF-32 encoding form
  (accessed with the string's `unicodeScalars` property)

Each example below shows a different representation of the following string,
which is made up of the characters `D`, `o`, `g`,
`‼` (`DOUBLE EXCLAMATION MARK`, or Unicode scalar `U+203C`),
and the 🐶 character (`DOG FACE`, or Unicode scalar `U+1F436`):

```swift
let dogString = "Dog‼🐶"
```

### Representação UTF-8

Você pode acessar uma representação UTF-8 de uma `String` 
iterando sobre a propriedade `utf8`.
Essa propriedade é do tipo `String.UTF8View`,
que é uma coleção de valores inteiros sem sinal de 8 _bits_ (`UInt8`),
um para cada byte na representação UTF-8 da string:

![](UTF8)

```swift
for codeUnit in dogString.utf8 {
   print("\(codeUnit) ", terminator: "")
}
print("")
// Imprime "68 111 103 226 128 188 240 159 144 182 "
```

No exemplo acima, os três primeiros valores `codeUnit` decimais
(`68`, `111`, `103`)
representam os caracteres `D`, `o` e `g`,
cuja representação UTF-8 é a mesma que sua representação ASCII.
Os próximos três valores `codeUnit` decimais 
(`226`, `128`, `188`)
são uma representação UTF-8 de três _bytes_ do caractere `DOUBLE EXCLAMATION MARK`.
Os quatro últimos valores `codeUnit` (`240`, `159`, `144`, `182`)
são uma representação UTF-8 de quatro _bytes_ do caractere `DOG FACE`.

### Representação UTF-16

Você pode acessar uma representação UTF-16 de uma `String`
iterando sobre a propriedade `utf16`.
Essa propriedade é do tipo `String.UTF16View`,
que uma coleção de valores inteiros sem sinal de 16 _bits_ (`UInt16`),
um para cada unidade de código de 16 _bits_ na representação UTF-16 da _string_:

![](UTF16)

```swift
for codeUnit in dogString.utf16 {
   print("\(codeUnit) ", terminator: "")
}
print("")
// Imprime "68 111 103 8252 55357 56374 "
```

Novamente, os três primeiros valores `codeUnit`
(`68`, `111`, `103`)
representam os caracteres `D`, `o` e `g`,
cujas unidades de código UTF-16 têm os mesmos valores que na representação UTF-8 da _string_
(pois esses escalares Unicode representam caracteres ASCII).

O quarto valor `codeUnit` (`8252`) é um decimal equivalente ao
valor hexadecima `203C`,
que representa o escalar Unicode `U+203C`
para o caractere `DOUBLE EXCLAMATION MARK`.
Esse caracteres pode ser representado como uma única unidade de código em UTF-16.

Os quinto e sexto valores `codeUnit` (`55357` e `56374`)
são uma representação de par de substituição UTF-16 do caractere `DOG FACE`.
Esses valores são um valor de alta substituição de `U+D83D` (valor decimal `55357`)
e um valor de baixa substituição de `U+DC36` (valor decimal `56374`).

### Unicode Scalar Representation

You can access a Unicode scalar representation of a `String` value
by iterating over its `unicodeScalars` property.
This property is of type `UnicodeScalarView`,
which is a collection of values of type `UnicodeScalar`.

Each `UnicodeScalar` has a `value` property that returns
the scalar's 21-bit value, represented within a `UInt32` value:

![](UnicodeScalar)


```swift
for scalar in dogString.unicodeScalars {
   print("\(scalar.value) ", terminator: "")
}
print("")
// Prints "68 111 103 8252 128054 "
```






The `value` properties for the first three `UnicodeScalar` values
(`68`, `111`, `103`)
once again represent the characters `D`, `o`, and `g`.

The fourth `codeUnit` value (`8252`) is again a decimal equivalent of
the hexadecimal value `203C`,
which represents the Unicode scalar `U+203C`
for the `DOUBLE EXCLAMATION MARK` character.

The `value` property of the fifth and final `UnicodeScalar`, `128054`,
is a decimal equivalent of the hexadecimal value `1F436`,
which represents the Unicode scalar `U+1F436` for the `DOG FACE` character.

As an alternative to querying their `value` properties,
each `UnicodeScalar` value can also be used to construct a new `String` value,
such as with string interpolation:

```swift
for scalar in dogString.unicodeScalars {
   print("\(scalar) ")
}
// D
// o
// g
// ‼
// 🐶
```



