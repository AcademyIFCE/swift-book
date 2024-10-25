# Um Guia de Swift

Explore os recursos e a sintaxe da linguagem.

A tradição sugere que o primeiro programa em uma nova linguagem deve imprimir a frase "Hello, world!" na tela.
Em Swift, isso pode ser feito em uma simples linha:

```swift
print("Hello, world!")
// Imprime "Hello, world!"
```

Essa sintaxe deve parecer familiar se você conhece outra linguagem de programação ---
em Swift, essa linha de código é um programa completo.
Você não precisa importar uma biblioteca separada para funcionalidades como
imprimir texto ou manipulação de *strings*.
O código escrito no escopo global é usado
como ponto de entrada para o programa,
então você não precisa de uma função `main()`.
Você também não precisa escrever ponto e vírgula
no final de cada declaração.

Este guia lhe dá informações suficientes
para começar a escrever códigos em Swift, mostrando como realizar uma variedade de tarefas de programação.
Não se preocupe se você não entender alguma coisa ---
tudo o que for introduzido neste guia será explicado em detalhes no resto do livro.

## Valores Simples

Use `let` para criar uma constante e `var` para criar uma variável.
O valor de uma constante não precisa ser sabido no momento do código ser compilado. mas você deve atribuí-la um valor somente uma vez. Isso significa que você pode usar constantes para nomear um valor que você determinou uma vez, mas utiliza em muitos lugares.

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```


Uma constante ou variável deve ser do mesmo tipo do valor que você quer atribuir a ela. Entretanto, você nem sempre precisa atribuir o tipo de forma explícita. 
Dar um valor quando você cria uma constante ou variável faz com que o compilador infira qual o seu tipo. No exemplo acima, o compilador irá inferir que a `myVariable` é um inteiro, pois o seu valor inicial é um inteiro. Se o valor inicial não fornecer informação suficiente (ou se não foi atribuído nenhum valor inicial), especifique o tipo escrevendo-o logo depois da variável, separado por dois pontos. 

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```




> Experimente: Crie uma constante com o tipo `Float` explícito e de valor `4`.

Valores nunca são implicitamente convertidos para outro tipo. Se você precisar converter um valor para um tipo diferente, crie explicitamente uma instância do tipo desejado." 

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```




> Experimente: Tente remover a conversão para `String` da última linha
> Que tipo de erro dá?



Existe uma forma ainda mais simples de incluir valores em uma *string*: escreva o valor em parênteses com uma barra invertida (`\`) antes do primeiro parêntese. Por exemplo:

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```




> Experimente: Use `\()` para incluir um cálculo de ponto flutuante em uma *string* e para incluir o nome de alguém em uma saudação.

Use três aspas duplas para *strings* com múltiplas linhas. A indentação no começo de cada linha de texto será removida, caso seja a mesma das aspas de fechamento. 
Por exemplo:

```swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```






Crie *arrays* e dicionários usando colchetes (`[]`), e acesse seus elementos escrevendo o índice ou chave também entre colchetes. A vírgula após o último elemento é permitida. 





```swift
var fruits = ["strawberries", "limes", "tangerines"]
fruits[1] = "grapes"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
 ]
occupations["Jayne"] = "Public Relations"
```




*Arrays* crescem automaticamente quando você adiciona elementos. 

```swift
fruits.append("blueberries")
print(fruits)
```




Para criar um *array* ou dicionário vazio, use a sintaxe de inicialização.

```swift
let emptyArray: [String] = []
let emptyDictionary: [String: Float] = [:]
```




Se o tipo da informação pode ser inferido, você pode escrever um *array* vazio com `[]` e um dicionário vazio com `[:]`. Por exemplo, quando você configura um novo valor para uma variável ou passa um argumento para uma função.




```swift
fruits = []
occupations = [:]
```




## Controle de Fluxo


