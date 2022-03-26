# Dependency Injection

### Classic Approach

**EN:**

Dependency Injection allows us to define contracts (eg. protocols) which can be used by any class conforms/inherits this contract. 

**PL:**

Dependency Injection pozwala nam zdefiniować i wykorzystać kontrakt (np. protokół), z którego będzie mogła skorzystać każda klasa zgodna z deklarowanym protokołem lub dziedzicząca.


#### Basic example / prosty przykład

```swift 

// 1. Set protocol which is our contract 

protocol SwimmingStyles {
    func frontCrawl()
    func breaststroke()
    func butterfly()
}


// 2. Tournament 1 and 2 are classes which conforms to SwimmingStyles protocol. 
class Tournament1: SwimmingStyles {
    func frontCrawl(){}
    func breaststroke(){}
    func butterfly(){}
}

class Tournament2: SwimmingStyles {
    func frontCrawl(){}
    func breaststroke(){}
    func butterfly(){}
}


// 3. Now we can inject this protocol via. init and we can use all methods and values from protocol in each single case we create on its base
class SelectedTournament {
    
    let tournament: SwimmingStyles
    
    init(tournament: SwimmingStyles) {
        self.tournament = tournament
    }
}

var selectedTournament1 = SelectedTournament(tournament: Tournament1())
var selectedTournament2 = SelectedTournament(tournament: Tournament2())

``` 

#### 'Real life' example / Przykład użycia

```swift
import UIKit

class ViewController: UIViewController, UITableViewDelegate, UITableViewDataSource {
    
    @IBOutlet var tableView: UITableView!
    var data = [DogBreed]()

    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.delegate = self
        tableView.dataSource = self
        data = breeds()
    }
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return data.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        let breed = data[indexPath.row]
        cell.textLabel?.text = "\(breed.breedName) - \(breed.countryOfOrigin)"
        return cell
    }

    // 3. Here we are returning array of breeds
    func breeds() -> [DogBreed] {
        return [BorderCollie(), GermanShepherd(), CaneCorso()]
    }
}

// 1. Our contract which create dog breed
protocol DogBreed {
    var breedName: String { get }
    var countryOfOrigin: String { get }
}

// 2. Classes below are build on base of DogBreed contract 
class BorderCollie: DogBreed {
    var breedName: String {
        "Border Collie"
    }
    var countryOfOrigin: String {
        "Scotland"
    }
}

class GermanShepherd: DogBreed {
    var breedName: String {
        "German Shepherd"
    }
    var countryOfOrigin: String {
        "Germany"
    }
}

class CaneCorso: DogBreed {
    var breedName: String {
        "Cane Corso"
    }
    var countryOfOrigin: String {
        "Italy"
    }
}

```

### Swinject 

**EN:**

**PL:**

#### Adding Swinject via pods

In terminal type: 

```
pod init // initializa cocoapods - you might have not installed 

open Podfile // Open Podfile and add Swinject - pod 'Swinject', save file and close.

pod install // to install dependencies in this case Swinject package
```
