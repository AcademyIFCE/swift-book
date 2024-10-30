# Operadores Básicos

Execute operações como atribuição, aritmética e comparação.

Um operador é um símbolo ou frase especial que você pode usar para verificar, mudar ou combinar valores.
Por exemplo, o operador de adição (`+`) soma dois números,
como em `let i = 1 + 2`,
e o operador lógico AND (`&&`) combina dois valores booleanos,
como em `if enteredDoorCode && passedRetinaScan`.

Swift suporta os operadores que você já conhece de linguagens como C,
e melhora vários pontos para eliminar erros comuns de codificação.
O operador de atribuição (`=`) não retorna um valor,
para evitar que seja usado erroneamente quando
o operador igual a (`==`) é pretendido.
Operadores aritméticos (`+`, `-`, `*`, `/`, `%` e assim por diante)
detectam e desabilitam _overflows_,
para evitar resultados inesperados quando estamos trabalhando com números que se tornam muito maiores ou muito menores
do que o intervalo permitido nos tipos que os armazenam.
Você pode ativar o comportamento de _overflow_
usando os operadores de _overflow_ do Swift,
conforme descrito em <doc:AdvancedOperators#Overflow-Operators>.

Swift também suporta operadores de intervalo que não são encontrados em C,
como `a..<b` e `a...b`,
como um atalho para expressar um intervalo de valores.

Este capítulo descreve os operadores comuns em Swift.
<doc:AdvancedOperators> abrange os operadores avançados de Swift,
e descreve como definir seus próprios operadores personalizados
e implementar os operadores padrão para seus próprios tipos personalizados.

## Terminologia

Operadores são unários, binários ou ternários:

- Os operadores **unários** operam em um único alvo (como `-a`).
  Os operadores **prefixos** unários aparecem imediatamente antes de seu alvo (como `!b`),
  e os operadores **postfixos** unários aparecem imediatamente após seu alvo (como `c!`).
- Os operadores **binários** operam em dois alvos (como `2 + 3`)
  e são **infixos** porque aparecem entre seus dois alvos.
- Os operadores **ternários** operam em três alvos.
  Como C, Swift tem apenas um operador ternário,
  o operador condicional ternário (`a ? b : c`).

Os valores que os operadores afetam são **operandos**.
Na expressão `1 + 2`, o símbolo `+` é um operador infixo
e seus dois operandos são os valores `1` e `2`.

## Operador de Atribuição

O **operador de atribuição** (`a = b`)
inicializa ou atualiza o valor de `a` com o valor de `b`:

```swift
let b = 10
var a = 5
a = b
// a agora é igual a 10
```

Se o lado direito da atribuição é uma tupla com multiplos valores,
os elementos podem ser decompostos em multiplas constantes ou variáveis de uma só vez:

```swift
let (x, y) = (1, 2)
// x é igual a 1, e y é igual a 2
```

Ao contrário do operador de atribuição em C e objective-C, 
em Swift o operador de atribuição não retorna um valor.
A declaração a seguir não é válida:

```swift
if x = y {
   // Isso não é válido, pois x = y não retorna um valor.
}
```

Esta característica previne que o operador de atribuição (`=`) seja usado acidentalmente
quando o operador de igualdade (`==`) é realmente a intenção.
Ao tornar `if x = y` inválido, Swift ajuda você a evitar esse tipo de erro no seu código.


## Operadores Aritméticos

Swift suporta os 4 **operadores aritméticos** padrões para todos os tipos de números: 

- Adição (`+`)
- Subtração (`-`)
- Multiplicação (`*`)
- Divisão (`/`)

```swift
1 + 2       // igual a 3
5 - 3       // igual a 2
2 * 3       // igual a 6
10.0 / 2.5  // igual a 4.0
```

Diferente dos operadores aritméticos em C e Objective-C,
os de Swift não permitem valores ultrapassem o tamanho padrão definido (não permite _overflow_).
Você pode optar pelo comportamento de _overflow_ de valor usando os operadores de _overflow_ do Swift
(como por exemplo `a &+ b`). Veja <doc:AdvancedOperators#Overflow-Operators>.

O operador de adição também é suportado para concatenação de `String`:

```swift
"hello, " + "world"  // igual a "hello, world"
```


### Operador de Resto de Divisão

O **operador de resto de divisão** (`a % b`)
calcula quantos múltiplos de `b` caberão dentro de `a`
e retorna a sobra
(conhecido como *resto*).

> Note: O operador de resto de divisão (`%`) também é conhecido como 
> **operador módulo** em outras linguagens.
> No entanto, seu comportamento em Swift para números negativos torna-o,
> estritamente falando, em um resto em vez de uma operação de módulo.


Veja como o operador de resto funciona.
Para calcular `9 % 4`, você primeiro calcula quantos `4`s caberão dentro de `9`:

