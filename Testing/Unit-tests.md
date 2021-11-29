# Unit Tests

**EN:** Testing a unit (single part) of code to prevents from having bugs the future while new developers makes changes in code.

**PL:** Służą do testowania pojedyńczej części kodu (test jednostokowy). Pisze się je, żeby ustrzec się przed błędami, bugami zarówno podczas pisania kodu jak i wprowadzaniu zmian w przyszłości. Nowym developerom łatwiej jest utrzymać napisany i znaleźć błędy w napisanym już kodzie. 


Easy Example - simple math calculations 

1. MathCalc class: 

```swift
class MathCalc {
    
    func addNumbers(x: Int, y: Int) -> Int {
        return x + y
    }
    
    func subtractNumbers(x: Int, y: Int) -> Int {
        return x - y
    }
    
    func multiplyNumbers(x: Int, y: Int) -> Int {
        return x * y
    }
    
    func divideNumbers(x: Int, y: Int) -> Int {
        return x + y
    }
}
```

2. **EN:** We are goint go test functions from MathCalc (listed above).

   **PL:** Dla przykładu przetestujemy sobie proste funkcje z klasy MathCalc

```swift 

import XCTest
// import Nimble - external library
@testable import SimpleAppForTest // our app name 

class SimpleAppForTests: XCTestCase {


    // test addNumbers func from MathCalc class

    func testAddNumbers(){
        let calculations = MathCalc()
        let result = calculations.addNumbers(x: 1, y: 2)
        
        XCTAssertEqual(result, 3) // result has to be equal 3 in other case test will fail
    } 
}

```

More common XCTests:

```swift

XCAssertFalse() // check bool
XCAssertTrue() // check bool
XCAssertNotNil() // result cannot be nil
XCAssertNil() // result have to be nil

```

**EN:** You can also use an external libraries like Nimble to make it even easier to do :)

**PL:** Możesz skorzystać również z bibliotek takich jak Nible, które jeszcze bardziej ułatwiają testowanie :)
