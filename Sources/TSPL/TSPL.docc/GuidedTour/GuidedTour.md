

# Um guia de Swift

A tradição sugere que o primeiro programa em uma nova linguagem  deve imprimir a frase "Olá, mundo!" na tela.
Em Swift, esta pode ser feita em uma simples linha:

```swift
print("Olá, mundo!")
// imprime "Olá, mundo!"
```

Se você já escreveu códigos em C ou Objective-C,
esta sitaxe parecerá familiar para você ---
em Swift, esta linha de código é um programa completo.
Você não precisa importar uma biblioteca à parte para uma funcionalidade como entrada e saída ou manipulação de uma string.
O código escrito em um escopo global é usado como ponto inicial para o programa, então você não precisa de uma função `main()`.
Você também não precisa escrever ponto e vírgula no final de cada declaração.

Este guia lhe dá informações suficientes
para começar a escrever códigos em Swift, mostrando como realizar uma variedade de tarefas de programação.
Não se preocupe se você não entender alguma coisa ---
tudo o que for introduzido neste guia será explicado em detalhes neste livro.

## Valores Simples

Use `let` para criar uma constante e `var` para criar uma variável.
O valor de uma constante não precisa ser sabido no momento do código ser compilado. mas você deve atribuí-la um valor somente uma vez. Isso significa que você pode usar constantes para nomear um valor que você determinou uma vez, mas utiliza em muitos lugares.

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```




A constante ou variável deve ser do mesmo tipo do valor que você quer atribuir a ela. Entretanto, você nem sempre precisa atribuir o tipo de forma explícita. 
Dar um valor à constante ou variável no momento de sua criação faz com que o compilador infira qual o seu tipo. No exemplo acima, o compilador irá inferir que a `myVariable` é um inteiro, pois o seu valor inicial é um inteiro. Se o valor inicial não entrega informação suficiente (ou se não foi atribuído nenhum valor inicial), especifique o tipo escrevendo-o logo depois da variável, separado por dois pontos. 

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```




> Experimente: Crie uma constante com o tipo `Float` explícito e de valor `4`.

Valores nunca são implicitamente convertidos para outro tipo. Se você precisar converter um valor para um tipo diferente, faça uma instância explicitamente do tipo desejado. 

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```




> Experimente: Tente remover a conversão para `String` da última linha
> Que tipo de erro dá?



Existe uma forma ainda mais simples de incluir valores em uma string: escreva o valor em parênteses com uma barra invertida (`\`) antes do primeiro parêntese. Por exemplo:

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```




> Experimente: Use `\()` para incluir um cálculo de floating-point em uma string e para incluir o nome de alguém em uma saudação.

Use três aspas duplas para strings que pegam múltiplas linhas. A indentação no começo de cada linha de texto será removida, caso seja a mesma das aspas fechando. 
Por exemplo:

```swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```






Crie arrays e dicionários usando colchetes (`[]`), e acesse seus elementos escrevendo o índex ou chave também entre colchetes. A vírgula após o último elemento é permitida. 





```swift
var fruits = ["strawberries", "limes", "tangerines"]
fruits[1] = "grapes"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
 ]
occupations["Jayne"] = "Public Relations"
```




Os Arrays crescem automaticamente quando você adiciona elementos a eles. 

```swift
fruits.append("blueberries")
print(fruits)
```




Para criar um array ou dicionário vazio, use a sintaxe de inicialização.

```swift
let emptyArray: [String] = []
let emptyDictionary: [String: Float] = [:]
```




Se o tipo da informação pode ser inferido, você pode escrever um array vazio com `[]` e um dicionário vazio com `[:]`. Por exemplo, quando você configura um novo valor para uma variável ou passa um argumento para uma função.




```swift
fruits = []
occupations = [:]
```




## Controle de Fluxo

`## Controle de Fluxo

Use `if` e `switch` para fazer condicionais,
e use `for`-`in`, `while`, e `repeat`-`while`
para criar loops.
É opcional inserir as condicionais ou variáveis de loop entre parênteses. 
É obrigatório inserir o texto _body_ entre chaves.

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Prints "11"
```








Em uma declaração `if`,
a condicional deve ser uma expressão booleana ---
isso significa que o código como `if score { ... }` é um erro,
não é uma comparação implicita à zero.

