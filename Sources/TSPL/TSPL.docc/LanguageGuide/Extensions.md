

# Extensões

*Extensões* adicionam novas funcionalidades a uma classe, estrutura, enumeração ou tipo de protocolo existente. Isso inclui a capacidade de estender tipos para os quais você não tem acesso ao código-fonte original (conhecido como *modelagem retroativa*). As extensões são semelhantes às categorias em Objective-C. (Ao contrário das categorias de Objective-C, as extensões Swift não têm nomes.)

Extensões no Swift podem:

- Adicionar propriedades de instância computadas e propriedades de tipo computado
- Definir métodos de instância e métodos de tipo
- Fornecer novos inicializadores
- Definir subscritos
- Definir e usar novos tipos aninhados
- Deixar um tipo existente em conformidade com um protocolo

Em Swift, você pode, inclusive, estender um protocolo para fornecer implementações de seus requisitos
ou adicionar funcionalidades extras que os tipos em conformidade podem aproveitar. Para mais detalhes, consulte <doc:Protocols#Protocol-Extensions>.

> Nota: As extensões podem adicionar novas funcionalidades a um tipo, mas eles não podem substituir a funcionalidade existente.


## Sintaxe de Extensão

Declare extensões com a palavra-chave `extension`:

```swift
extension SomeType {
   // nova funcionalidade para adicionar a 'SomeType' vai aqui
}
```

Uma extensão pode estender um tipo existente para que ele adote um ou mais protocolos. Para adicionar conformidade de protocolo, você escreve os nomes dos protocolos da mesma maneira que você os escreve para uma classe ou estrutura:

```swift
extension SomeType: SomeProtocol, AnotherProtocol {
   // implementação de requisitos do protocolo vai aqui
}
```

A adição de conformidade de protocolo dessa maneira é descrita em <doc:Protocols#Adding-Protocol-Conformance-with-an-Extension>.

Uma extensão pode ser usada para estender um tipo genérico existente, como descrito em <doc:Generics#Extending-a-Generic-Type>.
Você também pode estender um tipo genérico para adicionar funcionalidade condicionalmente, conforme descrito em <doc:Generics#Extensions-with-a-Generic-Where-Clause>.

> Nota: Se você definir uma extensão para adicionar uma nova funcionalidade a um tipo existente, a nova funcionalidade estará disponível em todas as instâncias existentes desse tipo, mesmo que tenham sido criadas antes da definição da extensão.

## Propriedades Computadas

Extensões podem adicionar propriedades computadas de instância e propriedades computadas de tipo a tipos existentes. 
Este exemplo adiciona cinco propriedades computadas de instância ao tipo built-in `_Double_` do Swift,
para fornecer suporte básico para trabalhar com unidades de distância:

```swift
extension Double {
   var km: Double { return self * 1_000.0 }
   var m: Double { return self }
   var cm: Double { return self / 100.0 }
   var mm: Double { return self / 1_000.0 }
   var ft: Double { return self / 3.28084 }
}
let oneInch = 25.4.mm
print("Uma polegada é \(oneInch) metros")
// imprime "Uma polegada é 0.0254 metros"
let threeFeet = 3.ft
print("Três pés é \(threeFeet) metros")
// Imprime "Três pés é 0.914399970739201 metros"
```

Estas propriedades computadas expressam que o valor de um `Double`
deve ser considerado como uma certa unidade de comprimento.
Apesar de serem implementadas como propriedades computadas,
os nomes destas propriedades podem ser anexados a um
literal de ponto flutuante com sintaxe de ponto,
como uma forma de usar aquele valor literal para realizar conversões a distância.

Neste exemplo, um `Double` de valor `1.0` é coonsiderado para representar "um metro".
E é por isso que a propriedade computada `m` reforta `self` ---
a expressão `1.m` é considerada para calcular um `Double`de valor `1.0`.

Outras unidades requerem alguma conversão para serem expressas como um valor medido em metros. 
Um quilometro é mesma coisa de 1.000 metros,
então a propriedade computada `km` multiplica o valor por `1_000.00`
para convertê-lo em um numero expresso em metros. 
Similarmente, temos 3,28084 pés em metros,
e então a propriedade computada `ft` divide o valor "Double" subjacente
por  `3.28084` para convertê-lo de pés para metros. 

Essas propriedades são propriedades computadas apenas de leitura,
então elas são expressadas sem a palavra-chave `get`, para fins de abreviação. 
Seu retorno é do tipo `Double	` e pode ser
usado dentro de cálculos matemáticos sempre que um `Double` é aceito:

```swift
let aMarathon = 42.km + 195.m
print("A marathon is \(aMarathon) meters long")
// Prints "A marathon is 42195.0 meters long"
```

> Note: Extensões podem adicionar notas propriedades cmoputadas, mas não podem
> propriedades guardadas ou adicionar observadores em propriedades existentes.


## Initializers

Extensions can add new initializers to existing types.
This enables you to extend other types to accept
your own custom types as initializer parameters,
or to provide additional initialization options
that were not included as part of the type's original implementation.

Extensions can add new convenience initializers to a class,
but they can't add new designated initializers or deinitializers to a class.
Designated initializers and deinitializers
must always be provided by the original class implementation.