Use `if` e `switch` para fazer condicionais,
e use `for`-`in`, `while`, e `repeat`-`while`
para criar *loops*.
É opcional inserir condicionais ou variáveis de *loop* entre parênteses. 
É obrigatório inserir o corpo do *loop* entre chaves.

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
// Imprime "11"
```








Em uma declaração `if`,
a condição deve ser uma expressão booleana ---
isso significa que um código como `if score { ... }` é um erro,
não uma comparação implicita à zero.

Você pode usar `if` e `let` juntos
para trabalhar com valores que podem estar ausentes.
Esses valores são representados como opcionais.
Um valor opcional contém um valor
ou contém `nil` para indicar um valor ausente.
Insira um ponto de interrogação, em seguida, digite um valor
para marcá-lo como opcional.





```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Imprime "false"

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
a condicional é `false` e o código nas chaves são pulados
Caso contrário, o valor opcional é desempacotado e atribuído,
para a constante depois de `let`
o que faz o valor desempacotado ficar disponível
dentro do bloco de código.

Outra maneira de lidar com valores opcionais
é provendo um valor padrão usando o operador `??`.
Se o valor opcional está ausente,
o valor padrão é usado como substituto. 

```swift
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
```



Você pode usar uma forma abreviada para desempacotar um valor, 
utilizando o mesmo nome para o valor desempacotado.

```swift
if let nickname {
    print("Hey, \(nickname)")
}
```




O comando `switch` suporta todos os tipos de dados
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
// Imprime "Is it a spicy red pepper?"
```




> Experimente: tente remover o caso _default_
> Qual o erro indicado?

Perceba como `let` pode ser usado em um padrão
para determinar o valor que combina o padrão
com a constante.

Após executar o código dentro do caso correspondente, 
o programa sai da controle `switch`.
A execução não continua para o próximo caso, 
então não é necessário sair explicitamente do `switch` 
no final do código de cada caso.


Você usa `for`-`in`para iterar os itens em um dicionário
provendo um par de nomes para usar
para cada par de chave-valor.
Dicionários são uma coleção não-ordenada
então, suas chaves e valores são iterados
em uma ordem arbitrária.



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
// Imprime "25"
```




> Experimente: Substitua `_` com o nome de uma variável,
> e acompanhe qual tipo de número foi maior.

Use `while` para repetir um bloco de código até a condição mudar.
As condições de um *loop* podem estar no final
assegurando que o *loop* será executado pelo menos uma vez.



```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Imprime "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Imprime "128"
```

> Experimente:
> Mude a condição de `m < 100` para `m < 0`
> para ver como `while` e `repeat`-`while` se comportam diferente
> quando a condição do *loop* já é false.


Você pode obter um índice em *loop*
usando `..<` para criar uma série de índices.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Imprime "6"
```




Use `..<` para criar um intervalo que omite seu maior valor,
e use `...` para usar um intervalo que inclui ambos os valores.

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




> Experimente: Remova o parâmetro `day`.
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




As funções são, na verdade, um caso especial de *closures*:
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

Use `class` seguido de um nome para criar uma classe. Uma propriedade declarada dentro de uma classe é escrita da mesma que a declaração de uma variável ou constante, mas se encaixando no contexto daquela classe. Da mesma forma, declarações de métodos e funções também são escritos da mesma maneira.



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

Crie uma instância de uma classe colocando parênteses depois do nome dela. Use a sintaxe de ponto para acessar as propriedades e métodos daquela instância.

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




Note como `self` é usado para diferenciar a propriedade `name` do argumento `name` para o inicializador. Os argumentos, para o inicializador, são chamados como uma chamada de função quando você cria uma instancia de uma classe. Toda propriedade precisa ter um valor atribuído — seja na sua declaração (como em `numberOfSides`) ou no inicializador (como em `name`).

Use `deinit` para criar um desinicializador se você precisar realizar uma limpeza antes que o objeto seja desalocado.

Subclasses incluem o nome de sua superclasse após seu nome, separado por dois pontos. Uma classe não tem a necessidade de herdar nenhuma classe raiz, portanto você pode incluir ou omitir uma superclasse conforme for necessário.

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




> Experimente: Crie outra subclasse de `NamedShape` chamada `Circle`, que pega o raio e o nome como argumentos no inicializador. Implemente `area()`e `simpeDescription()`na classe `Circle`. 

Em adição às propriedades simples que são armazenadas, cada propriedade pode ter um *getter* e um *setter*.


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
// Imprime "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Imprime "3.3000000000000003"
```





