# O Básico

Trabalhe com tipos comuns de dados e escreva sintaxe básica.

Swift fornece muitos tipos de dados fundamentais,
incluindo `Int` para inteiros,
`Double` para valores de ponto flutuante,
`Bool` para valores booleanos,
e `String` para texto.
Swift também fornece versões poderosas dos três tipos de coleção primários,
`Array`, `Set` e `Dictionary`,
conforme descrito em <doc:CollectionTypes>.

Swift usa variáveis ​​para armazenar e se referir a valores por um nome de identificação.
Swift também faz uso extensivo de variáveis ​​cujos valores não podem ser alterados.
Elas são conhecidas como constantes e são usadas para tornar o código mais seguro e claro na intenção
quando você trabalha com valores que não precisam ser alterados.

Além dos tipos familiares,
Swift introduz tipos avançados, como tuplas.
As tuplas permitem que você crie e passe agrupamentos de valores.
Você pode usar uma tupla para retornar vários valores de uma função como um único valor composto.

Swift também introduz tipos opcionais,
que lidam com a ausência de um valor.
Os opcionais dizem "**há** um valor, e ele é igual a **x**"
ou "**não há** nenhum valor".

Swift é uma linguagem **type-safe**,
o que significa que a linguagem ajuda você a ser claro sobre os tipos de valores com os quais seu código pode trabalhar.
Se parte do seu código requer uma `String`,
a segurança de tipos impede que você passe um `Int` por engano.
Da mesma forma, a segurança de tipos impede que você passe
acidentalmente uma `String` opcional
para um pedaço de código que requer uma `String` não opcional.
A segurança de tipos ajuda você a detectar e corrigir erros o mais cedo possível no processo de desenvolvimento.

## Constantes e Variáveis 

Constantes e variáveis associam um nome
(como `maximumNumberOfLoginAttempts` ou `welcomeMessage`)
com um valor de um tipo específico (como o número `10` ou a string `"Hello"`).
O valor de uma **constante** não pode ser alterado depois de definido,
enquanto uma **variável** pode ser definida com um valor diferente no futuro.

### Declarando Constantes e Variáveis 

Constantes e variáveis devem ser declaradas antes de serem usadas.
Você declara constantes com a palavra-chave `let` e variáveis com a palavra-chave `var`.
Aqui está um exemplo de como constantes e variáveis podem 
ser usadas para rastrear o número de tentativas de login feitas por um usuário:

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

Esse código pode ser lido como:

“Declare uma nova constante chamada `maximumNumberOfLoginAttempts`
e dê a ela um valor de `10`. 
Em seguida, declare uma nova variável chamada `currentLoginAttempt` 
e dê a ela um valor inicial de `0`.”

Neste exemplo, o número máximo de tentativas de login permitidas
é declarado como uma constante, porque o valor máximo nunca muda.
O contador de tentativas de login atual é declarado como uma variável,
porque esse valor deve ser incrementado após cada tentativa de login com falha.

Se um valor armazenado no seu código não mudar,
sempre declare-o como uma constante com a palavra-chave `let`.
Use variáveis ​​somente para armazenar valores que mudam.

Quando você declara uma constante ou uma variável,
você pode dar a ela um valor como parte dessa declaração,
como os exemplos acima.
Como alternativa,
você pode atribuir seu valor inicial mais tarde no programa,
desde que seja garantido que ele tenha um valor
antes da primeira leitura.

```swift
var environment = "development"
let maximumNumberOfLoginAttempts: Int
// `maximumNumberOfLoginAttempts` não tem valor ainda.

if environment == "development" {
    maximumNumberOfLoginAttempts = 100
} else {
    maximumNumberOfLoginAttempts = 10
}
// Agora `maximumNumberOfLoginAttempts` tem um valor, e pode ser lida.
```

Neste exemplo,
o número máximo de tentativas de login é constante,
e seu valor depende do ambiente.
No ambiente de desenvolvimento,
ele tem um valor de 100;
em qualquer outro ambiente, seu valor é 10.
Ambos os ramos da instrução `if`
inicializam `maximumNumberOfLoginAttempts` com algum valor,
garantindo que a constante sempre obtenha um valor.
Para obter informações sobre como Swift verifica seu código
quando você define um valor inicial dessa forma,
consulte <doc:Declarations#Constant-Declaration>.

Você pode declarar várias constantes ou várias variáveis em uma única linha, separadas por vírgulas:

```swift
var x = 0.0, y = 0.0, z = 0.0
```

### Anotações de Tipo

Você pode fornecer uma **anotação de tipo** ao declarar uma constante ou variável, 
para ser claro sobre o tipo de valores que a constante ou variável pode armazenar. 
Escreva uma anotação de tipo colocando dois pontos após o nome da constante ou variável, 
seguido de um espaço e do nome do tipo a ser usado.

Este exemplo fornece uma anotação de tipo para uma variável chamada `welcomeMessage`, 
para indicar que a variável pode armazenar valores do tipo `String`:

```swift
var welcomeMessage: String
```

Os dois pontos na declaração significam “…do tipo…”, 
então o código acima pode ser lido como:

“Declare uma variável chamada `welcomeMessage` que é do tipo `String`.”

A frase “do tipo `String`” significa “pode armazenar qualquer valor `String`.” 
Pense nisso como significando “o tipo de coisa” que pode ser armazenado.

A variável `welcomeMessage` agora pode ser definida para qualquer valor de _string_ sem erro:

```swift
welcomeMessage = "Hello"
```

Você pode definir várias variáveis relacionadas do mesmo tipo em uma única linha,
separadas por vírgulas, com uma única anotação de tipo após o nome da variável final:

```swift
var red, green, blue: Double
```

> Nota: É raro que você precise escrever anotações de tipo na prática. 
> Se você fornecer um valor inicial para uma constante ou variável no ponto em que ela é definida,
> a linguagem quase sempre pode inferir o tipo a ser usado para essa constante ou variável,
> conforme descrito em <doc:TheBasics#Type-Safety-and-Type- Inferência>.
> No exemplo `welcomeMessage` acima, nenhum valor inicial é fornecido e,
> portanto, o tipo da variável `welcomeMessage` é especificado com uma anotação de tipo 
> em vez de ser inferido de um valor inicial.

### Nomeando Constantes e Variáveis 

Os nomes de constantes e variáveis podem conter praticamente qualquer caractere,
incluindo caracteres **Unicode**:

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

