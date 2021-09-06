# Lazy


**EN:**

Lazy keyword in simplification means "right in time", so yo'll get your variable when needed. 

To make it easier to understand let's have a look on examples below (a and b)

a) While instantiate the object and one variable not know anything about others but we want to use it. We mark clubIntroduction as lazy because we don't want to call it before we do not get any required data (club and stadium)

b) When something requires time - like big loops. It's better to not run it when they're not necesscary. 

**PL:**

Lazy oznacza w skrócie - na czas. Dla rozjaśnienia, wykorzystujemy Lazy w przypadku kiedy chcemy dostać coś w konkretnym momencie. Może brzmi to zawile, ale jest dość łatwe do zrozumienia. Z pewnością dwa przykłady poniżej pomogą Ci zrozumieć o co chodzi. 

a) Kiedy zmienne nie wiedzą nic o sobie, a chcemy ich użyć. Oznaczmy clubIntroduction jako Lazy, gdyż póki nie będziemy mieli nazwy klubu oraz stadionu nie chcemy nic wywoływać. 

b) Kiedy jakiś proces zajmuje dużo czasu to nie chcemy go uruchamiać w tle tylko w momencie kiedy go potrzebujemy. 


Example A

```swift
struct MadridTeam {

  var club: String
  var stadium: String

  lazy var clubIntroduction = {
    return "One of most famous clubs in Madrid is \(club) which is playing on \(stadium)"
  }()

}

var atleti = MadridTeam(club: "Atletico", stadium: "Wanda Metropolitano")

print(atleti.clubIntroduction) // One of most famous clubs in Madrid is Atletico which is playing on Wanda Metropolitano
```

Example B

```swift

struct Calculator {

  static func calculateGames() -> Int {
    var games: [Int] = []
    for i in 1...3_000 { games.append(i) } // we have 3000 games and iteration will take some time
    return games.last!
  }
  
}

struct MadridTeam {

  var club: String
  var stadium: String
  lazy var gamesInLaLiga = Calculator.calculateGames() // if we do not have lazy keyword, every time when we create new team Calulator will run and count games

  lazy var clubIntroduction = {
    return "One of most famous clubs in Madrid is \(club) which is playing on \(stadium)"
  }()

}

```