No *setter* de `perimeter`, o novo valor tem o nome implícito `newValue`. Você pode dar a ele um nome explícito nos parênteses após `set`. Note que o inicializador para classe `EquilateralTriangle` possui três diferente passos:

1. Definir o valor das propriedades declaradas pela subclasse
2. Chamar o inicializador da superclasse
3. Mudar o valor das propriedades definidas pela superclasse. Qualquer trabalho de configuração que use métodos, *getters* ou *setters*.

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
// Imprime "10.0"
print(triangleAndSquare.triangle.sideLength)
// Imprime "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// Imprime "50.0"
```






Quando trabalhar com valores opcionais,  você pode usar `?` antes de operações como métodos, propriedades e subscrição . Se o valor antes de `?` for `nil`, tudo depois do sinal `?` é ignorado e o valor de toda expressão se torna `nil`. Caso contrário, o valor opcional é desempacotado, e tudo depois do sinal `?` age de acordo com o valor desempacotado. Em ambos os casos, o valor da expressão por inteiras é um valor opcional.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```




## Enumerações e Estruturas

Use `enum` para criar uma enumeração. Como as classes e todos os outros tipos nomeados, as enumerações podem ter métodos associados a elas.

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
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
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

> Experimente: Escreva uma função que compara dois valores `Rank` comparando seus valores brutos (*rawValue*).

Por padrão, Swift atribui os valores brutos começando em zero e incrementando em um a cada vez, mas você pode alterar esse comportamento especificando explicitamente os valores. No exemplo acima, `Ace` recebe explicitamente um valor bruto de `1`, e o resto dos valores brutos são atribuídos em ordem. Você também pode usar *strings* ou números de ponto flutuante como o tipo bruto de uma enumeração. Use a propriedade `rawValue` para acessar o valor bruto de um caso de enumeração.

Use o inicializador `init?(rawValue:)` para criar uma instância de uma enumeração a partir de um valor bruto. Ele retorna o caso de enumeração correspondente ao valor bruto ou `nil` se não houver `Rank` correspondente.

```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

Os valores `case` de uma enumeração são valores reais, não apenas outra maneira de escrever seus valores brutos. Na verdade, nos casos em que não há um valor bruto significativo, você não precisa fornecer um.

```swift
enum Suit {
    case spades, hearts, diamonds, clubs