Os nomes de constantes e variáveis não podem conter 
caracteres de espaço em branco, símbolos matemáticos, setas, valores escalares Unicode de uso privado 
ou caracteres de desenho de linha e caixa.
Eles também não podem começar com um número,
embora os números possam ser incluídos em outra posição dentro do nome.

Depois de declarar uma constante ou variável de um determinado tipo,
você não pode declará-la novamente com o mesmo nome
ou alterá-la para armazenar valores de um tipo diferente. 
Nem você pode transformar uma constante em uma variável 
ou uma variável em uma constante.

> Nota: Se você precisar dar a uma constante ou variável o mesmo nome de uma palavra-chave reservada, 
> coloque a palavra-chave entre crases (```) ao usá-la como um nome. 
> No entanto, evite usar palavras-chave como nomes, a menos que você não tenha escolha.

Você pode alterar o valor de uma variável existente para outro valor de tipo compatível. 
Neste exemplo, o valor de `friendlyWelcome` é alterado de `"Hello!"` para `"Bonjour!"`:

```swift
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// `friendlyWelcome` agora é "Bonjour!"
```

Ao contrário de uma variável, o valor de uma constante não pode ser alterado depois de definido. 
Tentar fazer isso é indicado como um erro quando seu código é compilado:

```swift
let languageName = "Swift"
languageName = "Swift++"
// Este é um erro de tempo de compilação: `languageName` não pode ser alterado.
```

### Imprimindo Constantes e Variáveis

Você pode imprimir o valor atual de uma constante ou variável com a função `print(_:separator:terminator:)`:

```swift
print(friendlyWelcome)
// Imprime "Bonjour!"
```

A função `print(_:separator:terminator:)` é uma função global 
que imprime um ou mais valores para uma saída apropriada. 
No Xcode, por exemplo, a função `print(_:separator:terminator:)` imprime sua saída no painel “console” do Xcode.
Os parâmetros `separator` e `terminator` possuem valores padrão, 
então você pode omiti-los quando chamar esta função.
Por padrão, a função termina a linha que imprime adicionando uma quebra de linha. 
Para imprimir um valor sem uma quebra de linha após ele, passe uma string vazia como terminador --- 
por exemplo, `print(someValue, terminator: "")`. 
Para obter informações sobre parâmetros com valores padrão, 
consulte <doc:Functions#Default-Parameter-Values>.


Swift usa **interpolação de _string_** para incluir o nome de uma constante ou variável 
como um espaço reservado em uma _string_ mais longa e para solicitar 
a substituição pelo valor atual dessa constante ou variável.
Coloque o nome entre parênteses e escape com uma barra invertida antes do parêntese de abertura:

```swift
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Imprime "The current value of friendlyWelcome is Bonjour!"
```

> Nota: Todas as opções que você pode usar com a interpolação de _string_ 
são descritas em <doc:StringsAndCharacters#String-Interpolation>.

## Comentários

Use comentários para adicionar texto não executável em seu código,
como notas ou lembretes para você mesmo.
Comentários são ignorados pelo compilador quando o seu código é compilado.

Os comentários em Swift são bem similares aos em C.
Comentários de uma única linha começam com duas barras inclinadas (`//`): 

```swift
// Isso é um comentário.
```

Comentários multilinha começam com uma barra inclinada seguida por um asterisco (`/*`)
e terminam com um asterisco seguido por uma barra inclinada (`*/`):

```swift
/* Isso também é um comentário
mas foi escrito em várias linhas. */
```

Diferentemente dos comentários multilinha em C,
comentários multilinha em Swift podem ser aninhados dentro de outro cometário multilinha.
Você escreve comentários aninhados começando um bloco de comentário multilinha 
e então começando um segundo comentário multilinha dentro do primeiro bloco. 
O segundo bloco é então fechado, seguindo pelo primeiro bloco:

```swift
/* Esse é o começo do primeiro comentário multilinha.
   /* Esse é o segundo, comentário multilinha aninhado. */
Esse é o final do primeiro comentário multilinha. */
```

Comentários multilinha aninhados permitem que você comente grandes blocos de código rapidamente e facilmente,
mesmo quando o código já contém comentários multilinha.

## Ponto e Vígula

Diferentemente de outras linguagens,
Swift não requer que você escreva um ponto e vírgula (`;`) depois de cada instrução do seu código,
embora você pode fazer se desejar.
No entanto, pontos e vírgulas **são** necessários
caso você queira escrever multiplas instruções em uma única linha:

```swift
let cat = "🐱"; print(cat)
// Imprime "🐱"
```

## Inteiros

*Inteiros* são todos os números sem componente fracionário,
como `42` e `-23`.
Inteiros também podem possuir sinal (positivo, zero, ou negativo)
ou não possuir sinal (positivo ou zero).

Swift dispõe de inteiros com sinal e sem sinal nas formas de 8, 16, 32 e 64 _bits_.
Esses inteiros seguem uma convenção de nomeclatura similar a C,
em que um inteiro sem sinal de 8 _bits_ é do tipo `UInt8`,
e um inteiro com sinal de 32 _bits_ é do tipo `Int32`.
Como todos os tipos em Swift, esses tipos inteiros possuem nomes com a primeira letra maiúscula.

### Limites Inteiros 

Você pode acessar o valor mínimo e máximo de cada tipo inteiro
com as propriedades `min` e `max`:

```swift
let minValue = UInt8.min  // `minValue` é igual a 0, e é do tipo `UInt8`
let maxValue = UInt8.max  // `maxValue` é igual a 255, e é do tipo `UInt8`
```

Os valores dessas propriedades têm o tamanho apropriado para o tipo numérico
(como o `UInt8` do exemplo acima)
e, por isso, podem ser usados em expressões com outros valores do mesmo tipo.

### Int

Na maioria dos casos, você não precisa escolher um tamanho específico de inteiro para usar no seu código.
Swift dispõe de um inteiro adicional, `Int`,
que possui o mesmo tamanho que a palavra nativa da plataforma atual:

- Em uma plataforma de 32 _bits_, `Int` é do mesmo tamanho que o `Int32`.
- Em uma plataforma de 64 _bits_, `Int` é do mesmo tamanho que o `Int64`.

A menos que você precise trabalhar com um tamanho específico de inteiro,
sempre use `Int` para valores inteiros no seu código.
Isso contribui para a consistência do código e interoperabilidade.
Mesmo em plataforma de 32 _bits_, `Int` pode armazenar qualquer valor entre `-2,147,483,648` e `2,147,483,647`,
e é sufucientemente grande para muitos intervalos de números inteiros.

### UInt

Swift também fornece um tipo inteiro sem sinal, `UInt`,
que possui o mesmo tamanho que a palavra nativa da plataforma atual:

- Em uma plataforma de 32 _bits_, `UInt` é do mesmo tamanho que o `UInt32`.
- Em uma plataforma de 64 _bits_, `UInt` é do mesmo tamanho que o `UInt64`.

> Nota: Use `UInt` apenas quando você precisar especificamente
> de um tipo inteiro sem sinal com o mesmo tamanho que a palavra nativa da plataforma atual.
> Se esse não for o caso, `Int` é preferido,
> mesmo quando os valores para serem armazenados são conhecidamente não negativos.
> O uso consistente do `Int` para valores inteiros contribui para a interpolaridade do código,
> evitando a necessidade de conversão entre diferentes tipos numéricos,
> e corresponde à inferência de tipo de inteiro, como descrito em <doc:TheBasics#Type-Safety-and-Type-Inference>.

## Números de Ponto Flutuante

*Números de ponto flutuante* são números com um componente fracionário,
como `3.14159`, `0.1` e `-273.15`.

Tipos de ponto flutuante podem representar uma gama muito maior de valores do que tipos inteiros,
e podem armazenar números que são muito maiores ou menores do que podem ser armazenados em um `Int`.
Swift fornece dois tipos de números de ponto flutuante com sinal:

- `Double` representa um número de ponto flutuante de 64 _bits_.
- `Float` representa um número de ponto flutuante de 32 _bits_.

> Nota: `Double` tem uma precisão de pelo menos 15 dígitos decimais,
> enquanto a precisão de `Float` pode ser de apenas 6 dígitos decimais.
> O tipo de ponto flutuante apropriado a ser usado depende da natureza e do intervalo de
> valores com os quais você precisa trabalhar em seu código.
> Em situações em que qualquer tipo seria apropriado, `Double` é preferivel.


## Segurança de Tipo e Inferência de Tipo

Swift é uma linguagem **type-safe**.
Uma linguagem **type-safe** encoraja você a ser claro sobre
os tipos de valores com os quais seu código pode trabalhar.
Se parte do seu código requer uma `String`, você não pode passar um `Int` por engano.

Como Swift é **type-safe**,
o compilador realiza **verificações de tipo** ao compilar seu código
e sinaliza quaisquer tipos incompatíveis como erros.
Isso permite que você detecte e corrija erros o mais cedo possível no processo de desenvolvimento.

A verificação de tipo ajuda a evitar erros quando você está trabalhando com diferentes tipos de valores.
No entanto, isso não significa que você precisa especificar o tipo de
cada constante e variável que você declara.
Se você não especificar o tipo de valor que precisa,
Swift usa **inferência de tipo** para descobrir o tipo apropriado.
A inferência de tipo permite que um compilador
deduza o tipo de uma expressão específica automaticamente quando compila seu código,
simplesmente examinando os valores que você fornece.

Por causa da inferência de tipo, Swift requer muito menos declarações de tipo
do que linguagens como C ou Objective-C.
Constantes e variáveis ​​ainda são explicitamente tipadas,
mas muito do trabalho de especificar seu tipo é feito para você.

A inferência de tipo é particularmente útil
quando você declara uma constante ou variável com um valor inicial.
Isso geralmente é feito atribuindo um **valor literal**
à constante ou variável no ponto em que você a declara.
(Um valor literal é um valor que aparece diretamente no seu código-fonte,
como `42` e `3.14159` nos exemplos abaixo.)

Por exemplo, se você atribuir um valor literal de `42` a uma nova constante
sem dizer qual é o tipo dela,
Swift infere que você quer que a constante seja um `Int`,
porque você a inicializou com um número que parece um inteiro:

```swift
let meaningOfLife = 42
// `meaningOfLife` é inferida como do tipo `Int`
```

Da mesma forma, se você não especificar um tipo para um literal de ponto flutuante,
Swift infere que você deseja criar um `Double`:

```swift
let pi = 3.14159
// `pi` é inferida como do tipo `Double`
```

Swift sempre escolhe `Double` (em vez de `Float`)
ao inferir o tipo de números de ponto flutuante.

Se você combinar inteiros e literais de ponto flutuante em uma expressão,
um tipo de `Double` será inferido do contexto:

```swift
let anotherPi = 3 + 0.14159
// `anotherPi` também é inferida como do tipo `Double`
```

O valor literal `3` não tem um tipo explícito em si mesmo,
e assim um tipo de saída apropriado de `Double` é inferido
da presença de um literal de ponto flutuante como parte da adição.

## Literais Numéricos

Literais inteiros podem ser escritos como:

- Um número *decimal*, sem prefixo
- Um número *binário*, com um prefixo `0b`
- Um número *octal*, com um prefixo `0o`
- Um número *hexadecimal*, com um prefixo `0x`

Todos esses literais inteiros têm um valor decimal de `17`:

```swift
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 em notação binária
let octalInteger = 0o21           // 17 em notação octal
let hexadecimalInteger = 0x11     // 17 em notação hexadecimal
```

Literais de ponto flutuante podem ser decimais (sem prefixo),
ou hexadecimais (com um prefixo `0x`).
Eles devem sempre ter um número (ou número hexadecimal) em ambos os lados do ponto decimal.
Floats decimais também podem ter um **expoente** opcional,
indicado por um `e` maiúsculo ou minúsculo;
floats hexadecimais devem ter um expoente,
indicado por um `p` maiúsculo ou minúsculo.

Para números decimais com um expoente de `x`,
o número base é multiplicado por 10ˣ:

- `1.25e2` significa 1.25 x 10², ou `125.0`.
- `1.25e-2` significa 1.25 x 10⁻², ou `0.0125`.

Para números hexadecimais com um expoente de `x`,
o número base é multiplicado por 2ˣ:

- `0xFp2` significa 15 x 2², ou `60.0`.
- `0xFp-2` significa 15 x 2⁻², ou `3.75`.

Todos esses literais de ponto flutuante têm um valor decimal de `12.1875`:

```swift
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

Literais numéricos podem conter formatação extra para torná-los mais fáceis de ler.
Tanto inteiros quanto flutuantes podem ser preenchidos com zeros extras
e podem conter sublinhados para ajudar na legibilidade.
Nenhum tipo de formatação afeta o valor subjacente do literal:

```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

## Conversão de Tipo Numérico

Use o tipo `Int` para todas as constantes e variáveis ​​inteiras de uso geral em seu código,
mesmo que sejam conhecidas por serem não negativas.
Usar o tipo inteiro padrão em situações cotidianas significa que
constantes e variáveis ​​inteiras são imediatamente interoperáveis ​​em seu código
e corresponderão ao tipo inferido para valores literais inteiros.

Use outros tipos inteiros somente quando forem especificamente necessários para a tarefa em questão,
por causa de dados explicitamente dimensionados de uma fonte externa,
ou para desempenho, uso de memória ou outra otimização necessária.
Usar tipos explicitamente dimensionados nessas situações
ajuda a capturar quaisquer _overflow_ de valor acidental
e documenta implicitamente a natureza dos dados que estão sendo usados.

### Conversão de inteiros

O intervalo de números que podem ser armazenados em uma constante ou variável inteira
é diferente para cada tipo numérico.
Uma constante ou variável `Int8` pode armazenar números entre `-128` e `127`,
enquanto uma constante ou variável `UInt8` pode armazenar números entre `0` e `255`.
Um número que não se encaixa em uma constante ou variável de um tipo inteiro dimensionado
é reportado como um erro quando seu código é compilado:

```swift
let cannotBeNegative: UInt8 = -1
// `UInt8` não pode armazenar números negativos, então isso irá reportar um erro
let tooBig: Int8 = Int8.max + 1
// `Int8` não pode armazenar um número maior que seu valor máximo,
// e isso também reportará um erro
```

Como cada tipo numérico pode armazenar um intervalo diferente de valores,
você deve optar pela conversão de tipo numérico caso a caso.
Essa abordagem `opt-in` previne erros de conversão ocultos
e ajuda a tornar as intenções de conversão de tipo explícitas em seu código.

Para converter um tipo de número específico em outro,
você inicializa um novo número do tipo desejado com o valor existente.
No exemplo abaixo,
a constante `twoThousand` é do tipo `UInt16`,
enquanto a constante `one` é do tipo `UInt8`.
Elas não podem ser adicionadas diretamente,
porque não são do mesmo tipo.
Em vez disso, o exemplo abaixo usa `UInt16(one)` para criar
uma nova `UInt16` inicializada com o valor de `one`,
e usa esse valor no lugar do original:

```swift
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

Como ambos os lados da adição agora são do tipo `UInt16`,
a adição é permitida.
A constante de saída (`twoThousandAndOne`) é inferida como sendo do tipo `UInt16`,
porque é a soma de dois valores `UInt16`.

`SomeType(ofInitialValue)` é a maneira padrão de chamar o inicializador de um tipo Swift
e passar um valor inicial.
Nos bastidores, `UInt16` tem um inicializador que aceita um valor `UInt8`,
e então esse inicializador é usado para fazer um novo `UInt16` a partir de um `UInt8` existente.
Você não pode passar **qualquer** tipo aqui, no entanto ---
ele tem que ser um tipo para o qual `UInt16` fornece um inicializador.
Estender tipos existentes para fornecer inicializadores que aceitam novos tipos
(incluindo suas próprias definições de tipo)
é abordado em <doc:Extensions>.

### Conversão de Inteiros e de Ponto Flutuante

As conversões entre tipos numéricos de inteiros e de ponto flutuante devem ser explicitadas:

```swift
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// `pi` é igual a 3.14159, e é inferido como do tipo `Double`
```

O valor da constante `three` é usado para criar um novo valor do tipo `Double`,
para que ambos os lados da adição sejam do mesmo tipo.
Sem essa conversão em vigor, a adição não seria permitida.

A conversão de ponto flutuante para inteiro também deve ser explicota.
Um tipo inteiro pode ser inicializado com um valor `Double` ou `Float`:

```swift
let integerPi = Int(pi)
// `integerPi` é igual a 3, e é inferido como do tipo `Int`
```

Valores de ponto flutuante são sempre truncados quando usados ​​para inicializar um novo valor inteiro dessa forma.
Isso significa que `4.75` se torna `4` e `-3.9` se torna `-3`.

> Nota: As regras para combinar constantes e variáveis ​​numéricas são diferentes
> das regras para literais numéricos.
> O valor literal `3` pode ser adicionado diretamente ao valor literal `0.14159`,
> porque  um literal numérico não têm um tipo explícito por si só.
> Seu tipo é inferido apenas no ponto em que são avaliados pelo compilador.

## Apelidos de Tipo

**Apelidos de tipo** definem um nome alternativo para um tipo existente.
Você define apelidos de tipo com a palavra-chave `typealias`.

Apelidos de tipo são úteis quando você quer se referir a um tipo existente
por um nome que seja contextualmente mais apropriado,
como ao trabalhar com dados de um tamanho específico de uma fonte externa:

```swift
typealias AudioSample = UInt16
```

Depois de definir um apelido de tipo,
você pode usar o apelido em qualquer lugar em que usaria o nome original:

```swift
var maxAmplitudeFound = AudioSample.min
// `maxAmplitudeFound` agora é 0
```

Aqui, `AudioSample` é definido como um apelido para `UInt16`.
Por ser um apelido,
a chamada para `AudioSample.min` na verdade chama `UInt16.min`,
que fornece um valor inicial de `0` para a variável `maxAmplitudeFound`.

## Booleanos

O Swift tem um tipo *Booleano* básico, chamado `Bool`.
Os valores booleanos são chamados de **lógicos**,
porque eles só podem ser verdadeiros ou falsos.
Swift fornece dois valores constantes booleanos,
`true` e `false`:

```swift
let orangesAreOrange = true
let turnipsAreDelicious = false
```

Os tipos de `orangesAreOrange` e `turnipsAreDelicious`
foram inferidos como `Bool` pelo fato de que
eles foram inicializados com valores literais booleanos.
Assim como com `Int` e `Double` acima,
você não precisa declarar constantes ou variáveis ​​como `Bool`
se você defini-las como `true` ou `false` assim que criá-las.
A inferência de tipos ajuda a tornar o código mais conciso e legível
quando inicializa constantes ou variáveis ​​com outros valores cujo tipo já é conhecido.

Os valores booleanos são particularmente úteis quando você trabalha com instruções condicionais
como a instrução `if`:

```swift
if turnipsAreDelicious {
   print("Mmm, tasty turnips!")
} else {
   print("Eww, turnips are horrible.")
}
// Imprime "Eww, turnips are horrible."
```

Instruções condicionais como a instrução `if` são abordadas com mais detalhes em <doc:ControlFlow>.

A segurança de tipo impede que valores não booleanos sejam substituídos por `Bool`.
O exemplo a seguir relata um erro de tempo de compilação:

```swift
let i = 1
if i {
   // este exemplo não será compilado e reportará um erro
}
```

Entretanto, o exemplo alternativo abaixo é válido:

```swift
let i = 1
if i == 1 {
   // esse exemplo será compilado com sucesso
}
```

O resultado da comparação `i == 1` é do tipo `Bool`,
e então este segundo exemplo passa na verificação de tipo.
Comparações como `i == 1` são discutidas em <doc:BasicOperators>.

Assim como outros exemplos de segurança de tipo em Swift,
esta abordagem evita erros acidentais
e garante que a intenção de uma seção específica do código esteja sempre clara.

## Tuplas

*Tuplas* agrupam vários valores em um único valor composto.
Os valores dentro de uma tupla podem ser de qualquer tipo
e não precisam ser do mesmo tipo uns dos outros.

Neste exemplo, `(404, "Not Found")` é uma tupla que descreve um **código de status HTTP**.
Um código de status HTTP é um valor especial retornado por um servidor web sempre que você solicita uma página web.
Um código de status `404 Not Found` é retornado se você solicitar uma página web que não existe.

```swift
let http404Error = (404, "Not Found")
// `http404Error` é do tipo `(Int, String)`, e igual a (404, "Not Found")
```

A tupla `(404, "Not Found")` agrupa um `Int` e uma `String`
para dar ao código de status HTTP dois valores separados:
um número e uma descrição legível por humanos.
Ele pode ser descrito como “uma tupla do tipo `(Int, String)`”.

Você pode criar tuplas de qualquer permutação de tipos,
e elas podem conter quantos tipos diferentes você quiser.
Não há nada que impeça você de ter
uma tupla do tipo `(Int, Int, Int)`, ou `(String, Bool)`,
ou de fato qualquer outra permutação que você precise.

Você pode **decompor** o conteúdo de uma tupla em constantes ou variáveis ​​separadas,
que você então acessa normalmente:

```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Imprime "The status code is 404"
print("The status message is \(statusMessage)")
// Imprime "The status message is Not Found"
```

Se você só precisa de alguns valores da tupla,
ignore partes da tupla com um sublinhado (`_`)
quando você decompõe a tupla:

```swift
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Imprime "The status code is 404"
```

Alternativamente,
acesse os valores dos elementos individuais em uma tupla usando números de índice começando em zero:

```swift
print("The status code is \(http404Error.0)")
// Imprime "The status code is 404"
print("The status message is \(http404Error.1)")
// Imprime "The status message is Not Found"
```

Você pode nomear os elementos individuais em uma tupla quando a tupla é definida:

```swift
let http200Status = (statusCode: 200, description: "OK")
```

Se você nomear os elementos em uma tupla,
você pode usar os nomes dos elementos para acessar os valores desses elementos:

```swift
print("The status code is \(http200Status.statusCode)")
// Imprime "The status code is 200"
print("The status message is \(http200Status.description)")
// Imprime "The status message is OK"
```

Uma função que tenta recuperar uma página da web pode retornar o tipo de tupla `(Int, String)`
para descrever o sucesso ou a falha da recuperação da página.
Ao retornar uma tupla com dois valores distintos,
cada um de um tipo diferente,
a função fornece informações mais úteis sobre seu resultado
do que se pudesse retornar apenas um único valor de um único tipo.
Para obter mais informações, consulte <doc:Functions#Functions-with-Multiple-Return-Values>.

> Nota: Tuplas são úteis para grupos simples de valores relacionados.
> Elas não são adequadas para a criação de estruturas de dados complexas.
> Se sua estrutura de dados provavelmente for mais complexa,
> modele-a como uma classe ou estrutura, em vez de uma tupla.
> Para obter mais informações, consulte <doc:ClassesAndStructures>.

## Opcionais

Você usa **opcionais** em situações em que um valor pode estar ausente.
Um opcional representa duas possibilidades:
Ou *há* um valor, e você pode desempacotar o opcional para acessar esse valor,
ou *não há* nenhum valor.

Como exemplo de um valor que pode estar faltando,
o tipo `Int` em Swift tem um inicializador
que tenta converter um valor `String` em um valor `Int`.
No entanto, apenas algumas _strings_ podem ser convertidas em inteiros.
A _string_ `"123"` pode ser convertida no valor numérico `123`,
mas a _string_ `"hello, world"` não tem um valor numérico correspondente.
O exemplo abaixo usa o inicializador para tentar converter uma `String` em um `Int`:

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// O tipo de `convertedNumber` é `Int` opcional
```

Como o inicializador pode falhar,
ele retorna um `Int` **opcional**, em vez de um `Int`.
Um `Int` opcional é escrito como `Int?`, não `Int`.
O ponto de interrogação indica que o valor que ele contém é opcional,
o que significa que ele pode conter **algum** valor `Int`,
ou pode não conter **nenhum** valor.
(Ele não pode conter nada mais, como um valor `Bool` ou um valor `String`.
Ele é um `Int` ou não é nada.)

### nil

Você define uma variável opcional para um estado sem valor
atribuindo a ela o valor especial `nil`:

```swift
var serverResponseCode: Int? = 404
// `serverResponseCode` contém um valor `Int` de 404
serverResponseCode = nil
// `serverResponseCode` agora não contém nenhum valor
```

Se você definir uma variável opcional sem fornecer um valor padrão,
a variável será automaticamente definida como `nil`:

```swift
var surveyAnswer: String?
// `surveyAnswer` é automaticamente definida como `nil`
```

Você pode usar uma instrução `if` para descobrir se um opcional contém um valor
comparando o opcional com `nil`.
Você realiza essa comparação com o operador “igual a” (`==`)
ou o operador “diferente de” (`!=`).

Se um opcional tiver um valor, ele é considerado “diferente de” `nil`:

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)