![](remainderInteger)


Você pode colocar dois `4`s dentro de `9`, e o restante é `1` (mostrado em laranja).

Em Swift, isso seria escrito como:

```swift
9 % 4    // igual a 1
```

Para determinar a resposta para `a % b`,
o operador `%` calcula a seguinte equação
e retorna `resto` como a saída:

`a` = (`b` x `mutiplicador`) + `resto`

aonde `mutiplicador` é o maior número de múltiplos de `b`
que caberá dentro de `a`.

Colocar `9` e `4` nesta equação produz:

`9` = (`4` x `2`) + `1`

O mesmo método é aplicado ao calcular o restante para um valor negativo de `a`:

```swift
-9 % 4   // igual -1
```

Colocar `-9` e `4` na equação produz:

`-9` = (`4` x `-2`) + `-1`

dando um valor de resto de `-1`.

O sinal de `b` é ignorado para valores negativos de `b`.
Isso significa que `a % b` e `a % -b` sempre dão a mesma resposta.

### Operador Unário de Menos

O sinal de um valor numérico pode ser alternado usando um prefixo `-`,
conhecido como o *operador unário de menos* (`-`):

```swift
let three = 3
let minusThree = -three       // `minusThree` igual a -3
let plusThree = -minusThree   // `plusThree` igual a 3, ou "menos menos 3"
```

O operador unário de menos (`-`) é prefixado diretamente antes do valor em que opera,
sem nenhum espaço em branco.

### Operador Unário de Mais

O *operador unário de mais* (`+`) simplesmente retorna
o valor em que opera, sem qualquer alteração:

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // `alsoMinusSix` igual a -6
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
// `a` agora é igual a 3
```

A expressão `a += 2` é um abreviação para `a = a + 2`.
Efetivamente, a adição e a atribuição são combinadas em um operador
que executa as duas tarefas ao mesmo tempo.

> Nota: Os operadores de atribuição compostos não retornam um valor.
> Por exemplo, você não pode escrever `let b = a += 2`.

Para obter informações sobre os operadores fornecidos pela biblioteca padrão,
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
> Para obter mais informações, consulte <doc:ClassesAndStructures#Operadores-de-Identidade>.

Cada um dos operadores de comparação retorna um valor `Bool` para indicar se a declaração é verdadeira ou não:

```swift
1 == 1   // `true` porque 1 é igual a 1
2 != 1   // `true` porque 2 não é igual a 1
2 > 1    // `true` porque 2 é maior que 1
1 < 2    // `true` porque 1 é menor que 2
1 >= 1   // `true` porque 1 é maior ou igual a 1
2 <= 1   // `false` porque 2 não é menor ou igual a 1
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

Para saber mais sobre a instrução `if`, veja <doc:ControlFlow>.

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
(1, "zebra") < (2, "apple")   // `true` porque 1 é menor que 2; "zebra" e "apple" não são comparados
(3, "apple") < (3, "bird")    // `true` porque 3 é igual a 3 e "apple" é menor que "bird"
(4, "dog") == (4, "dog")      // `true` porque 4 é igual a 4 e "dog" é igual a "dog"
```

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
("blue", -1) < ("purple", 1)        // OK, avalia como `true`
("blue", false) < ("purple", true)  // Erro, pois < não pode ser usado para valores booleanos
```

> Nota: A biblioteca padrão Swift inclui operadores de comparação de tuplas
> para tuplas com menos de sete elementos.
> Para comparar tuplas com sete ou mais elementos,
> você mesmo deve implementar os operadores de comparação.

## Operador Condicional Ternário

O **operador condicional ternário** é um operador especial com três partes, 
no formato `question ? answer1 : answer2`. 
É uma abreviação para escolher uma de duas expressões
baseado se `question` é verdadeiro ou falso. 
Se `question` for verdadeiro, ele escolhe `answer1` e retorna seu valor; 
caso contrário, ele escolhe `answer2` e retorna seu valor.

O operador condicional ternário é uma abreviação para o código abaixo:

```swift
if question {
   answer1
} else {
   answer2
}
```

Aqui está um exemplo, que calcula a altura da linha (`rowHeight`) de uma tabela. A altura da linha deve ser 50 pontos mais alta que a altura do conteúdo (`contentHeight`) se a linha tiver um cabeçalho (`hasHeader`). Caso contrário, a altura da linha deve ser 20 pontos mais alta:

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
o que é mais conciso que o código usado no segundo exemplo.

O operador condicional ternário fornece 
uma abreviação eficiente para decidir qual de duas expressões escolher. 
No entanto, use o operador condicional ternário com cuidado. 
Sua concisão pode levar a um código difícil de ler se usado em excesso. 
Evite combinar vários usos do operador condicional ternário em uma instrução composta.

