

# Tipos Aninhados

Enumerações são frequentemente criadas para dar suporte a uma funcionalidade especifica de uma classe ou estrutura.
Similarmente, pode ser conveniente definir classes e estruturas de utilidade
puramente para o uso dentro de um contexto de um tipo mais complexo.
Para fazer isso, o Swift permite que você defina *tipos aninhados*,
nos quais você aninha enumerações, classes e estruturas de suporte
dentro da definição do tipo que elas suportam.

## Overview

Para aninhar um tipo dentro de outro tipo,
escreva sua definição dentro das chaves externas do tipo que ele suporta.
Os tipos podem ser aninhados em até quantos níveis forem necessários.

## Tipos Aninhados em Ação

O exemplo abaixo define a estrutura chamada `BlackjackCard`,
que modela uma carta de baralho usada no jogo de Blackjack.
A estrutra `BlackjackCard` contém dois tipos enumerados aninhados
chamados de `Suit` e `Rank`.

Em Blackjack, as cartas de Ás têm o valor de um ou onze.
Este recurso é representado por uma estrutura chamada `Values`,
que está aninhada dentro da enumeração `Rank`:

```swift
struct BlackjackCard {

   // enumeração Suit aninhada
   enum Suit: Character {
      case spades = "♠", hearts = "♡", diamonds = "♢", clubs = "♣"
   }

   // enumeração Rank aninhada
   enum Rank: Int {
      case two = 2, three, four, five, six, seven, eight, nine, ten
      case jack, queen, king, ace
      struct Values {
         let first: Int, second: Int?
      }
      var values: Values {
         switch self {
            case .ace:
               return Values(first: 1, second: 11)
            case .jack, .queen, .king:
               return Values(first: 10, second: nil)
            default:
               return Values(first: self.rawValue, second: nil)
         }
      }
   }

   // propriedades e metodos de BlackjackCard 
   let rank: Rank, suit: Suit
   var description: String {
      var output = "naipe é \(suit.rawValue),"
      output += " valor é \(rank.values.first)"
      if let second = rank.values.second {
         output += " ou \(second)"
      }
      return output
   }
}
```






A enumeração `Suit` descreve os quatro naipes comuns em jogos de baralho,
junto a um valor bruto `Character` para representar seu símbolo.
 
A enumeração `Rank` descreve as treze categorias de cartas possíveis em jogos de baralho,
junto a um valor bruto `Int` para representar seu valor nominal.
(Esse valor bruto `Int` não é usado por cartas Valetes, Rainhas, Reis nem Ás)
 
Como mencionado acima, a enumeração `Rank` define
uma estrutura aninhada própria, chamada `Values`.
Essa estrutura encapsula o fato que a maioria das cartas possuem um valor,
mas a carta de Ás possui dois valores.
A estrutura `Values` define duas propriedades para representar isso:
 
- `first`, do tipo `Int`
- `second`, do tipo `Int?`, ou “opcional `Int`”

`Rank` também define uma propriedade computada, `values`,
que retorna uma instância da estrutura `Values`.
Essa propriedade computada considera a categoria da carta
e inicializa uma nova instância `Values` com valores apropriados baseados na sua própria categoria.
Ela usa valores especiais para `jack`, `queen`, `king`, e `ace`. 
Para as cartas numeradas, ela usa o valor bruto `Int` da categoria.

A própria estrutura `BlackjackCard` possui duas propriedades --- `rank` e `suit`.
Ela também define uma propriedade computada chamada `description`,
que usa valores armazenados em `rank` e `suit` para compilar
uma descrição do nome e valor da carta.
A propriedade `description` usa ligação opcional para verificar se existe
um segundo valor a ser exibido, e sendo esse o caso,
insere detalhes descritivos adicionais para o segundo valor.

Por `BlackjackCard` ser uma estrutura sem inicializadores personalizados,
ela possui um inicializador de membro implícito,
como descrito em <doc:Initialization#Memberwise-Initializers-for-Structure-Types>.
Você pode usar esse inicializador para inicializar uma nova constante chamada `theAceOfSpades`: 

```swift
let theAceOfSpades = BlackjackCard(rank: .ace, suit: .spades)
print("theAceOfSpades: \(theAceOfSpades.description)")
// Prints "theAceOfSpades: naipe é ♠, valor é 1 ou 11"
```




Embora `Rank` e `Suit` estejam aninhados em `BlackjackCard`,
seus tipos podem ser inferidos pelo contexto,
e então a inicialização dessa instância é capaz de se referir ao caso de enumeração
apenas pelo seus nomes de caso (`.ace` e `.spades`).
No exemplo acima, a propriedade `description` corretamente reporta que
o Ás de Espada possui o valor de `1` ou `11`.

## Referring to Nested Types

To use a nested type outside of its definition context,
prefix its name with the name of the type it's nested within:

```swift
let heartsSymbol = BlackjackCard.Suit.hearts.rawValue
// heartsSymbol is "♡"
```




For the example above,
this enables the names of `Suit`, `Rank`, and `Values` to be kept deliberately short,
because their names are naturally qualified by the context in which they're defined.