    func simpleDescription() -> String {
        switch self {
            case .spades:
                return "spades"
            case .hearts:
                return "hearts"
            case .diamonds:
                return "diamonds"
            case .clubs:
                return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```

> Experimente: Adicione um método `color()` a `Suit` que retorna "black" para espadas e paus, e retorna "red" para copas e ouros.

Observe as duas maneiras como o caso `hearts` da enumeração é referido acima: Ao atribuir um valor à constante `hearts`, o caso de enumeração `Suit.hearts` é referenciado por seu nome completo porque a constante não tem um tipo explícito especificado. Dentro do `switch`, o caso de enumeração é referido pela forma abreviada `.hearts` porque o valor de `self` já é conhecido como `Suit`. Você pode usar a forma abreviada sempre que o tipo do valor já for conhecido.

Se uma enumeração tiver valores brutos, esses valores serão determinados como parte da declaração, o que significa que cada instância de um determinado caso de enumeração sempre terá o mesmo valor bruto. Outra opção para casos de enumeração é ter valores associados ao caso --- esses valores são determinados quando você cria a instância e podem ser diferentes para cada instância de um caso de enumeração. Você pode pensar nos valores associados como se comportando como propriedades armazenadas da instância de caso de enumeração. Por exemplo, considere o caso de solicitar os horários do nascer e do pôr do sol de um servidor. O servidor responde com as informações solicitadas ou com uma descrição do que deu errado.

```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
    case let .result(sunrise, sunset):
        print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
    case let .failure(message):
        print("Failure...  \(message)")
}
// Imprime "Sunrise is at 6:00 am and sunset is at 8:09 pm."
```

> Experimento: Adicione um terceiro caso a `ServerResponse` e ao `switch`.

Observe como os horários do nascer e do pôr do sol são extraídos do valor `ServerResponse` como parte da comparação do valor com os casos de alternância.

Use `struct` para criar uma estrutura. As estruturas suportam muitos dos mesmos comportamentos das classes, incluindo métodos e inicializadores. Uma das diferenças mais importantes entre estruturas e classes é que as estruturas sempre são copiadas quando são passadas em seu código, mas as classes são passadas por referência.

```swift
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

> Experimente: Escreva uma função que retorne um *array* contendo um baralho completo de cartas, com uma carta de cada combinação de valor e naipe.

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
Quando você usar o valor que ela retorna, escreva `await`.

```swift
func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let username = fetchUsername(from: server)
    let greeting = await "Hello \(username), user ID \(userID)"
    print(greeting)
}
```

Use `Task` para chamar funções assíncronas a partir de um código síncrono,
sem esperar que elas retornem.

```swift
Task {
    await connectUser(to: "primary")
}
// Imprime "Hello Guest, user ID 97"
```

Use `TaskGroup` para estruturar código concorrente.

```swift
let userIDs = await withTaskGroup(of: Int.self) { group in
    for server in ["primary", "secondary", "development"] {
        group.addTask {
            return await fetchUserID(from: server)
        }
    }

    var results: [Int] = []
    for await result in group {
        results.append(result)
    }
    return results
}
```

Atores são similares a classes,
exceto que eles garantem que diferentes funções assíncronas
possam interagir com segurança com uma instância do mesmo ator ao mesmo tempo.

```swift
actor ServerConnection {
    var server: String = "primary"
    private var activeUsers: [Int] = []
    func connect() async -> Int {
        let userID = await fetchUserID(from: server)
        // ... communicate with server ...
        activeUsers.append(userID)
        return userID
    }
}
```

Quando você chama um método em um ator ou acessa uma de suas propriedades,
você marca esse código com `await`
para indicar que ele pode ter que esperar outro código
que já está em execução no ator terminar.

```swift
let server = ServerConnection()
let userID = await server.connect()
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

> Experimente: Adicione outro requisito ao `ExampleProtocol`.
> Que mudanças você precisa fazer
> em `SimpleClass` e `SimpleStructure`
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
// Imprime "The number 7"
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
// Imprime "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Uncomment to see the error
```

Mesmo que a variável `protocolValue`
tem um tipo de tempo de execução de `SimpleClass`,
o compilador o trata como o tipo dado de `ExampleProtocol`.
Isso significa que você não pode acessar acidentalmente
métodos ou propriedades que a classe implementa
além de sua conformidade com o protocolo.

## Tratamento de Erros

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
// Imprime "Job sent"
```

> Experimente: Altere o nome da impressora para "Never Has Toner",
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
// Imprime "Job sent"
```

> Experimente: Adicione um código para lançar um erro dentro do bloco `do`.
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
// Imprime "false"
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




> Experimente: Modifique a função `anyCommonElements(_:_:)`
> para fazer uma função que retorna um _array_
> dos elementos que tenham duas sequências em comum.


Escrever `<T: Equatable>`
é a mesma coisa que escrever `<T> ... where T: Equatable`.