## Operador _Nil-Coalescing_ 

O **operador _nil-coalescing_** (`a ?? b`)
desempacota um `a` opcional se ele contiver um valor,
ou retorna um valor padrão `b` se `a` for `nil`.
A expressão `a` é sempre de um tipo opcional.
A expressão `b` deve corresponder ao tipo que está armazenado dentro de `a`.

O operador _nil-coalescing_ é uma abreviação para o código abaixo:

```swift
a != nil ? a! : b
```

O código acima usa o operador condicional ternário e o desempacotamento forçado (`a!`)
para acessar o valor encapsulado dentro de `a` quando `a` não é `nil`,
e para retornar `b` caso contrário.
O operador _nil-coalescing_ fornece uma maneira mais elegante de encapsular
essa verificação condicional e desempacotamento em um formato conciso e legível.

> Nota: Se o valor de `a` não for `nil`,
> o valor de `b` não será avaliado.
> Isso é conhecido como **avaliação de curto-circuito**.

O exemplo abaixo usa o operador _nil-coalescing_ para escolher entre
um nome de cor padrão e um nome de cor opcional definido pelo usuário:

```swift
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// `userDefinedColorNam` é nil, então `colorNameToUse` é definido como o valor padrão "red"
```

A variável `userDefinedColorName` é definida como uma `String` opcional,
com um valor padrão de `nil`.
Como `userDefinedColorName` é de um tipo opcional,
você pode usar o operador _nil-coalescing_ para considerar seu valor.
No exemplo acima, o operador é usado para determinar
um valor inicial para uma variável `String` chamada `colorNameToUse`.
Como `userDefinedColorName` é `nil`,
a expressão `userDefinedColorName ?? defaultColorName` retorna
o valor de `defaultColorName`, ou `"red"`.

Se você atribuir um valor não `nil` a `userDefinedColorName`
e executar a verificação do operador _nil-coalescing_ novamente,
o valor encapsulado dentro de `userDefinedColorName` será usado em vez do padrão:

```swift
userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
// `userDefinedColorName` não é nil, entã `colorNameToUse` é definido como "green"
```

## Operadores de Intervalo

Swift possuí diversos **operadores de intervalo**, que são maneiras mais simples de se expressar um intervalo de valores.

### Operador de Intervalo Fechado

O *operador de intervalo fechado* (`a...b`) estabelece um intervalo que vai de `a` até `b`, incluindo os próprios valores de `a` e `b`. O valor de `a` não pode ser maior que o valor de `b`.

O operador de intervalo fechado pode ser útil quando se deve iterar sobre um intervalo
em que você quer que todos os valores sejam utilizados, 
assim como em um laço `for`-`in`:

```swift
for index in 1...5 {
   print("\(index) times 5 is \(index * 5)")
}
// Imprime "1 times 5 is 5"
// Imprime "2 times 5 is 10"
// Imprime "3 times 5 is 15"
// Imprime "4 times 5 is 20"
// Imprime "5 times 5 is 25"
```

Para saber mais sobre laços `for`-`in`, veja <doc:ControlFlow>.

### Operador de Intervalo Semiaberto

O **operador de intervalo semiaberto**
define o intervalo que vai de ‘a’ até ‘b’,
mas não inclui ‘b’.
É dito como **semiabeto**
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
// Imprime "Person 1 is called Anna"
// Imprime "Person 2 is called Alex"
// Imprime "Person 3 is called Brian"
// Imprime "Person 4 is called Jack"
```

Note que o _array_ contém quatro itens,
mas `0..<count` somente conta até `3`
(o índice do último item no _array_),
pois é um intervalo semiaberto.
Para saber mais sobre _arrays_, veja: <doc:CollectionTypes#Arrays>.


### Intervalos Unilaterais

O operador de intervalo fechado
tem uma forma alternativa para intervalos que continuam
o mais longe possível em uma direção ---
por exemplo,
um intervalo que inclui todos os elementos de um _array_
do índice 2 até o fim do _array_.
Nesses casos, você pode omitir o valor
de um lado do operador de intervalo.
Esse tipo de intervalo é chamado de *intervalo unilateral*
porque o operador possui valor em apenas um lado.
Por exemplo:

```swift
for name in names[2...] {
    print(name)
}
// Imprime "Brian"
// Imprime "Jack"