Você pode usar ‘if’ e ‘let’ juntos
para trabalhar com valores que podem estar ausentes.
Esses valores são representados como opcionais.
Um valor opcional contém um valor
ou contém `nil`para indicar um valor ausente.
Insira um ponto de interrogação, em seguida, digite um valor
para marcá-lo como opcional.





```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Prints "false"

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```




> Experimente: Altere `optionalName` para `nil`.
> Qual saudação você recebe?
> Insira `else` para definir uma saudação diferente
> Se `optionalName` é `nil`.

Se o valor opcional é `nil`,
a condicional é ‘false’ e o código nas chaves são pulados
Caso contrário, o valor opcional é desempacotado e atribuído,
para a constant edepois de ‘let’
o que faz o valor desempacotado ficar disponível
dentro do bloco de código.

Outra maneira de lidar com os valores opcionais
é provendo um valor padrão usando o operador ‘??’.
Se o valor opcional está ausente,
o valor padrão é usado como substituto. 

```swift
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
```




You can use a shorter spelling to unwrap a value,
using the same name for that unwrapped value.

```swift
if let nickname {
    print("Hey, \(nickname)")
}
```




Switches suporta todos os tipos de dados
e uma grande variedade de operações de comparação —
sem limitação de inteiros
e testes para igualdade.



```swift
let vegetable = "red pepper"
switch vegetable {
    case "celery":
        print("Add some raisins and make ants on a log.")
    case "cucumber", "watercress":
        print("That would make a good tea sandwich.")
    case let x where x.hasSuffix("pepper"):
        print("Is it a spicy \(x)?")
    default:
        print("Everything tastes good in soup.")
}
// Prints "Is it a spicy red pepper?"
```




> Experimente: tente remover a  _default case_
> Qual o erro que foi percebido?

Perceba como ‘let’ pode ser usado em um padrão
para determinar o valor que combina o padrão
com a constante.

Depois de executar o código dentro do ’switch case’



Você usa `for`-`in`para integrar os itens em um dicionário
provendo um par names para usar
para cada par de chave de valor.
Dicionários são uma coleção não-ordenada
então, suas chaves e valores são integrados
em uma ordem arbritária



```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (_, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Prints "25"
```




> Experimente: Substitua `_` com o nome de uma variável,
> e acompanhe qual tipo de número foi maior.

Use `while` para repetir um bloco de código até a condição mudar.
As condições de um loop podem estar no final
assegurando que o loop será executado pelo menos uma vez.



```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Prints "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Prints "128"
```




Você pode manter um _index_ em loop
usando `..<` para criar uma série de _indexes_.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Prints "6"
```




Use `..<` para criar um intervalo que omite seu maior valor,
e use `...` para usar um intervalo que inclui ambos valores.

## Funções e *Closures*

Use `func` para declarar uma função.
Crie uma função seguindo seu nome
com uma lista de argumentos entre parênteses.
Use `->` para separar os nomes e tipos de parâmetros do tipo de retorno da função.



```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```




> Experimente: tente remover o parâmetro `day`.
> Adicione um parâmetro que inclua o almoço especial de hoje na saudação.

Por padrão,
funções usam seus nomes de parâmetros
como rótulos para seus argumentos.
Escreva um rótulo de argumento personalizado antes do nome do parâmetro,
ou escreva `_` para não usar nenhum rótulo de argumento.


```swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```





Use uma tupla para fazer um valor composto ---
por exemplo, para retornar vários valores de uma função.
Os elementos de uma tupla podem ser referenciados pelo
nome ou pelo número.




```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Imprime "120"
print(statistics.2)
// Imprime "120"
```




Funções podem ser aninhadas.
Funções aninhadas têm acesso a variáveis
que foram declaradas na função externa.
Você pode usá-las para organizar o código em funções
que são longas ou complexas.

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```





As funções são um tipo de primeira classe, o que significa que podem ter outra função como seu valor de retorno.

```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```




Uma função pode ter outra função como um de seus argumentos.

```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```