if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// Imprime "convertedNumber contains some integer value."
```

Você não pode usar `nil` com constantes ou variáveis ​​não opcionais.
Se uma constante ou variável no seu código precisa trabalhar com
a ausência de um valor sob certas condições,
declare-a como um valor opcional do tipo apropriado.
Uma constante ou variável que é declarada como um valor não opcional
tem a garantia de nunca conter um valor `nil`.
Se você tentar atribuir `nil` a um valor não opcional,
você obterá um erro de tempo de compilação.

Essa separação de valores opcionais e não opcionais
permite que você marque explicitamente quais informações podem estar faltando
e facilita a escrita de código que lida com ausência de valores.
Você não pode tratar acidentalmente um opcional como se fosse não opcional
porque isso produz um erro em tempo de compilação.
Depois de desempacotar o valor,
nenhum outro código que funciona com esse valor precisa verificar `nil`,
então não há necessidade de verificar repetidamente o mesmo valor
em diferentes partes do seu código.

Quando você acessa um valor opcional,
seu código sempre lida com o caso `nil` e não `nil`.
Há várias coisas que você pode fazer quando um valor está faltando,
conforme descrito nas seções a seguir:

- Pular o código que opera no valor quando ele é `nil`.

- Propagar o valor `nil`, retornando `nil`
ou usando o operador `?.` descrito em <doc:OptionalChaining>.

- Fornecer um valor de _fallback_, usando o operador `??`.

- Parar a execução do programa, usando o operador `!`.

> Nota:
> Em Objective-C, `nil` é um ponteiro para um objeto inexistente.
> Em Swift, `nil` não é um ponteiro --- é a ausência de um valor de um certo tipo.
> Opcionais de **qualquer** tipo podem ser definidos como `nil`, não apenas tipos de objeto.

### _Binding_ Opcional

Você usa **_binding_ opcional** para descobrir se um opcional contém um valor,
e se sim, para tornar esse valor disponível como uma constante ou variável temporária.
Um _binding_ opcional pode ser usada com instruções `if`, `guard` e `while`
para verificar um valor dentro de um opcional,
e para extrair esse valor em uma constante ou variável,
como parte de uma única ação.
Para mais informações sobre `if`, `guard` e `while`, consulte <doc:ControlFlow>.

Escreva um _binding_ opcional para uma instrução `if` da seguinte maneira:

```
if let <#constantName#> = <#someOptional#> {
   <#statements#>
}
```

Você pode reescrever o exemplo `possibleNumber` da
seção <doc:TheBasics#Optionals>
para usar _binding_ opcional em vez de desempacotamente forçado:

```swift
if let actualNumber = Int(possibleNumber) {
   print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
   print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
}
// Imprime "The string "123" has an integer value of 123"
```

Este código pode ser lido como:

“Se o opcional `Int` retornado por `Int(possibleNumber)` contém um valor,
defina uma nova constante chamada `actualNumber` para o valor contido no opcional.”

Se a conversão for bem-sucedida,
a constante `actualNumber` se torna disponível para uso dentro
do primeiro ramo da declaração `if`.
Ela já foi inicializada com o valor contido **dentro** do opcional,
e então você não usa o sufixo `!` para acessar seu valor.
Neste exemplo, `actualNumber` é simplesmente usado para imprimir o resultado da conversão.

Se você não precisar se referir à constante ou variável original e opcional
depois de acessar o valor que ela contém,
você pode usar o mesmo nome para a nova constante ou variável:

```swift
let myNumber = Int(possibleNumber)
// Aqui `myNumber` é um inteiro opcional
if let myNumber = myNumber {
    // Aqui `myNumber` um inteiro não opcional
    print("My number is \(myNumber)")
}
// Imprime "My number is 123"
```

Este código começa verificando se `myNumber` contém um valor,
assim como o código no exemplo anterior.
Se `myNumber` tiver um valor,
Uma nova constante chamada `myNumber` é definida como esse valor.
Dentro do corpo da declaração `if`,
escrever `myNumber` se refere a essa nova constante não opcional.
Antes do início da declaração `if` e após seu fim,
escrever `myNumber` se refere à constante inteira opcional.

Como esse tipo de código é tão comum,
você pode usar uma abreviação para desempacotar um valor opcional:
escreva apenas o nome da constante ou variável que você está desempacotando.
A nova constante ou variável desempacotando
implicitamente usa o mesmo nome do valor opcional.

```swift
if let myNumber {
    print("My number is \(myNumber)")
}
// Imprime "My number is 123"
```

Você pode usar constantes e variáveis ​​com _binding_ opcional.
Se você quisesse manipular o valor de `myNumber`
dentro do primeiro ramo da declaração `if`,
você poderia escrever `if var myNumber` em vez disso,
e o valor contido dentro do opcional
seria disponibilizado como uma variável em vez de uma constante.
As alterações que você fizer em `myNumber` dentro do corpo da declaração `if`
se aplicam somente àquela variável local,
**não** à constante ou variável original e opcional que você desempacotou.

Você pode incluir quantas _binding_ opcionais e condições booleanas
em uma única instrução `if` forem necessárias,
separadas por vírgulas.
Se qualquer um dos valores nos _binding_ opcionais for `nil`
ou qualquer condição booleana for avaliada como `false`,
toda a condição da instrução `if`
será considerada `false`.
As seguintes instruções `if` são equivalentes:

```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
   print("\(firstNumber) < \(secondNumber) < 100")
}
// Imprime "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Imprime "4 < 42 < 100"
```

> Nota: Constantes e variáveis ​​criadas com _binding_ opcional em uma instrução `if`
> estão disponíveis somente dentro do corpo da instrução `if`.
> Em contraste, as constantes e variáveis ​​criadas com uma instrução `guard`
> estão disponíveis nas linhas de código que seguem a instrução `guard`,
> conforme descrito em <doc:ControlFlow#Early-Exit>.

### Fornecendo um Valor de _Fallback_

Outra maneira de lidar com um valor ausente é fornecer
um valor padrão usando o operador _nil-coalescing_ (`??`).
Se o opcional à esquerda de `??` não for `nil`,
esse valor será desembrulhado e usado.
Caso contrário, o valor à direita de `??` será usado.
Por exemplo,
o código abaixo cumprimenta alguém pelo nome, se um for especificado,
e usa uma saudação genérica quando o nome for `nil`.

```swift
let name: String? = nil
let greeting = "Hello, " + (name ?? "friend") + "!"
print(greeting)
// Imprime "Hello, friend!"
```

Para obter mais informações sobre o uso de `??` para fornecer um valor de _fallback_,
consulte <doc:BasicOperators#Nil-Coalescing-Operator>.

### Desempacotamento Forçado

Quando `nil` representa uma falha irrecuperável,
como um erro de programador ou estado corrompido,
você pode acessar o valor subjacente
adicionando um ponto de exclamação (`!`) ao final do nome do opcional.
Isso é conhecido como **forçar o desempacotamento** do valor do opcional.
Quando você força o desempacotamento de um valor não `nil`,
o resultado é seu valor desempacotado.
Forçar o desempacotamento de um valor `nil` dispara um erro em tempo de execução.

O `!` é, efetivamente, uma grafia mais curta de [`fatalError(_:file:line:)`][].
Por exemplo, o código abaixo mostra duas abordagens equivalentes:

[`fatalError(_:file:line:)`]: https://developer.apple.com/documentation/swift/fatalerror(_:file:line:)

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)

let number = convertedNumber!

guard let number = convertedNumber else {
    fatalError("The number was invalid")
}
```

