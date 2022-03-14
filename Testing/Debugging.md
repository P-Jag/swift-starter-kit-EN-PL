# Debugging

## Print statements

**EN:** As the name suggests print statements helps us to print desired value in debug console. In Swift there's two types of prints: **print() and debugPrint()**

**PL:** Jak sama nazwa wskazuje print pozwala nam 'wydrukować' porządaną wartość w debugerze. W Swifcie rozróżniamy dwa rodzaje printów: **print() i debugPrint()**

```swift 

print()

debugPrint() 

// In case of NSObjects

class Dummy: NSObject {
     
    // that's the place we're getting print()
    override var description: String {
        return "Bar Description"
    }
    
    // that's the place we're getting debugPrint()
    override var debugDescription: String {
        return "Bar Debug Description"
    }
}

// EN: In case of regular swift class we can use both prints without any addons, however, both prints comes from protocols: CustomStringConvertible (print) and CustomDebugStringConvertible

// PL: W przypadku 'czystych' klas swiftowych możemy użyć obu printów niezależnie od rozszerzeń bądź dodatków do klasy. Jeśli jednak chcemy edytować ich właściwości musimy dostosować naszą klasę do odpowiednich protokołów: CustomStringConvertible (print) and CustomDebugStringConvertible

class SwiftDummy: CustomStringConvertible, CustomDebugStringConvertible {
  let weekDay = "Monday"
  let day = 12
}

// EN: Protocols mentioned above helps us to customize our print statements to get more info than just a string. 
// PL: Wyżej wymienione protokoły pozwalają nam na modyfikację printów w ten sposób, żebyśmy otrzynali więcej informacji niż tylko zwykły string. 

extension CustomDebugStringConvertible {
    var debugDescription: String {
        let className = type(of: self)
        let address = "\(Unmanaged.passUnretained(self as AnyObject).toOpaque())"
        var description = "<\(className): \(address), {"
        
        let mirror = Mirror(reflecting: self)
        description += mirror.children.compactMap {
            let (label, value) = $0
            guard let propertyName = label else { return nil }
            return "\(propertyName): \(value)"
        }.joined(separator: ", ")
        
        description += "}>"
        
        return description
    }
}

//EN: Extension above let us print class name, addres and also all properties stored inside
//PL: Zaprezentowane wyżej rozszerzenie protokołu, pozwala nam na wydrukowanie w konsoli informacje jak: nazwa klasy, jej adres oraz wartości, które przechowuje. 

```

## Breakpoints

**EN:** Breakpoint it's just a way to stop executing program which let you inspect values, state and also change it. 

If you double-click on breakpoint you can set specific conditions, ingore some executions and also configure how debug should inform you that was reached. 

**PL:** Breakpointy zatrzymują wykonywanie programu, dzięki czemu z łatwością możesz sprawdzić i zmienić wartości czy dokonać inspekcji stanu w jakim jest Twoja aplikacja.

Jeśli klikniesz dwa razy w breakpoint będziesz mógł go dowolnie skonfingurować m.in: nadając mu warunki do spełnienia, wymuszając pominiecie wybranej liczby wywołań czy skonfigurować sposób powiadomienia, że wybrany breakpoint jest aktywny.

<img width="549" alt="Screenshot 2022-03-12 at 14 49 58" src="https://user-images.githubusercontent.com/58946631/158020661-5ee1e826-015a-4cdb-be21-a7d22f81d9db.png">

**EN:** When your program hits the breakpoint then your able to use commands in debugger window  **(lldb)**. 

**PL:** Kiedy wybrany breakpoint zatrzyma działanie programu, wówczas w oknie debuggera **(lldb)** będziesz mógł korzystać z komend jak:

```swift 

// Our dummy class for test puprose 
 
class Person {
     var name: String
     var age: Int

     init(name: String, age: Int) {
          self.name = name
          self.age = age
     }
}

var person1 = Person(name: "Mike", age: 27)

```

Some basics lldb commands: 

* **help** - turn on menu with available commands // **help po** - shows description how **po** command works

* **po** - print out description of the object // **po person1** (if preson1 object exists ofc)

* **e** - expression allow us to change the value // **e person1.name = "Adam"** - we change name from Mike to Adam

* **c** - continume execution


## Symbolic Breakpoints

**EN:**

**PL:**

## View Debugger

**EN:**

**PL:**

## Memory Grpah

**EN:**

**PL:**

## Thread Sanitizer

**EN:**

**PL:**

## Address Sanitizer

**EN:**

**PL:**

## Reverse Engineering Basics

**EN:**

**PL:**

## Instruments Time Profiler

**EN:**

**PL:**

## Bonus: Memory leaks - how to find and fix

**EN:** To diagnose memory leak you can use Instruments which is a part of Xcode. Instruments provides multiple templates for drilling down not only memory leaks. You can use it to check threads, network and more. 

**PL:** Do zdiagonozowania wycieku danych możemy użyć Instruments, które masz zainstalowane razem z Xcodem. Instruments zawiera templatki do badania/grzebania w projekcie nie tylko pod względem wycieków. Świetnia sprawdza się również w przypadku weryfikacji poprawnego działania wątków czy networkingu. 

<img width="793" alt="Screenshot 2022-03-14 at 19 57 16" src="https://user-images.githubusercontent.com/58946631/158241910-2c98656d-2c4c-4719-8d33-1aba9ba23164.png">

**EN:** The second thing which can help you to find memory leaks is Debug Memory Graph - which can be turned on by clicking button below. 

**PL:** Drugim narzędziem pozwalającym na łatwiejszą lokalizację przecieków jest Debug Memory Graph - który włączamy za pomocą przycisku poniżej. 

<img width="379" alt="Screenshot 2022-03-14 at 20 03 05" src="https://user-images.githubusercontent.com/58946631/158243565-490a52f9-1d7c-478d-8c4c-5a7296e45a80.png">

**EN:** Debug Memory Graph is presenting structure (graph) of conections between objects.

**PL:** Debug Memory Graph przedstawia diagram połączeń pomiędzy obiektami.