As funções são, na verdade, um caso especial de closures:
blocos de código que podem ser chamados posteriormente.
O código em uma *closure* tem acesso a coisas como variáveis e funções que estavam disponíveis no escopo de sua criação, ainda que a *clusore* esteja em um escopo diferente quando for executada, --- você viu um exemplo disso já com funções aninhadas.
Você pode escrever uma *closure* sem um nome, envolvendo o código com chaves (`{}`).
Use `in` para separar os argumentos e o tipo de retorno do corpo da *closure*.

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```




> Experimente: Reescreva essa *closure* para retornar zero para todos os números ímpares.

Você tem várias opções para escrever *closures* de forma mais concisa.
Quando o seu tipo já é conhecido,
como o retorno de uma chamada para um *delegate*,
você pode omitir o tipo de seus parâmetros,
seu tipo de retorno, ou ambos.
*Closures* de instrução única retornam implicitamente o valor
de sua única instrução.

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Imprime "[60, 57, 21, 36]"
```




Você pode se referir a parâmetros por número em vez de por nome ---
essa abordagem é especialmente útil em *closures* muito curtas.
Uma *closure* passada como o último argumento para uma função
pode aparecer logo após os parênteses.
Quando uma *closure* é o único argumento para uma função,
você pode omitir os parênteses.

```swift
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Imprime "[20, 19, 12, 7]"
```










## Objetos e Classes

Use `class` seguido do nome da classe para criar uma classe. Uma propriedade declarada dentro de uma classe é escrita da mesma que a declaração de uma variável ou constante, mas se encaixando no contexto daquela classe. Da mesma forma, declarações de métodos e funções também são escritos da mesma maneira.



```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```




> Experimente: Adicione uma propriedade constante com `let`,
> e adicione outro método que leve ela como argumento.

Crie uma instância de uma classe colocando parênteses depois do nome dela. Use a sintaxe ponto para acessar as propriedades e métodos daquela instancia.

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```





Nessa versão da classe `Shape`, está faltando algo importante: um inicializador para configurar a classe quando uma instância for criada. Use `init` para criar um inicializador.

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
       self.name = name
    }

    func simpleDescription() -> String {
       return "A shape with \(numberOfSides) sides."
    }
}
```




Note como `self` é usado para diferenciar a propriedade `name` do argumento `name` para o inicializador. Os argumentos, para o inicializador, são chamados como uma chamada de função quando você cria uma instancia de uma classe. Toda propriedade precisa ter um valor atribuído — seja na sua declaração (como em `numberOfSides`) ou no através do inicializador (como em `name`).

Use `deinit` para criar um desinicializador se você precisar realizar uma limpeza antes que o objeto seja deslocado.

Subclasses possuem o nome de sua superclasse após seu nome declarado, separado por dois pontos. Uma classe não tem a necessidade de herdar nenhuma das root classes, portanto você pode incluir ou omitir uma superclasse conforme for necessário.

Métodos em uma subclasse que sobrescrevem a implementação da superclasse são marcados com `override` — sobrescrever um método por acidente, sem o uso de `override`, é uma ação identificada pelo compilador como um erro. O compilador também identifica métodos com `override` que não sobrescrevem nenhum método na superclasse.


```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```




> Experimente: Crie outra subclasse de `NamedShape` chamada `Circle`, que pega o raio e o nome como argumentos do inicialiador. Implemente `area()`e `simpeDescription()`na classe `Circle`. 

Em adição às propriedades simples que são armazenadas, cada propriedade pode ter um getter e um setter.


```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
             return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// Prints "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Prints "3.3000000000000003"
```





No setter de `perimeter`, o novo valor tem o nome implícito `newValue`. Você pode dar a ele um nome explícito nos parênteses após `set`. Note que o inicializador para classe `EquilateralTriangle` possui três diferente passos:

- Definir o valor das propriedades declaradas pela subclasse
- Chamar o inicializador da superclasse
- Mudar o valor das propriedades definidas pela superclasse. Qualquer trabalho de configuração que use métodos, getters ou setters.

Se não houver necessidade de computar a propriedade, mas ainda for necessário fornecer um código que será executado antes e depois de ser definido um novo valor, use `willSet` e `didSet`. O código fornecido será executado em qualquer situação em que o valor for alterado fora de um inicializador. A classe abaixo, por exemplo, garante que a medida a lateral do triangulo seja sempre a mesma medida da lateral do quadrado.



