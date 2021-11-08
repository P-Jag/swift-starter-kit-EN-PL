# didSet { }

**EN:**

didSet invoke block of code when property is assingned to. Commonly used in reactive programming. Helps us to react for changes on selected value. 
To clarify let's check it on two examples below.

**PL:**

didSet uruchamia blok kodu kiedy przypiszemy do niego jakąś wartość - ulega zmianie. Stosowany jest w programowaniu rekatywnym, jak sama nazwa podpowiada pomaga nam na bieżąco reagować na daną zmianę wartości. 

Dla łatwiejszego zrozumienia didSet przyjrzyj się poniższym przykładom. 

1. Easy example

```swift 

example code

```

2. Little bit more complicated one

```swift

```

**EN:**

There's also a willSet block which is invoked **before** value will change - but it's not in use very often. 

**PL:**

Warto wspomnieć, że drugim blokiem tego typu jest willSet, który uruchamia się **przed tym** jak nasza wartość zostanie zmieniona.

```swift

private let someNumber = "1" {
  willSet {
    code to execute 
  }
}
```
