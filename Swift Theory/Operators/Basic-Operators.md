# Basic Operators

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

* ## Compound Assignment Operator +=

**EN:**

Simply - take current value and add something to it. It's a shortcut for a = a + b

**PL:**

Najprościej rzecz ujmując, bierze obecną zmienną (jej wartość) i dodaje do niej kolejną. Jest to skrót dla działań takich jak a = a + b

```swift

a = a + b // 'normal' way
a += b // Compound Assignment Operator

var a = 10
a += 15 // a = 10 + 15

```

* ## Comparison Operators

**EN:**

Basisc comparsion operators which checks is if our values are equal, not equal, less, greater, less then or equal, geater then or equal. Comparsion operators are often use in conditinal statements like **if**. 

**PL:**

Podstawowe operatory, których zadaniem jest porównanie wybranych wartości. Czy dwie waerości są równe, nierówne sobie, czy jedna jest mniejsz, większa, mniejsza lub równa, większa lub równa. Używa się ich zazwyczaj w instrukcjach warunkowych takich jak if. 

```swift

4 == 4  // true because 4 is equal to 4 // prawda bo 4 jest równe 4
3 != 1   // true because 3 isn't equal to 1 // prawda bo 3 nie jest równe 1
2 > 1    // true because 5 is greater than 2 // prawda bo 5 jest większe niż 2
1 < 10   // true because 1 is less than 2 // prawda bo 1 jest mniejsze od 10
1 >= 1   // true because 1 is greater than or equal to 1 // prawda bo 1 jest równe 1
17 <= 5   // false because 17 isn't less than or equal to 1 // fałsz bo 17 nie jest mniejsze od 5

```

```swift
Comparsion operators in if statement:

var age = 19 

if age >= 18 { // in US version 21 ;)
  print("Let's have a drink")
} else {
  print("You are too young to drink")
}

// Prints "Let's have a drink" because our age (19) is greater than required 18
```

* ## Ternary Conditional Operator ? :

**EN:**

Ternary Conditional Operator is a shorthand of if statement which answers true/false. 
Important: Avoid to use nested ternary operators 

**PL:**

Ternary Conditional Operator to skrócona forma prostego if'a, wykonującego instrukcję na bazie odpowiedzi - true/false. 
Ważne: Staraj się unikać zagnieżdżania TCO jeden w drugim itp. 

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

* ## Nil-Coalescing Operator ??

**EN:**

Nil-Coalescing Operator unwraps optional variable (ex. someValue, with ? mark) and return default one while someValue is **nil**

**PL:**

Nil-Coalescing Operator 'rozpakowuje' zmienną zadeklarowaną jako opcjonalna (przed dodanie ?) i zrwaca domyślną wartość kiedy nasz 'opcjonalna' zawiera **nil**

```swift

var defaultColor = "white"
var userSelectedColor: String? // now this variable is equal nil because we do not choose color

var selectedColorToUse = userSelectedColor ?? defaultColor // output will be "white"

if user pick color and our variable is not empty, nil-coalesing operator will return it like in example below:

userSelectedColor = "black"
var selectedColorToUse = userSelectedColor ?? defaultColor // output will be "black"

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