```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
// Prints "10.0"
print(triangleAndSquare.triangle.sideLength)
// Prints "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// Prints "50.0"
```






Quando trabalhar com valores opcionais,  você pode usar `?` antes de operações como métodos, propriedades e subscrição . Se o valor antes de `?` for `nil`, tudo depois do sinal `?` é ignorado e o valor de toda expressão se torna `nil`. Caso contrário, o valor opcional é desempacotado, e tudo depois do sinal `?` age de acordo com o valor desempacotado. Em ambos os casos, o valor da expressão por inteiras é um valor opcional.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```




## Enumerações e Estruturas

Use `enum` para criar uma enumeração.
Como classes e todos os outros tipos, enumerações podem ter métodos associados a elas.



```swift
enum Posicao: Int {
    case aS = 1
    case dois, tres, quatro, cinco, seis, sete, oito, nove, dez
    case valete, rainha, rei

    func descricao() -> String {
        switch self {
            case .as:
                return "às"
            case .valete:
                return "valete"
            case .rainha:
                return "rainha"
            case .rei:
                return "rei"
            default:
                return String(self.rawValue)
        }
    }
}
let aS = Posicao.aS
let asRawValue = aS.rawValue
```


@Comment {
  - test: `guided-tour`
  
  ```swifttest
  -> enum Rank: Int {
         case ace = 1
         case two, three, four, five, six, seven, eight, nine, ten
         case jack, queen, king
  ---
         func descricao() -> String {
             switch self {
                 case .ace:
                     return "ace"
                 case .jack:
                     return "jack"
                 case .queen:
                     return "queen"
                 case .king:
                     return "king"
                 default:
                     return String(self.rawValue)
             }
         }
     }
  -> let as = Posicao.as
  -> let asDescricao = as.rawValue
  >> print(asDescricao)
  << 1
  ```
}


> Experimento: Escreva uma função que compare dois valores de Posicao
> comparando os seus `rawValue`.

Por padrão, Swift atribui os `rawValue` começando de zero e incrementando um de cada vez. 
No exemplo acima, `as` é explicitamente atribuído a um `rawValue` de 1 e o resto são atribuídos por ordem.
Também é possível utilizar cadeias de caracteres (Strings) ou números de ponto flutuante (Float) como o tipo de `rawValue` na enumeração.
Use o construtor `init?(rawValue:)` para criar uma enumeração a partir de um `rawValue`. Retorna o caso correspondente ou `nil` se não houver relação.


```swift
if let posicaoConvertida = Posicao(rawValue: 3) {
    let descricaoTres = posicaoConvertida.descricao()
}
```




Os valores de caso de uma enumeração são valores reais,
e não apenas outra forma de escrever os seus valores em bruto.
De fato, nos casos em que não existe contexto,
não é necessário fornecer um.

```swift
enum Naipe {
    case espadas, copas, ouros, paus

    func descricao() -> String {
        switch self {
            case .espadas:
                return "espadas"
            case .copas:
                return "copas"
            case .ouros:
                return "ouros"
            case .paus:
                return "paus"
        }
    }
}
let copas = Naipe.copas
let copasDescricao = copas.descricao()
```




> Experimento: Adicione um método `cor()` à `Naipe` que retorna "preto"
> para espadas e paus, e retorna "vermelho" para copas e ouros.



Repare nas duas maneiras que o caso "copas" da enumeração é referida acima:
Quando se atribui um valor à constante "copas",
o caso de enumeração `Naipe.copas` é referido pelo seu nome completo
porque a constante não tem um tipo explícito especificado.
Dentro do switch,
o caso de enumeração é referido pela forma abreviada `.copas`.
porque o valor de `self` já é conhecido por ser um fato.
Pode utilizar a forma abreviada sempre que o tipo de valor for conhecido.

Se uma enumeração tiver valores em bruto (`rawValue`),
esse são determinados como parte da declaração,
o que significa cada instância de um caso de enumeração particular
tem sempre o mesmo valor.
Outra escolha para casos de enumeração
é ter valores associados ao caso ---
estessão determinados quando se faz a instância,
e podem ser diferentes para cada caso de enumeração.
Pode-se pensar nos valores associados como comportando-se como propriedades armazenadas da instância de enumeração.
Por exemplo, considerar o caso de pedir a hora do nascer e do pôr-do-sol de um servidor.
O servidor ou responde com as informações solicitadas, ou responde com uma descrição do que correu mal.



```swift
enum RepostaServidor {
    case resultado(String, String)
    case falha(String)
}