Ambas as versões do código acima dependem de `convertedNumber`
sempre contendo um valor.
Escrever esse requisito como parte do código,
usando qualquer uma das abordagens acima,
permite que seu código verifique se o requisito é verdadeiro em tempo de execução.

Para obter mais informações sobre como impor requisitos de dados
e verificar suposições em tempo de execução,
consulte <doc:TheBasics#Assertions-and-Preconditions>.

### Opcionais Implicitamente Desempacotados

Conforme descrito acima,
opcionais indicam que uma constante ou variável pode ter "nenhum valor".
Opcionais podem ser verificados com uma instrução `if` para ver se um valor existe,
e podem ser condicionalmente desempacotados com _binding_ opcionais
para acessar o valor do opcional se ele existir.

Às vezes fica claro na estrutura de um programa que um opcional **sempre** terá um valor,
depois que esse valor for definido pela primeira vez.
Nesses casos, é útil remover a necessidade
de verificar e desempacotar o valor do opcional toda vez que ele for acessado,
porque pode-se presumir com segurança que ele tem um valor o tempo todo.

Esses tipos de opcionais são definidos como **opcionais implicitamente desempacotados**.
Você escreve um opcional implicitamente desempacotado colocando um ponto de exclamação (`String!`)
em vez de um ponto de interrogação (`String?`) após o tipo que você quer tornar opcional.
Em vez de colocar um ponto de exclamação após o nome do opcional quando você o usa,
você coloca um ponto de exclamação após o tipo do opcional quando você o declara.