for name in names[...2] {
    print(name)
}
// Imprime "Anna"
// Imprime "Alex"
// Imprime "Brian"
```

O intervalo semiaberto também tem
uma forma unilateral que é escrita
com apenas seu valor final.
Da mesma forma que se inclui um valor em ambos os lados,
o valor final não é parte do intervalo.
Por exemplo:

```swift
for name in names[..<2] {
    print(name)
}
// Imprime "Anna"
// Imprime "Alex"
```

Intervalos unilaterais podem ser usados em outros contextos,
não apenas em subscritos.
Você não pode iterar sobre um intervalo unilateral
que omite o primeiro valor,
pois não é claro onde a iteração deve iniciar.
Voce **pode** iterar sobre um intervalo unilateral que omite seu valor final;
entretanto, por conta do intervalo continuar indefinidamente, 
certifique-se de adicionar uma condição explícita para finalizar o _loop_.
Voce pode também checar se um intervalo unilateral contém um valor particular,
como mostrado no código abaixo.


```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```

## Operadores Lógicos

*Operadores lógicos'* modificam ou combinam
os valores lógicos booleanos `true` e `false`.
Swift suporta os três operadores lógicos padrão encontrados em linguagens baseadas em C:

- Lógica NOT (`!a`)
- Lógica AND (`a && b`)
- Lógica OR (`a || b`)

### Operador Lógico NOT
O *operador lógico NOT* (`!a`) inverte o valor booleano para que `true` vire `false` e `false` vire `true`. 

O operador lógico NOT é um operador de prefixo,
e aparece imediatamente antes do valor em que opera,
sem nenhum espaço em branco.

Ele pode ser lido como "não `a`", como no exemplo a seguir:

```swift
let allowedEntry = false
if !allowedEntry {
   print("ACCESS DENIED")
}
// Imprime "ACCESS DENIED"
```

A frase `if !allowedEntry` pode ser lida como "se entrada não permitida."
A linha só é executada se "entrada não permitida" for verdadeira;
isto é, `if allowedEntry` é `false`.

Como neste exemplo,
a escolha cuidadosa de nomes de constantes e variáveis booleanas
pode ajudar a manter o código legível e conciso,
evitando duplas negativas ou declarações lógicas confusas.

### Operador Lógico AND

O *operador lógico AND* (`a && b`) cria expressões lógicas
onde ambos os valores devem ser `true` para que a expressão geral também seja `true`.

Se um dos valores for `falso`,
a expressao geral será tida como `false`.
Na verdade, se o **primeiro** valor for `false`,
o segundo valor nem será avaliado,
porque não é possível que a expressão geral seja igual a `true`.
Isso é conhecido como **avaliação de curto-circuito**.

Este exemplo considera dois valores `Bool`
e só permite acesso se ambos os valores forem `true`:

```swift
let enteredDoorCode = true
let passedRetinaScan  = false
if enteredDoorCode && passedRetinaScan  {
   print("Welcome!")
} else {
   print("ACESS DENIED")
}
// Imprime "ACESS DENIED"
```

### Operador Lógico OR

O **operador lógico OR**
(`a || b`) é um operador infixo feito de dois caracteres _pipe_ adjacentes.
Você o usa para criar expressões lógicas nas quais
basta que **um** dos dois valores seja `true`
para que a expressão geral seja `true`.

Como o operador lógico AND acima,
o operador lógico OR usa avaliação de curto-circuito para considerar suas expressões.
Se o lado esquerdo de uma expressão lógica OR for `true`,
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
// Imprime "Welcome!"
```

### Combinando Operadores Lógicos

Você pode combinar vários operadores lógicos para criar expressões compostas mais longas:

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Imprime "Welcome!"
```

Este exemplo usa vários operadores `&&` e `||` para criar uma expressão composta mais longa.
No entanto, os operadores `&&` e `||` ainda operam sobre apenas dois valores,
então, na verdade, são três expressões menores encadeadas.
O exemplo pode ser lido como:

"Se inserimos o código da porta correto e passarmos no _scanner_ de retina,
ou se tivermos uma chave de porta válida,
ou se soubermos a senha de substituição de emergência,
então permita o acesso."

Com base nos valores de `enteredDoorCode`, `passedRetinaScan` e `hasDoorKey`,
as duas primeiras subexpressões são `false`.
No entanto, a senha de substituição de emergência é conhecida,
então a expressão composta geral ainda é avaliada como `true`.

> Note: Os operadores lógicos `&&` e `||` são associativos à esquerda,
> significando que expressões compostas com vários operadores lógicos
> avaliam primeiro a subexpressão mais à esquerda.

### Parênteses Explícitos

Às vezes é útil incluir parênteses quando eles não são estritamente necessários,
para tornar a intenção de uma expressão complexa mais fácil de ler.
No exemplo de acesso à porta acima,
é útil adicionar parênteses em torno da primeira parte da expressão compostas
para deixar claro sua intenção:

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Imprime "Welcome!"
```

Os parênteses deixam claro que os dois primeiros valores
são considerados como parte de um estado possível separado na lógica geral.
A saída da expressão composta não muda,
mas a intenção geral é mais clara para o leitor.
Legibilidade é sempre preferível à brevidade;
use parênteses onde eles ajudam a tornar suas intenções claras.