let sucesso = RepostaServidor.resultado("6:00", "20:09")
let falha =  RepostaServidor.falha("Deu bug")

switch sucesso {
    case let .result(nascerDoSol, porDoSol):
        print("Nascer do Sol será às \(sunrise) e Pôr do Sol será às \(porDoSol).")
    case let .falha(mensagem):
        print("Falha...  \(mensagem)")
}
// Printa "Nascer do Sol será às 6:00 e Pôr do Sol será às 20:09."
```




> Experimento: Adicione um terceiro caso à `ServerResponse`, bem como para o Switch


Repare como o nascer do sol e o pôr-do-sol
são extraídos do valor `ServerResponse`.
como parte da correspondência do valor com os casos do switch.

Utilize `struct` para criar uma estrutura.
As estruturas suportam muitos dos mesmos comportamentos que as classes,
incluindo métodos e inicializadores.
Uma das diferenças mais importantes
entre elas é que
as estruturas são sempre copiadas quando são passadas de um lado para o outro no seu código,
mas as classes são passadas por referência.


```swift
struct Carta {
    var posicao: Posicao
    var naipe: Naipe
    func descricao() -> String {
        return "O \(posicao.descricao) de \(naipe.descricao)"
    }
}

let tresDeEspadas = Carta(posicao: .tres, naipe: .espadas)
let tresDeEspadasDescricao = tresDeEspadas.descricao()
```




> Experimento: Escrever uma função que devolve um array 
>contendo um baralho cheio de cartas 
>com uma delas de cada combinação de Posicao e Naipe

## Concorrência

Use `async` para marcar uma função que é executada de forma assíncrona.

```swift
func fetchUserID(from server: String) async -> Int {
    if server == "primary" {
        return 97
    }
    return 501
}
```

Você marca uma chamada para uma função assíncrona escrevendo `await` na frente dela.

```swift
func fetchUsername(from server: String) async -> String {
    let userID = await fetchUserID(from: server)
    if userID == 501 {
        return "John Appleseed"
    }
    return "Guest"
}
```

Use `async let` para chamar uma função assíncrona,
deixando-a rodar em paralelo com outro código assíncrono.
Quando você usar o valor que ela retorna, escreva 'await'.

```swift
func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let username = fetchUsername(from: server)
    let greeting = await "Hello \(username), user ID \(userID)"
    print(greeting)
}
```

Use `Task` para chamar funções assíncronas de código síncrono,
sem esperar que eles retornem.

```swift
Task {
    await connectUser(to: "primary")
}
// Printar "Hello Guest, user ID 97"
```

## Protocolos e Extensões

Use `protocol` para declarar um protocolo.

```swift
protocol ExampleProtocol {
     var simpleDescription: String { get }
     mutating func adjust()
}
```

Classes, enumerações e estruturas podem adotar protocolos.

```swift
class SimpleClass: ExampleProtocol {
     var simpleDescription: String = "A very simple class."
     var anotherProperty: Int = 69105
     func adjust() {
          simpleDescription += "  Now 100% adjusted."
     }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
     var simpleDescription: String = "A simple structure"
     mutating func adjust() {
          simpleDescription += " (adjusted)"
     }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

> Experimento: Adicione outro requisito ao `ExampleProtocol`.
> Que mudanças você precisa fazer
> para `SimpleClass` e `SimpleStructure`
> para que ainda estejam em conformidade com o protocolo?

Observe o uso da palavra-chave `mutating`
na declaração `SimpleStructure`
para marcar um método que modifica a estrutura.
A declaração `SimpleClass` não precisa
qualquer um de seus métodos marcados como `mutating`
porque os métodos em uma classe sempre podem modificar a classe.

Use `extension` para adicionar funcionalidade a um tipo existente,
como novos métodos e propriedades computadas.
Você pode usar uma extensão para adicionar conformidade de protocolo
para um tipo declarado em outro lugar,
ou até mesmo para um tipo que você importou de uma biblioteca ou _framework_.

```swift
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
 }
print(7.simpleDescription)
// Prints "The number 7"
```

> Experiência: Escreva uma extensão para o tipo `Double`
> que adiciona uma propriedade `absoluteValue`.

Você pode usar um nome de protocolo como qualquer outro tipo nomeado ---
por exemplo, para criar uma coleção de objetos
que tem vários tipos diferentes,
mas que todos estão em conformidade com um único protocolo.
Quando você trabalha com valores cujo tipo é um tipo de protocolo,
métodos que não estão na definição do protocolo não estarão disponíveis.

```swift
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// Prints "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Uncomment to see the error
```

Mesmo que a variável `protocolValue`
tem um tipo de tempo de execução de `SimpleClass`,
o compilador o trata como o tipo dado de `ExampleProtocol`.
Isso significa que você não pode acessar acidentalmente
métodos ou propriedades que a classe implementa
além de sua conformidade com o protocolo.

## Tratamento de erros

Você representa erros usando qualquer tipo que adote o protocolo `Error`.

```swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```

Use `throw` para lançar um erro
e `throws` para marcar uma função que pode lançar um erro.
Se você lançar um erro em uma função,
a função retorna imediatamente e o código que chamou a função
trata o erro.

```swift
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```

Existem várias maneiras de lidar com erros.
Uma maneira é usar `do`-`catch`.
Dentro do bloco `do`,
você marca o código que pode lançar um erro escrevendo `try` na frente dele.
Dentro do bloco `catch`,
o erro recebe automaticamente o nome `error`
a menos que você dê um nome diferente.

```swift
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
// Prints "Job sent"
```

> Experiência: Altere o nome da impressora (printerName) para "Never Has Toner",
> para que a função `send(job:toPrinter:)` lance um erro.

Você pode fornecer vários blocos `catch`
que lidam com erros específicos.
Você escreve um padrão depois de `catch` assim como você faz
após `case` em um _switch_.

```swift
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
// Prints "Job sent"
```

> Experimento: Adicione código para lançar um erro dentro do bloco `do`.
> Que tipo de erro você precisa lançar para que o erro seja tratado pelo primeiro bloco `catch`?
> E quanto ao segundo e terceiro blocos?

Outra maneira de lidar com erros
é usar `try?` para converter o resultado em um opcional.
Se a função lançar um erro,
o erro específico é descartado e o resultado é `nil`.
Caso contrário, o resultado é um opcional contendo
o valor que a função retornou.

```swift
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```

Use `defer` para escrever um bloco de código
que é executado depois de todos os outros códigos na função,
pouco antes da função retornar.
O código é executado independentemente da função gerar um erro.
Você pode usar `defer` para escrever o código de configuração e limpeza um ao lado do outro,
mesmo que eles precisem ser executados em momentos diferentes.

```swift
var fridgeIsOpen = false
let fridgeContent = ["milk", "eggs", "leftovers"]

func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }

    let result = fridgeContent.contains(food)
    return result
}
fridgeContains("banana")
print(fridgeIsOpen)
// Prints "false"
```

## Genéricos

Escreva o nome dentro de "<" e ">"
para fazer uma função ou tipo genérico.



```swift
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result: [Item] = []
    for _ in 0..<numberOfTimes {
         result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```




Você pode fazer formas genéricas de métodos e funções,
assim como classes, enumerações e estruturas.

```swift
// Reimplement the Swift standard library's optional type
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```




Use _where_ logo antes do corpo da função
para especificar uma lista de requisitos ---
por exemplo,
para requisitar o tipo que implementa um protocolo,
para requisitar que dois tipos sejam os mesmos
ou para requerir que uma classe tenha uma superclasse específica.


```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
   return false
}
anyCommonElements([1, 2, 3], [3])
```




> Experimento: Modifique a função `anyCommonElements(_:_:)`
> para fazer uma função que retorna um _array_
> dos elementos que tenham duas sequências em comum.


Escrever `<T: Equatable>`
é a mesma coisa que escrever `<T> ... where T: Equatable`.


