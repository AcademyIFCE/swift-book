# Tipos de Coleção

Organize dados usando _arrays_, _sets_, e dicionários.

Swift oferece três *tipos de coleção* primários, 
conhecidos como _arrays_, _sets_ e dicionários, 
para armazenar coleções de valores. 
_Arrays_ são coleções ordenadas de valores. 
_Sets_ são coleções não ordenadas de valores únicos. 
Dicionários são coleções não ordenadas de associações chave-valor.

![](CollectionTypes_intro)

_Arrays_, _sets_ e dicionários em Swift são sempre claros sobre 
os tipos de valores e chaves que podem armazenar. 
Isso significa que você não pode inserir um valor do tipo errado 
em uma coleção por engano. 
Isso também significa que você pode ter certeza sobre o tipo de valores
que recuperará de uma coleção.

> Nota: Os tipos `Array`, `Set` e `Dictionary` em Swift são implementados como **coleções genéricas**. 
> Para saber mais sobre tipos genéricos e coleções, consulte <doc:Generics>.

## Mutabilidade de Coleções

Se você criar um _array_, um _set_ ou um dicionário e atribuí-lo a uma variável,
a coleção criada será **mutável**. 
Isso significa que você pode alterar (ou **mutar**) a coleção depois de criada
adicionando, removendo ou alterando itens na coleção. 
Se você atribuir um _array_, um _set_ ou um dicionário a uma constante,
essa coleção é **imutável** e seu tamanho e conteúdo não podem ser alterados.

> Nota: É uma boa prática criar coleções imutáveis
> em todos os casos em que a coleção não precisa ser alterada.
> Fazer isso torna mais fácil raciocinar sobre seu código 
> e permite que o compilador otimize o desempenho
> das coleções que você cria.

## Arrays

Um *array* armazena valores do mesmo tipo em uma lista ordenada.
O mesmo valor pode aparecer em um _array_ várias vezes em posições diferentes.

