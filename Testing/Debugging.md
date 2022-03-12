# Debugging

## Print statements

**EN:** As the name suggests print statements helps us to print desired value in debug console. In Swift there's two types of prints: print() and debugPrint()

**PL:** Jak sama nazwa wskazuje print pozwala nam 'wydrukować' porządaną wartość w debugerze. W Swifcie rozróżniamy dwa rodzaje printów: print() i debugPrint()

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
