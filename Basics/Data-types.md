## Data types

```swift
// int 
let number = 4 
// double 
let doubleNumber = 4.5
// float
let floatNumber = 4.5
// string
let someText = "Text"
// bool
var isTrue = false
```
**EN:**

Swift know what kind of type you use while the value is assigned like: var isTrue = false // now Swift knows is Bool

*Float and double data type looks same, but then are not! Surprise. Apple reccomends to use double type beacuse is more accurate.
(Float has less space for storing numbers - try it out in Swift Playground - compare double and float with value of 123456,7890987)

Remember also that Swift always want to know what type of data are you using, so use annotation like below (by adding : and type):

**PL:**

Swift wie jakiego typu danych używasz kiedy przypiszesz go do zmiennej jak w przypadku: var isTrue = false // Swift już wie, że używasz Bool'a

*Może Ci się wydawać, że Float i Double to to samo. Nie do końca. Musisz pamiętać, że Float ma mniej miejsca na przechowywanie liczb i ucina je tak, aby dać jak najbliższy prawdzie wynki.

Dla sprawdzenia: W Swift Playgorund stwórz zmienne z typem Double oraz Float i przypisz do nich dużą liczbę np: 1234567,890987

Pamiętaj również, że Swift zawsze chce wiedzieć jakiego typu danych chcesz użyć. Jeśli wiesz, co zostanie przypisane do danej zmiennej możesz użyć adnotacji typu poprzez dodanie do nazwy : oraz typu jak w przykładach poniżej:

```swift
var number: Int
number = 4

var number: Float
number = 4.5

etc. 
```