Opcionais implicitamente desempacotados são úteis quando
o valor de um opcional é confirmado como existente imediatamente após o opcional ser definido pela primeira vez
e pode definitivamente ser assumido como existente em todos os pontos depois disso.
O uso primário de opcionais implicitamente desempacotados em Swift é durante a inicialização de classes,
conforme descrito em <doc:AutomaticReferenceCounting#Unowned-References-and-Implicitly-Unwrapped-Optional-Properties>.

Não use um opcional implicitamente desempacotado quando houver a possibilidade de
uma variável se tornar `nil` em um ponto posterior.
Sempre use um tipo opcional normal se precisar verificar um valor `nil`
durante o tempo de vida de uma variável.

Um opcional implicitamente desempacotado é um opcional normal nos bastidores,
mas também pode ser usado como um valor não opcional,
sem a necessidade de desempacotar o valor opcional toda vez que ele for acessado.
O exemplo a seguir mostra a diferença de comportamento entre
uma _string_ opcional e uma _string opcional_ implicitamente desempacotada
ao acessar seu valor encapsulado como uma `String` explícita:

```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // necessário ponto de exclamação

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // não necessário ponto de exclamação
```

Você pode pensar em um opcional implicitamente desempacotado como
dando permissão para que o opcional seja desempacotado à força, se necessário.
Quando você usa um valor opcional implicitamente desempacotado,
o compilador primeiro tenta usá-lo como um valor opcional comum;
se ele não puder ser usado como um opcional, valor é desempacotado à força.
No código acima,
o valor opcional `assumedString` é desempacotado à força
antes de atribuir seu valor a `implicitString`
porque `implicitString` tem um tipo explícito e não opcional de `String`.
No código abaixo,
`optionalString` não tem um tipo explícito
então é um opcional comum.

