# Variables and Constants

```swift
var animal =  "Dog"  // variable declaration
animal = "Cat" // changing variable value

let car = "Mercedes" // constant declaration
car = "Kia" // Xcode will throw an error
```

**EN:**
As you probably know variables can vary which means we can change it's values during the coding process.
Constants (let in Swift) is a value which cannot be changed. If you tried to do it xcode will refuse to build our app.

Why we shoud separate var/let? 
- prevent from making mistakes 
- constant values makes our code run faster

**PL:**
Powyżej widzisz jak w Swifcie deklaruje się zmienne (var) oraz stałe (let). 
Jak zapewne już wiesz w prównaniu do **let**, **var** może ulec zmianie - możemy przypisać inną wartość. Jak w przykładzie powyżej.

Warto pamiętać, aby w miarę możliwości korzystać z obu deklaracji, dlatego że:
- uchroni nas to przed niepożądanymi błędami
- tworzenie stałych **let** pozwala naszemu kodowi działać szybciej (niż operując na samych **var**)
