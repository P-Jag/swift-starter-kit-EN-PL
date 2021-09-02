# Typealias

**EN:**

In simple terms using typealias is just giving a nickname to part of your code (you can give a name to a closure or combinie protocols - check ```Codable``` which is a typealias for ```Encodable & Decodable``` protocols). You can also rename types to have your code little bit cleaner - readable. 

**PL:**

Najprościej rzecz ujmując używając typealias nadajemy konkretną nazwę jakiejś części kodu (np. domknięciu), możemy też łączyć w nim protokały tak, aby użyć samej nazwy zadeklarowanej jako typealias, a nie kilku protokołów. Za przykład może posłużyć ```Codable``` którego używasz przy tworzeniu modelu. Codable to nic innego jak typealias dla dwóch protokołów ```Endcodable i Decodable```. Możesz również nadawać nazwy typom w taki sposób, żeby łatwiej było Ci odnaleźć się w kodzie. 

```swift 

typealias FancyAliasName = your code here

combining protocols

typealias MainViewProtocols = FirstProtocol & SecondPrococol

```

Renaming types/Nadawanie nazwy typom

**EN:**

If you have function which can be called anywhere (let's take this one written below) you can be confused which type of message you have to use. The solution is simple - use typealias to change what kind of type you expect. 

**PL:**

Kiedy masz funkcję, którą możesz wywołać w każdym miejscu w kodzie może dojść do sytuacji, w której nie będziesz wiedział, co przesłać dalej / jaki tekst podać? W tym przypadku na ratunek przychodzi typealias. Po prostu zmień nazwę typu tak, żeby lepiej opisywał czego w tym wypadku oczekujesz.

```swift
before

func showSomeAlert(with messsage: String, in view: UIView) {
  some code here // not important right now
}

after 

typealias EmptyListMessage = String

func showSomeAlert(with message: EmptyListMessage, in view: UIView) {
  some code here // not important rught now
}

```