```swift
let optionalString = assumedString
// O tipo de `optionalString` é "String?" e `assumedString` é desempacotado à força.
```

Se um opcional implicitamente desempacotado for `nil` e você tentar acessar seu valor encapsulado,
você disparará um erro de tempo de execução.
O resultado é exatamente o mesmo que se você escrevesse um ponto de exclamação
para forçar o desempacotamento de um opcional normal que não contém um valor.

Você pode verificar se um opcional implicitamente desempacotado é `nil`
da mesma forma que verifica um opcional normal:

```swift
if assumedString != nil {
   print(assumedString!)
}
// Imprime "An implicitly unwrapped optional string."
```

Você também pode usar um opcional implicitamente desempacotado com opcional _binding_,
para verificar e desempacotado seu valor em uma única declaração:

```swift
if let definiteString = assumedString {
   print(definiteString)
}
// Imprime "An implicitly unwrapped optional string."
```

## Tratamento de Erros

Você usa **tratamento de erros** para responder a condições de erro
que seu programa pode encontrar durante a execução.

Ao contrário dos opcionais,
que podem usar a presença ou ausência de um valor
para comunicar o sucesso ou falha de uma função,
o tratamento de erros permite que você determine a causa especifica da falha,
e, se necessário, propague o erro para outra parte do seu programa.

