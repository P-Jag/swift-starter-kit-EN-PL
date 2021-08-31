# Arrays

**EN:**

Arrays let you group items in one collection. You can reach items with using it's position (index) inside array, however you need to know that Swift - like other languages - starts counting form 0, so position of first item is 0 not 1. 

**PL:**

Arrays pozwalają na grupowanie naszych danych. Każdy element można 'wyciągnąć' odwołując się do jego pozycji (index). Należy jedak pamiętać, że Swift podobnie jak inne języki liczy od 0, więc pierwszy element będzie miał index 0, drugi 1 etc... 

```swift 
var animals = ["Dog", "Cat", "Hamster", "Horse", "Owl"]

animals[0] // Dog
animals[2] // Hamster and so on

```

**EN:**

If you want array to hold multiple data types use special keyword ```any```

**PL:**

Jeśli chcesz żeby lista przechowywała inne typy danch użyj ```any```

```swift
var newArray: [Any] = ["New", 4, "Array"]
```

**EN:**

Two most common ways to create empty array

**PL:**

Dwa najpopularniejsze sposoby tworzenia pustej listy

```swift
var food: [String] = []
var drinks = [String]()
```

**EN:**

You can combine two arrays with using ```+``` operator or ```+=```

**PL:**

Można łączyć listy ze sobą za pomocą operatorów ```+``` oraz ```+=```

```swift

var firstArray = ["Peugeot", "BMW"]
var secondArray = ["Mercedes", "Fiat"]

var bothArrays = firstArray + secondArray // output ["Peugeot", "BMW", "Mercedes", "Fiat"]

bothArrays += ["Citroen"] // output ["Peugeot", "BMW", "Mercedes", "Fiat", "Citroen"]

```
