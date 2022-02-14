# Final

**EN:** 

**Final** keyword has two important functions in Swift - prevents class for subclassing (entirely) and also marks methods as non-overridable which means they cannot be modified. 

**PL:**

**Final** w Swifcie ma dwa kluczowe działania - zabezpiecza daną klasę przed dziedziczeniem (całości) oraz metody oznaczone jako final nie mogą być modyfikowane (non-overridable)

```swift 

// 'locked' class 

final class ExampleClass { /* properties and methods */ }

// 'locked method' - doSomething func cannot be override 

class ExampleClass { final func doSomething(){} } 

```
