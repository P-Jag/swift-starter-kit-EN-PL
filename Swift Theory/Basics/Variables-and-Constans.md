# Variables and Constants

**EN:** Most important thing is: The value of a constant can’t be changed once it’s set / variable can be set to a different value in the future
**PL:** Najważniejsze jest, żebyś wiedział, że stałej (let) raz zadeklarowanej nie możesz później zmienić. / (var) czyli zmienna może być edytowana w przyszłości


### Variable and Constant Declaration

```swift

// keyword name = value 

var animal =  "Dog"  // variable declaration
animal = "Cat" // changing variable value

let car = "Mercedes" // constant declaration
car = "Kia" // Xcode will throw an error
```

### Multiple variables/constatns

**EN:** You can declare multiple constants/variables in one line - just separate it with , (but all of it have to have same type like string below)
**PL:** Możesz zadelkarować kilka zmiennych/stałych w jednej linii - oddzielając je za pomocą , (muszą być tego samego typu np. string)

```swift 
var name = "Some", lastName = "Dude"
```

### Type annotation

### Summary / Podsumowanie

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