Quando uma função encontra uma condição de erro, ela **lança** um erro.
O chamador dessa função pode então **capturar** o erro e responder apropriadamente.

```swift
func canThrowAnError() throws {
   // esta função pode ou não gerar um erro
}
```

Uma função indica que pode lançar um erro
ao incluir a palavra-chave `throws` em sua declaração.
Quando você chama uma função que pode lançar um erro,
você acrescenta a palavra-chave `try` à expressão.

O Swift propaga automaticamente os erros para fora do escopo atual
até que sejam manipulados por uma cláusula `catch`.

```swift
do {
   try canThrowAnError()
   // nenhum erro lançado
} catch {
   // algum erro lançado
}
```

Uma declaração `do` cria um novo escopo de contenção,
que permite que erros sejam propagados para uma ou mais cláusulas `catch`.

Aqui está um exemplo de como o tratamento de erros pode ser usado
para responder a diferentes condições de erro:

```swift
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

Neste exemplo, a função `makeASandwich()` lançará um erro
se não houver pratos limpos disponíveis
ou se algum ingrediente estiver faltando.
Como `makeASandwich()` pode lançar um erro,
a chamada de função é encapsulada em uma expressão `try`.
Ao encapsular a chamada de função em uma instrução `do`,
quaisquer erros lançados serão propagados
para as cláusulas `catch` fornecidas.

Se nenhum erro for lançado, a função `eatASandwich()` será chamada.
Se um erro for lançado e ele corresponder ao caso `SandwichError.outOfCleanDishes`,
então a função `washDishes()` será chamada.
Se um erro for lançado e ele corresponder ao caso `SandwichError.missingIngredients`,
então a função `buyGroceries(_:)` será chamada
com o valor `[String]` associado capturado pela cláusula `catch`.

Lançar, capturar e propagar erros é abordado com mais detalhes em
<doc:ErrorHandling>.

## Asserções e Precondições

**Asserções** e **precondições**
são verificações que acontecem em tempo de execução.
Você as usa para garantir que uma condição essencial seja satisfeita
antes de executar qualquer código adicional.
Se a condição booleana na afirmação ou pré-condição
for avaliada como `true`,
a execução do código continua normalmente.
Se a condição for avaliada como `false`,
o estado atual do programa é inválido;
a execução do código termina e seu aplicativo é encerrado.

Você usa asserções e precondições
para expressar as suposições que você faz
e as expectativas que você tem
ao codificar,
para que você possa incluí-las como parte do seu código.
Asserções ajudam você a encontrar erros e suposições incorretas durante o desenvolvimento,
e as precondições ajudam você a detectar problemas na produção.

Além de verificar suas expectativas em tempo de execução,
asserções e precondições também se tornam uma forma útil de documentação
dentro do código.
Ao contrário das condições de erro discutidas em <doc:TheBasics#Error-Handling> acima,
asserções e precondições não são usadas
para erros recuperáveis ​​ou esperados.
Como uma asserção ou precondição com falha
indica um estado de programa inválido,
não há como capturar uma asserção com falha.
A recuperação de um estado inválido é impossível.
Quando uma asserção falha,
pelo menos uma parte dos dados do programa é inválida ---
mas você não sabe por que é inválida
ou se um estado adicional também é inválido.

Usar asserções e precondições
não é um substituto para projetar seu código de tal forma
que condições inválidas sejam improváveis ​​de surgir.
No entanto,
usá-las para impor dados e estados válidos
faz com que seu programa seja encerrado de forma mais previsível
se um estado inválido ocorrer,
e ajuda a tornar o problema mais fácil de depurar.
Quando as suposições não são verificadas,
você pode não notar esse tipo de problema até muito mais tarde
quando o código em outro lugar começar a falhar visivelmente,
e depois que os dados do usuário forem silenciosamente corrompidos.
Parar a execução assim que um estado inválido for detectado
também ajuda a limitar os danos causados ​​por esse estado inválido.

A diferença entre asserções e precondições está em quando elas são verificadas:
Asserções são verificadas apenas em compilações em modo _debug_,
mas as precondições são verificadas em compilações em modo _debug_ e _release_.
Em compilações em modo _release_,
a condição dentro de uma asserção não é avaliada.
Isso significa que você pode usar quantas asserções quiser
durante seu processo de desenvolvimento,
sem impactar o desempenho em produção.

### Debugando com Asserções

Você escreve uma asserção chamando a função
[`assert(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1541112-assert)
da biblioteca padrão.
Você passa para essa função uma expressão que avalia como `true` ou `false`
e uma mensagem para exibir se o resultado da condição for `false`.
Por exemplo:

```swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// Essa asserção fala porque -3 não é maior que 0.
```

Neste exemplo, a execução do código continua se `age >= 0` for avaliado como `true`,
isto é, se o valor de `age` for não negativo.
Se o valor de `age` for negativo, como no código acima,
então `age >= 0` será avaliado como `false`,
e a asserção falha, encerrando o programa.

Você pode omitir a mensagem de asserção ---
por exemplo, quando ela apenas repetiria a condição como prosa.

```swift
assert(age >= 0)
```

Se o código já verificar a condição,
você usa a função
[`assertionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539616-assertionfailure)
para indicar que uma asserção falhou.
Por exemplo:

```swift
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```

### Impondo Precondições

Use uma precondição sempre que uma condição tiver o potencial de ser falsa,
mas deve **definitivamente** ser verdadeira para que seu código continue a execução.
Por exemplo, use uma precondição para verificar se um subscrito não está fora dos limites,
ou para verificar se uma função recebeu um valor válido.

Você escreve uma precondição chamando a função
[`precondition(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1540960-precondition).
Você passa para essa função uma expressão que avalia como `true` ou `false`
e uma mensagem para exibir se o resultado da condição for `false`.
Por exemplo:

```swift
// Na implementação de um subscrito...
precondition(index > 0, "Index must be greater than zero.")
```

Você também pode chamar a função
[`preconditionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure)
para indicar que ocorreu uma falha ---
por exemplo, se o caso padrão de um _switch_ foi usado,
mas todos os dados de entrada válidos deveriam ter sido manipulados
por um dos outros casos do _switch_.

> Nota: Se você compilar no modo não verificado (`-Ounchecked`),
> as precondições não serão verificadas.
> O compilador assume que as precondições são sempre verdadeiras,
> e otimiza seu código de acordo.
> No entanto, a função `fatalError(_:file:line:)` sempre interrompe a execução,
> independentemente das configurações de otimização.
>
> Você pode usar a função `fatalError(_:file:line:)`
> durante a prototipagem e o desenvolvimento inicial
> para criar _stubs_ para funcionalidades que ainda não foram implementadas,
> escrevendo `fatalError("Unimplemented")` como a implementação do _stub_.
> Como os erros fatais nunca são otimizados,
> ao contrário de asserções ou precondições,
> você pode ter certeza de que a execução sempre para
> se encontrar uma implementação de _stub_.