If you use an extension to add an initializer to a value type that provides
default values for all of its stored properties
and doesn't define any custom initializers,
you can call the default initializer and memberwise initializer for that value type
from within your extension's initializer.
This wouldn't be the case if you had written the initializer
as part of the value type's original implementation,
as described in <doc:Initialization#Initializer-Delegation-for-Value-Types>.

If you use an extension to add an initializer to a structure
that was declared in another module,
the new initializer can't access `self` until it calls
an initializer from the defining module.

The example below defines a custom `Rect` structure to represent a geometric rectangle.
The example also defines two supporting structures called `Size` and `Point`,
both of which provide default values of `0.0` for all of their properties:

```swift
struct Size {
   var width = 0.0, height = 0.0
}
struct Point {
   var x = 0.0, y = 0.0
}
struct Rect {
   var origin = Point()
   var size = Size()
}
```




Because the `Rect` structure provides default values for all of its properties,
it receives a default initializer and a memberwise initializer automatically,
as described in <doc:Initialization#Default-Initializers>.
These initializers can be used to create new `Rect` instances:

```swift
let defaultRect = Rect()
let memberwiseRect = Rect(origin: Point(x: 2.0, y: 2.0),
   size: Size(width: 5.0, height: 5.0))
```




You can extend the `Rect` structure to provide an additional initializer
that takes a specific center point and size:

```swift
extension Rect {
   init(center: Point, size: Size) {
      let originX = center.x - (size.width / 2)
      let originY = center.y - (size.height / 2)
      self.init(origin: Point(x: originX, y: originY), size: size)
   }
}
```




This new initializer starts by calculating an appropriate origin point based on
the provided `center` point and `size` value.
The initializer then calls the structure's automatic memberwise initializer
`init(origin:size:)`, which stores the new origin and size values
in the appropriate properties:

```swift
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
   size: Size(width: 3.0, height: 3.0))
// centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
```




> Note: If you provide a new initializer with an extension,
> you are still responsible for making sure that each instance is fully initialized
> once the initializer completes.

## Methods

Extensions can add new instance methods and type methods to existing types.
The following example adds a new instance method called `repetitions` to the `Int` type:

```swift
extension Int {
   func repetitions(task: () -> Void) {
      for _ in 0..<self {
         task()
      }
   }
}
```




The `repetitions(task:)` method takes a single argument of type `() -> Void`,
which indicates a function that has no parameters and doesn't return a value.

After defining this extension,
you can call the `repetitions(task:)` method on any integer
to perform a task that many number of times:

```swift
3.repetitions {
   print("Hello!")
}
// Hello!
// Hello!
// Hello!
```




### Mutating Instance Methods

Instance methods added with an extension can also modify (or *mutate*) the instance itself.
Structure and enumeration methods that modify `self` or its properties
must mark the instance method as `mutating`,
just like mutating methods from an original implementation.

The example below adds a new mutating method called `square` to Swift's `Int` type,
which squares the original value:

```swift
extension Int {
   mutating func square() {
      self = self * self
   }
}
var someInt = 3
someInt.square()
// someInt is now 9
```




## Subscripts

Extensions can add new subscripts to an existing type.
This example adds an integer subscript to Swift's built-in `Int` type.
This subscript `[n]` returns the decimal digit `n` places in
from the right of the number:

- `123456789[0]` returns `9`
- `123456789[1]` returns `8`

…and so on:

```swift
extension Int {
   subscript(digitIndex: Int) -> Int {
      var decimalBase = 1
      for _ in 0..<digitIndex {
         decimalBase *= 10
      }
      return (self / decimalBase) % 10
   }
}
746381295[0]
// returns 5
746381295[1]
// returns 9
746381295[2]
// returns 2
746381295[8]
// returns 7
```








If the `Int` value doesn't have enough digits for the requested index,
the subscript implementation returns `0`,
as if the number had been padded with zeros to the left:

```swift
746381295[9]
// returns 0, as if you had requested:
0746381295[9]
```








## Nested Types

Extensions can add new nested types to existing classes, structures, and enumerations:

```swift
extension Int {
   enum Kind {
      case negative, zero, positive
   }
   var kind: Kind {
      switch self {
         case 0:
            return .zero
         case let x where x > 0:
            return .positive
         default:
            return .negative
      }
   }
}
```




This example adds a new nested enumeration to `Int`.
This enumeration, called `Kind`,
expresses the kind of number that a particular integer represents.
Specifically, it expresses whether the number is
negative, zero, or positive.

This example also adds a new computed instance property to `Int`,
called `kind`,
which returns the appropriate `Kind` enumeration case for that integer.

The nested enumeration can now be used with any `Int` value:

```swift
func printIntegerKinds(_ numbers: [Int]) {
   for number in numbers {
      switch number.kind {
         case .negative:
            print("- ", terminator: "")
         case .zero:
            print("0 ", terminator: "")
         case .positive:
            print("+ ", terminator: "")
      }
   }
   print("")
}
printIntegerKinds([3, 19, -27, 0, -6, 0, 7])
// Prints "+ + - 0 - 0 + "
```






This function, `printIntegerKinds(_:)`,
takes an input array of `Int` values and iterates over those values in turn.
For each integer in the array,
the function considers the `kind` computed property for that integer,
and prints an appropriate description.

> Note: `number.kind` is already known to be of type `Int.Kind`.
> Because of this, all of the `Int.Kind` case values
> can be written in shorthand form inside the `switch` statement,
> such as `.negative` rather than `Int.Kind.negative`.