> Nota: o tipo `Array` em Swift é uma ponte para a classe `NSArray` do Foundation.
> Para obter mais informações sobre como usar `Array` com Foundation e Cocoa,
> veja [Bridging Between Array and NSArray](https://developer.apple.com/documentation/swift/array#2846730).

### Sintaxe Abreviada de Array

O tipo de um array em Swift é escrito por completo como `Array<Element>`,
onde `Element` é o tipo de valores que o _array_ pode armazenar. 
Você também pode escrever o tipo de um _array_ de forma abreviada como `[Element]`.
Embora as duas formas sejam funcionalmente idênticas, 
a forma abreviada é preferida 
e é usada ao longo deste guia ao se referir ao tipo de um _array_.

### Criando um _Array_ vazio

Você pode criar um array vazio de um determinado tipo 
usando a sintaxe de inicialização:

```swift
var someInts: [Int] = []
print("someInts is of type [Int] with \(someInts.count) items.")
// Imprime "someInts is of type [Int] with 0 items."
```

Note que o tipo da variável `someInts` é inferido como `[Int]`
a partir do tipo do inicializador.

Alternativamente, se o contexto já fornece informações sobre o tipo,
como um argumento de função ou uma variável ou constante já digitada,
você pode criar um _array_ vazio com um literal de array vazio,
que é escrito como `[]` (um par vazio de colchetes):

```swift
someInts.append(3)
// `someInts` agora contém um valor do tipo `Int`
someInts = []
// `someInts` agora é uma array vazia, mas ainda é do tipo `[Int]`
```

### Criando um _Array_ com um Valor Padrão

O tipo `Array` em Swift também fornece
um inicializador para criar uma _array_ de um determinado tamanho
com todos os seus valores definidos como mesmo valor padrão.
Você passa a esse inicializador 
um valor padrão do tipo apropriado (`repeating`) 
e o número de vezes que esse valor é repetido (`count`):

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// `threeDoubles` é do tipo `[Double]`, e igual a [0.0, 0.0, 0.0]
```

### Criando um _Array_ Somando Dois _Arrays_

Você pode criar um novo array adicionando dois arrays existentes com tipos compatíveis
com o operador de adição (`+`). O tipo do novo array é inferido
a partir do tipo dos dois _arrays_ que você adiciona:

```swift
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// `anotherThreeDoubles` é do tipo `[Double]`, e igual a [2.5, 2.5, 2.5]

var sixDoubles = threeDoubles + anotherThreeDoubles
// `sixDoubles` é inferido como `[Double]`, e igual a [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

### Criando um Array com um Literal de Array 

Você também pode inicializar um array com um *literal de array*,
que é uma forma abreviada de escrever um ou mais valores como uma coleção de array.
Um literal de array é escrito como uma lista de valores,
separados por vírgulas, entre colchetes:

```
[<#value 1#>, <#value 2#>, <#value 3#>]
```

O exemplo abaixo cria um _array_ chamado `shoppingList` para armazenar valores `String`:

```swift
var shoppingList: [String] = ["Eggs", "Milk"]
// `shoppingList` inicializado com dois items iniciais
```

A variável `shoppingList` é declarada como
“um array de valores de string”, escrita como `[String]`.
Como esse _array_ especificou um tipo de valor `String`, 
é permitido armazenar apenas valores `String`.
Aqui, o _array_ `shoppingList` é inicializado com dois valores `String` (`"Eggs"` e `"Milk"`),
escritos dentro de um literal de array.

> Nota: O array `shoppingList` é declarado como uma variável (com o introdutor `var`) 
> e não uma constante (com o introdutor `let`) 
> porque mais itens são adicionados à lista de compras nos exemplos abaixo.

Nesse caso, o literal de _array_ contém dois valores `String` e nada mais. 
Isso corresponde ao tipo de declaração da variável `shoppingList` (um array que só pode conter valores `String`) 
e, portanto, a atribuição do literal do _array_ é permitida como uma forma de inicializar `shoppingList` com dois itens iniciais.

Graças à inferência de tipo em Swift, você não precisa escrever o tipo do _array_
se estiver inicializando-o com um literal de _array_ contendo valores do mesmo tipo. 
A inicialização de `shoppingList` poderia ter sido escrita de uma forma mais curta:

```swift
var shoppingList = ["Eggs", "Milk"]
```

Como todos os valores no literal de _array_ são do mesmo tipo, 
é possivel inferir que `[String]` é o tipo correto a ser usado para a variável `shoppingList`.

### Acessando e Modificando um Array

Você acessa e modifica um array por meio de seus métodos e propriedades ou usando a sintaxe de subscrito.

Para descobrir o número de itens em um array, verifique sua propriedade `count` que é somente de leitura:

```swift
print("The shopping list contains \(shoppingList.count) items.")
// Imprime "The shopping list contains 2 items."
```

Use a propriedade booleana `isEmpty` como um atalho para verificar se a propriedade `count` é igual a `0`:

```swift
if shoppingList.isEmpty {
   print("The shopping list is empty.")
} else {
   print("The shopping list isn't empty.")
}
// Imprime "The shopping list isn't empty."
```

Você pode adicionar um novo item ao final de um array chamando o método `append(_:)` do array:

```swift
shoppingList.append("Flour")
// shoppingList agora contém 3 itens e alguém está fazendo panquecas
```

Alternativamentea, anexe um array de um ou mais itens compatíveis com o operador de atribuição de adição (`+=`):

```swift
shoppingList += ["Baking Powder"]
// shoppingList agora contém 4 itens
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList agora contém 7 itens
```

Recupere um valor do array usando *sintaxe de subscrito*, passando o índice do valor que deseja recuperar entre colchetes imediatamente após o nome do array:

```swift
var firstItem = shoppingList[0]
// firstItem é igual a "Eggs"
```

> Nota: O primeiro item no array tem um índice de `0`, não `1`. Arrays em Swift são sempre indexados por zero.

Você pode usar a sintaxe de subscrito para alterar um valor existente em um determinado índice:

```swift
shoppingList[0] = "Six eggs"
// o primeiro item da lista agora é igual a "Six eggs" em vez de "Eggs"
```

Ao usar a sintaxe de subscrito, o índice especificado precisa ser válido. 
Por exemplo, escrever `shoppingList[shoppingList.count] = "Salt"` 
para tentar anexar um item ao final do _array_ resulta em um erro em tempo de execução.

Você também pode usar a sintaxe de subscrito para alterar um intervalo de valores de uma só vez, 
mesmo se o conjunto de valores de substituição tiver um comprimento diferente do intervalo que você está substituindo. 
O exemplo a seguir substitui `"Chocolate Spread"`, `"Cheese"` e `"Butter"` por `"Bananas"` e `"Apples"`:

```swift
shoppingList[4...6] = ["Bananas", "Apples"]
// `shoppingList` agora contém 6 itens
```

Para inserir um item no _array_ em um índice especificado, chame o método `insert(_:at:)`:

```swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList agora contém 7 itens
// "Maple Syrup" é agora o primeiro item da lista
```

Essa chamada para o método `insert(_:at:)` insere um novo item com um valor de `"Maple Syrup"` 
bem no início da lista de compras, indicado por um índice de `0`.

Da mesma forma, você remove um item do array com o método `remove(at:)`. 
Este método remove o item no índice especificado e retorna o item removido 
(embora você possa ignorar o valor retornado se não precisar dele):

```swift
let mapleSyrup = shoppingList.remove(at: 0)
// o item que estava no índice 0 foi removido
// `shoppingList` agora contém 6 itens, sem "Maple Syrup"
// a constante `mapleSyrup` agora é igual a string "Maple Syrup" removida
```

> Nota: Se você tentar acessar ou modificar um valor para um índice que está fora dos limites existentes de um _array_, 
> você irá disparar um erro de tempo de execução. 
> Você pode verificar se um índice é válido antes de usá-lo, comparando-o com a propriedade `count` do _array_. 
> O maior índice válido em uma _array_ é `count - 1` porque _arrays_ são indexados a partir de zero --- 
> no entanto, quando `count` é `0` (o que significa que o _array_ está vazio), não há índices válidos.

Quaisquer lacunas em um _array_ são fechadas quando um item é removido e, 
portanto, o valor no índice `0` é novamente igual a `"Six eggs"`:

```swift
firstItem = shoppingList[0]
// `firstItem` é igual a "Six eggs"
```

Se você deseja remover o item final de um _array_, use o método `removeLast()` em vez do método `remove(at:)` 
para evitar a necessidade de consultar a propriedade `count` do _array_.
Como o método `remove(at:)`, `removeLast()` retorna o item removido:

```swift
let apples = shoppingList.removeLast()
// O último item do array foi removido
// `shoppingList` agora contém 5 itens
// a constante apples é igual a string "Apples" removida
```

### Iterando sobre um Array

Você pode iterar sobre todos os valores em um _array_ com o _loop_ `for`-`in`:

```swift
for item in shoppingList {
   print(item)
}
// Six eggs
// Milk
// Flour
// Baking Powder
// Bananas
```

Se você precisar do índice inteiro de cada item, bem como de seu valor, use o método `enumerated()` para iterar sobre o _array_. 
Para cada item no _array_, o método `enumerated()` retorna uma tupla composta por um inteiro e o item. 
Os inteiros começam em zero e contam para cima em um para cada item; 
se você enumerar sobre todo um _array_, esses inteiros corresponderão aos índices dos itens. 
Você pode decompor a tupla em constantes ou variáveis temporárias como parte da iteração:

```swift
for (index, value) in shoppingList.enumerated() {
   print("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```

Para saber mais sobre o loop `for`-`in`, consulte <doc:ControlFlow#For-In-Loops>.

## Sets

Um **set** armazena valores distintos do mesmo tipo
em uma coleção sem ordenação definida.
Você pode usar um _set_ em vez de um _array_ quando a ordem dos itens não for importante,
ou quando você precisar garantir que um item apareça apenas uma vez.

> Nota: O tipo `Set` em Swift é conectado à classe `NSSet` do Foundation. Para obter mais informações sobre o uso de `Set` com Foundation e Cocoa,
> consulte [Conexão entre Set e NSSet](https://developer.apple.com/documentation/swift/set#2845530).

### Valores de Hash para Sets

Um tipo deve ser **hasháveis** para ser armazenado em um _set_ ---
ou seja, o tipo deve fornecer uma maneira de calcular um **valor de _hash_** para si mesmo.
Um valor de _hash_ é um valor `Int` que é o mesmo para todos os objetos que se comparam igualmente,
de modo que se `a == b`,
o valor de_ hash_ de `a` é igual ao valor de _hash_ de `b`.

Todos os tipos básicos em Swift (como `String`, `Int`, `Double` e `Bool`)
são hasháveis ​​por padrão e podem ser usados ​​como tipos de valor de _set_ ou tipos de chave de dicionário.
Valores de caso de enumeração sem valores associados
(conforme descrito em <doc:Enumerations>)
também são hasháveis ​​por padrão.

> Nota: você pode usar seus próprios tipos personalizados como elementos de um _set_ ou chaves de dicionários
> tornando-os conformes ao protocolo `Hashable`
> da biblioteca padrão.
> Para obter informações sobre a implementação do método `hash(into:)` necessário,
> consulte [`Hashable`](https://developer.apple.com/documentation/swift/hashable).
> Para obter informações sobre conformidade com protocolos, consulte <doc:Protocols>.

### Sintaxe de _Set_

O tipo de um _set_ é escrito como `Set<Element>`,
onde `Element` é o tipo que o _set_ tem permissão para armazenar.
Ao contrário de _arrays_, _sets_ não têm uma forma abreviada equivalente.

### Criando e Inicializando um _Set_ Vazio

Você pode criar um _set_ vazio de um certo tipo
usando a sintaxe de inicializador:

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Imprime "letters is of type Set<Character> with 0 items."
```

> Nota: O tipo da variável `letters` é inferido como `Set<Character>`,
> a partir do tipo do inicializador.

Alternativamente, se o contexto já fornece informações de tipo,
como um argumento de função ou uma variável ou constante já digitada,
você pode criar um _set_ vazio com um literal de _array_ vazio:

```swift
letters.insert("a")
// `letters` agora contém 1 valor do tipo `Character`
letters = []
// `letters` agora está vazio, mas ainda é do tipo `Set<Character>`
```

### Criando um _Set_ a partir de um Literal de _Array_

Você também pode inicializar um _set_ com um literal de _array_,
como uma forma abreviada de escrever um ou mais valores como um _set_.

O exemplo abaixo cria um _set_ chamado `favoriteGenres` para armazenar valores do tipo `String`:

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// `favoriteGenres` foi initializado com três items iniciais
```

A variável `favoriteGenres` é declarada como
“um _set_ de valores `String`”, escrito como `Set<String>`.
Como esse _set_ em particular especificou um tipo de valor `String`,
ele *somente* tem permissão para armazenar valores `String`.
Aqui, o _set_ `favoriteGenres` é inicializado com três valores `String`
(`"Rock"`, `"Classical"` e `"Hip hop"`), escritos dentro de um literal de array.

> Nota: O _set_ `favoriteGenres` é declarado como uma variável (com `var`)
> e não uma constante (com `let`)
> porque itens são adicionados e removidos nos exemplos abaixo.

Um _set_ não pode ser inferido de um literal de _array_ sozinho,
então o tipo `Set` deve ser declarado explicitamente.
No entanto, por causa da inferência de tipo,
você não precisa escrever o tipo dos elementos do _set_
se estiver inicializando-o com um literal de _array_
que contém valores de apenas um tipo.
A inicialização de `favoriteGenres` poderia ter sido escrita em uma forma mais curta:

```swift
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

Como todos os valores no literal da _array_ são do mesmo tipo,
O compilador consegue inferir que `Set<String>` é
o tipo correto a ser usado para a variável `favoriteGenres`.

### Acessando e Modificando um _Set_

Você acessa e modifica um _set_ por meio de seus métodos e propriedades.

Para descobrir o número de itens em um _set_,
verifique sua propriedade `count`:

```swift
print("I have \(favoriteGenres.count) favorite music genres.")
// Imprime "I have 3 favorite music genres."
```

Use a propriedade booleana `isEmpty`
como um atalho para verificar se a propriedade `count` é igual a `0`:

```swift
if favoriteGenres.isEmpty {
   print("As far as music goes, I'm not picky.")
} else {
   print("I have particular music preferences.")
}
// Imprime "I have particular music preferences."
```

Você pode adicionar um novo item a um _set_ chamando o método `insert(_:)`:

```swift
favoriteGenres.insert("[Tool J]")
// `favoriteGenres` agora contém 4 itens
```

Você pode remover um item de um _set_ chamando o método `remove(_:)`,
que remove o item se ele for um membro do _set_,
e retorna o valor removido,
ou retorna `nil` se o _set_ não o conter.
Como alternativa, todos os itens em um _set_ podem ser removidos com seu método `removeAll()`.

```swift
if let removedGenre = favoriteGenres.remove("Rock") {
   print("\(removedGenre)? I'm over it.")
} else {
   print("I never much cared for that.")
}
// Imprime "Rock? I'm over it."
```

Para verificar se um _set_ contém um item específico, use o método `contains(_:)`.

```swift
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// Imprime "It's too funky in here."
```

### Iterando Sobre um _Set_

Você pode iterar sobre os valores em um _set_ com um loop `for`-`in`.

```swift
for genre in favoriteGenres {
   print("\(genre)")
}
// Classical
// [Tool J]
// Hip hop
```

Para mais informações sobre o loop `for`-`in`, consulte <doc:ControlFlow#For-In-Loops>.

O tipo `Set` não tem uma ordenação definida.
Para iterar sobre os valores de um _set_ em uma ordem específica,
use o método `sorted()`,
que retorna os elementos do _set_ como um _array_
ordenado usando o operador `<`.

```swift
for genre in favoriteGenres.sorted() {
   print("\(genre)")
}
// Classical
// Hip hop
// [Tool J]
```

## Executando Operações de _Set_

Você pode executar com eficiência operações fundamentais de _sets_,
como combinar dois _sets_,
determinar quais valores dois _sets_ têm em comum,
ou determinar se dois _sets_ contêm todos, alguns ou nenhum dos mesmos valores.

### Operações Fundamentais de _Set_

A ilustração abaixo descreve dois _sets_ --- `a` e `b` ---
com os resultados de várias operações de _set_ representados pelas regiões sombreadas.

![](setVennDiagram)

- Use o método `intersection(_:)` para criar um novo _set_ com apenas os valores comuns a ambos os _sets_.
- Use o método `symmetricDifference(_:)` para criar um novo _set_ com valores em qualquer _set_, mas não em ambos.
- Use o método `union(_:)` para criar um novo _set_ com todos os valores em ambos os _sets_.
- Use o método `subtracting(_:)` para criar um novo _set_ com valores que não estão no _set_ especificado.

```swift
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]
```

### Associação e Igualdade de _Sets_

A ilustração abaixo descreve três _sets_ ---`a`, `b` e `c`---
com regiões sobrepostas representando elementos compartilhados entre os _sets_.
O _set_ `a` é um ***superset*** do _set_ `b`,
porque `a` contém todos os elementos em `b`.
Por outro lado, o _set_ `b` é um ***subset*** de `a`,
porque todos os elementos em `b` também são contidos por `a`.
O _set_ `b` e o _set_ `c` são **disjuntos** um com o outro,
porque eles não compartilham nenhum elemento em comum.

![](setEulerDiagram)

- Use o operador "é igual" (`==`) para determinar se dois _sets_ contêm todos os mesmos valores.
- Use o método `isSubset(of:)` para determinar se todos os valores de um _set_ estão contidos no _set_ especificado.
- Use o método `isSuperset(of:)` para determinar se um _set_ contém todos os valores em um _set_ especificado.
- Use os métodos `isStrictSubset(of:)` ou `isStrictSuperset(of:)` para determinar se um _set_ é um _subset_ ou _superset_, mas não igual a, um _set_ especificado.
- Use o método `isDisjoint(with:)` para determinar se dois _sets_ não têm valores em comum.

```swift
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```

## Dictionaries

A *dictionary* stores associations between
keys of the same type and values of the same type
in a collection with no defined ordering.
Each value is associated with a unique *key*,
which acts as an identifier for that value within the dictionary.
Unlike items in an array, items in a dictionary don't have a specified order.
You use a dictionary when you need to look up values based on their identifier,
in much the same way that a real-world dictionary is used to look up
the definition for a particular word.

> Note: Swift's `Dictionary` type is bridged to Foundation's `NSDictionary` class.For more information about using `Dictionary` with Foundation and Cocoa,
> see [Bridging Between Dictionary and NSDictionary](https://developer.apple.com/documentation/swift/dictionary#2846239).

### Dictionary Type Shorthand Syntax

The type of a Swift dictionary is written in full as `Dictionary<Key, Value>`,
where `Key` is the type of value that can be used as a dictionary key,
and `Value` is the type of value that the dictionary stores for those keys.

> Note: A dictionary `Key` type must conform to the `Hashable` protocol,
> like a set's value type.

You can also write the type of a dictionary in shorthand form as `[Key: Value]`.
Although the two forms are functionally identical,
the shorthand form is preferred
and is used throughout this guide when referring to the type of a dictionary.

### Creating an Empty Dictionary

As with arrays,
you can create an empty `Dictionary` of a certain type by using initializer syntax:

```swift
var namesOfIntegers: [Int: String] = [:]
// namesOfIntegers is an empty [Int: String] dictionary
```




This example creates an empty dictionary of type `[Int: String]`
to store human-readable names of integer values.
Its keys are of type `Int`, and its values are of type `String`.

If the context already provides type information,
you can create an empty dictionary with an empty dictionary literal,
which is written as `[:]`
(a colon inside a pair of square brackets):

```swift
namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type [Int: String]
```




### Creating a Dictionary with a Dictionary Literal

You can also initialize a dictionary with a *dictionary literal*,
which has a similar syntax to the array literal seen earlier.
A dictionary literal is a shorthand way to write
one or more key-value pairs as a `Dictionary` collection.

A *key-value pair* is a combination of a key and a value.
In a dictionary literal,
the key and value in each key-value pair are separated by a colon.
The key-value pairs are written as a list, separated by commas,
surrounded by a pair of square brackets:

```
[<#key 1#>: <#value 1#>, <#key 2#>: <#value 2#>, <#key 3#>: <#value 3#>]
```


The example below creates a dictionary to store the names of international airports.
In this dictionary, the keys are three-letter International Air Transport Association codes,
and the values are airport names:

```swift
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```




The `airports` dictionary is declared as having a type of `[String: String]`,
which means “a `Dictionary` whose keys are of type `String`,
and whose values are also of type `String`”.

> Note: The `airports` dictionary is declared as a variable (with the `var` introducer),
> and not a constant (with the `let` introducer),
> because more airports are added to the dictionary in the examples below.

The `airports` dictionary is initialized with
a dictionary literal containing two key-value pairs.
The first pair has a key of `"YYZ"` and a value of `"Toronto Pearson"`.
The second pair has a key of `"DUB"` and a value of `"Dublin"`.

This dictionary literal contains two `String: String` pairs.
This key-value type matches the type of the `airports` variable declaration
(a dictionary with only `String` keys, and only `String` values),
and so the assignment of the dictionary literal is permitted
as a way to initialize the `airports` dictionary with two initial items.

As with arrays,
you don't have to write the type of the dictionary
if you're initializing it with a dictionary literal whose keys and values have consistent types.
The initialization of `airports` could have been written in a shorter form instead:

```swift
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```




Because all keys in the literal are of the same type as each other,
and likewise all values are of the same type as each other,
Swift can infer that `[String: String]` is
the correct type to use for the `airports` dictionary.

### Accessing and Modifying a Dictionary

You access and modify a dictionary through its methods and properties,
or by using subscript syntax.

As with an array, you find out the number of items in a `Dictionary`
by checking its read-only `count` property:

```swift
print("The airports dictionary contains \(airports.count) items.")
// Prints "The airports dictionary contains 2 items."
```




Use the Boolean `isEmpty` property
as a shortcut for checking whether the `count` property is equal to `0`:

```swift
if airports.isEmpty {
   print("The airports dictionary is empty.")
} else {
   print("The airports dictionary isn't empty.")
}
// Prints "The airports dictionary isn't empty."
```




You can add a new item to a dictionary with subscript syntax.
Use a new key of the appropriate type as the subscript index,
and assign a new value of the appropriate type:

```swift
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
```




You can also use subscript syntax to change the value associated with a particular key:

```swift
airports["LHR"] = "London Heathrow"
// the value for "LHR" has been changed to "London Heathrow"
```




As an alternative to subscripting,
use a dictionary's `updateValue(_:forKey:)` method
to set or update the value for a particular key.
Like the subscript examples above, the `updateValue(_:forKey:)` method
sets a value for a key if none exists,
or updates the value if that key already exists.
Unlike a subscript, however,
the `updateValue(_:forKey:)` method returns the *old* value after performing an update.
This enables you to check whether or not an update took place.

The `updateValue(_:forKey:)` method returns an optional value
of the dictionary's value type.
For a dictionary that stores `String` values, for example,
the method returns a value of type `String?`,
or “optional `String`”.
This optional value contains the old value for that key if one existed before the update,
or `nil` if no value existed:

```swift
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
   print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."
```




You can also use subscript syntax to retrieve a value from the dictionary for a particular key.
Because it's possible to request a key for which no value exists,
a dictionary's subscript returns an optional value of the dictionary's value type.
If the dictionary contains a value for the requested key,
the subscript returns an optional value containing the existing value for that key.
Otherwise, the subscript returns `nil`:

```swift
if let airportName = airports["DUB"] {
   print("The name of the airport is \(airportName).")
} else {
   print("That airport isn't in the airports dictionary.")
}
// Prints "The name of the airport is Dublin Airport."
```




You can use subscript syntax to remove a key-value pair from a dictionary
by assigning a value of `nil` for that key:

```swift
airports["APL"] = "Apple International"
// "Apple International" isn't the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary
```




Alternatively, remove a key-value pair from a dictionary
with the `removeValue(forKey:)` method.
This method removes the key-value pair if it exists
and returns the removed value,
or returns `nil` if no value existed:

```swift
if let removedValue = airports.removeValue(forKey: "DUB") {
   print("The removed airport's name is \(removedValue).")
} else {
   print("The airports dictionary doesn't contain a value for DUB.")
}
// Prints "The removed airport's name is Dublin Airport."
```




### Iterating Over a Dictionary

You can iterate over the key-value pairs in a dictionary with a `for`-`in` loop.
Each item in the dictionary is returned as a `(key, value)` tuple,
and you can decompose the tuple's members into temporary constants or variables
as part of the iteration:

```swift
for (airportCode, airportName) in airports {
   print("\(airportCode): \(airportName)")
}
// LHR: London Heathrow
// YYZ: Toronto Pearson
```




For more about the `for`-`in` loop, see <doc:ControlFlow#For-In-Loops>.

You can also retrieve an iterable collection of a dictionary's keys or values
by accessing its `keys` and `values` properties:

```swift
for airportCode in airports.keys {
   print("Airport code: \(airportCode)")
}
// Airport code: LHR
// Airport code: YYZ

for airportName in airports.values {
   print("Airport name: \(airportName)")
}
// Airport name: London Heathrow
// Airport name: Toronto Pearson
```




If you need to use a dictionary's keys or values
with an API that takes an `Array` instance, initialize a new array
with the `keys` or `values` property:

```swift
let airportCodes = [String](airports.keys)
// airportCodes is ["LHR", "YYZ"]

let airportNames = [String](airports.values)
// airportNames is ["London Heathrow", "Toronto Pearson"]
```




Swift's `Dictionary` type doesn't have a defined ordering.
To iterate over the keys or values of a dictionary in a specific order,
use the `sorted()` method on its `keys` or `values` property.



