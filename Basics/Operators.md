# Operators

* ## Arithmetic Operators
```swift

var a = 10 
var b = 20

var c = a + b
c = a - b
c = a * b
c = a / b

var name = "John"
var lastName = "Doe"

var fullName = name + " " + lastName // return "John Doe"
```

**EN:**

Swift is case sensitive, so if you are comparing strings remember that they have to be written same

**PL:**

Przy porównywaniu stringów (tekstu) muszą być one zapisane jednakowo. Swift zwraca uwagę na wielkość liter przez, co może zwrócić bool false, którego byśmy nie chcieli.

```swift
Case sensitive 

var name = "John Doe"
name == "John Doe" // return true
name == "John DOE" // return false 
```

* ## Remainder Operator %

**EN:**
Reminder operator called Modulo counts how many times a fits in b and return left over (reminder). Example use: check is even or odd. 

**PL:**

Tzw. Modulo oblicza ile razy warość a miejści się w b, po czym zwraca to co pozostało. Przykładowo można łatwo sprawdzić parzystość/nieparzystość liczy etc. 

```swift

11 % 5 // return 1 

Example above return 1 because 5 can fit in 11, two times (5x2 = 10).

```

* ## Unary Minus Operator -

**EN:**

Unary Minus operator change value of variable/constant. It have to be written directly before value (without any whitespaces)

**PL:**

Operator - zmienia wartość zmiennej na przeciwną, jak w przykładzie poniżej. Jak w matematyce - i - daje plus więc podwóje jego użycie przywraca zmienną do pozycji wyjściowej. W zapisie używamy go bezpośrednio przed wartością na której operujemy (bez spacji etc). 

```swift

let five = 5
let minusFive = -five // -5 
let plusFive = -minusFive // 5

```

* ## Unary Plus Operator +

**EN:**

Actually, it's do nothig. You can use it just to have clean an consistent code when you are using Unary Minus Operator

**PL:**

Nie robi nic. Wartość, do której jest przypisany się nie zmienia. Dobrze jest go używać w przypadku kiedy korzystamy z Unary Minus, po to by zachować jednolitość, przejrzystość i czystość kodu. 

```swift

let minusTen = -10
let nothingChangesStillMinusTen = +minusTen

```

* ## Compound Assignment Operators

**EN:**

**PL:**

```swift

```

* ## Comparison Operators

**EN:**

**PL:**

```swift

```

* ## Ternary Conditional Operator

**EN:**

Ternary Conditional Operator is a shorthand of if statement which answers true/false. 

**PL:**

Ternary Conditional Operator to skrócona forma prostego if'a, wykonującego instrukcję na bazie odpowiedzi - true/false. 

```swift

if satetment 

if questionToAsk {
  do this if true
} else {
  do this if false
}

Ternary operator

questionToAsk ? do this if true : do this if false 


Example use 

var height = 150
var hasBottomBar = true
var callingCardHeight = height + (hasBottomBar ? 50 : 10)

hasBottomBar is set for true, so callingCardHeight will be 200 (150 from height variable and 50 from ternary operator)

```

* ## Nil-Coalescing Operator

**EN:**

**PL:**

```swift

```

* ## Range Operators

**EN:**

**PL:**

```swift

```

* ## Logical Operators

**EN:**

**PL:**

```swift

```
