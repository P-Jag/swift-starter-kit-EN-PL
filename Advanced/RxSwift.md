# RxSwift - all in guide

# Observables

**EN:**

Basic concept of **Observables/Sequence** is that every time when we emit event (tap, scorll etc) the value is changing and subscribing to observables let us control it and get the changed value and to something with it.

**PL:**

Najprościej rzecz ujmująć **Observable/Sequence** pozwala nam kontrolować zmiany wywołane przez jakiś event np. kliknięcie czy scrollowanie ekranu. Dzięki ich subskrybcji możemy wyłapać zmianę danej wartości.

### Implementing Observable - most common cases

```swift 

let observable = Observable.just(value) // Observable for JUST one element 

//for collections:

let observable2 = Observable.of(value, value, value) // Observable<Int> for int one by one
let observable3 = Observable.of([1, 67, 176]) // Observable<[Int]> for whole array

let observable4 = Observable.from(["A","B","C","D","E"]) // Observable<Int> function on single elements from array not on array as all
```

**EN:**

When you subscribe observable than you have an access to values which are observing, but you have to remember that subscripe returns an event not direct value. 

**PL:**

Subskrybując observable otrzymujemy dostęp do wartości, które są przez niego obserwowane. Warto jednak pamiętać, że subscribe zrwaca event, a nie wartość samą w sobie.

## Subscribe 

### Implemening Subscription

```swift 

observable4.subscribe = { event in 
  print(event) // in that case our print will be: next(A), next(B)... complete - So those are events with observable value. 
}
```

### How to get values?

```swift
observable4.subscribe = { event in
  if let element = event.element {
    print(element) // print output A, B, C, D, E - our values
  }
}
```

### onNext:

**EN:**

If let unwrapping was so common so RxSwift have their own shorter way to get elements - it's onNext:
**It's a func so take a look that now we have () instead of =**

**PL:**

Rozpakowywanie wartości za pomocą if let jest tak powszechne, że RxSwift swój odpowiednik jakim jest onNext:
**Zwróc uwagę na () zamiast =**

```swift

observable4.subscribe(onNext: { element in 
  print(element) // we are getting our values.
})

```

### Create function - for subscription

```swift

let disposeBag = DisposeBag()

Observable<String>.create = { observer in

  observer.onNext("H") // return H
  observer.onCompleted() // what to do when complete
  observer.onNext("A") // never gets run - its after onCompleted
  
  return Disposables.create() // always call it

}.subscribe(onNext: { }, onError: { }, onCompleted: { }, onDisposed: { }).dispose(by: disposeBag)

```
## Dispose

### Disposing and Terminating

**EN:**

Every single time when we are creating observables and their subscriptions we have to be sure that we dispose it correctly, to prevent us from memory leaks. Once we create subscriber then he will observe values until we say "Hey dude you can get some rest. I get what I want to" by disposing. 

**PL:**

Kiedy stworzymy observable i będziemy go nasłuchiwać - za pomocą subscribe - musiby pamiętać też, żeby go później usunąć. Pozwoli to nam na zabezpieczenie się przed wyciekami. Jeśli nie usnuniemy (dispose) naszego subscribera będzie on stale nasłuchiwał na zmiany - musimy w pewnym momencie powiedzieć "Koleś możesz odpocząć już mam co chciałem"

```swift 

let subscription = observable.subscribe(onNext: { element in
  print(element)
})

subscription.dispose()
```

**EN:**

That's how it's done! However sometimes you can forgot about disposing so better way is to:

**PL:**

Tak to się robi! Jednakże czasem możesz zapomnieć o dispose więc lepiej podejść do tematu w:

```swift

let disposeBag = DisposeBag()

Observable.of(1,2,3)
  .subscribe {
    print($0) // print particular event
  }.disposed(by: disposedBag) 

Now we are sure that our subscriber will be disposed when needs to be

```

# Subjects

**EN:**

Subjects are both observable and observer. What does it mean? Subjects are getting events and then forward result to subscribers. 

**PL:**

Subjects są zarówno obserwatorami jak i obserwującymi. Otrzymują one jakiś określony event po czym przekazują jego rezultat dalej - do subskrybentów. 

## PublishSubject

**EN:**

PublishSubject can be subscribed and also emit events. Important thing is that every event which we want te emit has to be delcarated after setting a subscription. Someone has to recieve this event (example 1)

**PL:**

PublishSubject może emitować eventy oraz być subskrybowany. Należy pamiętać, że każdy event który chcemy wemitować musi być określony po nadaniu subskrybcji - ktoś to musi odebrać. (example 1)

```swift

let pubSubject = PublishSubject<T>() // t - stands for type like String, Int, Bool etc.

pubSubject.onNext(event to emit)

```
Example 1

```swift

let subject = PublisSubject<Int>() // now its empty

subject.onNext(1)

subject.subscribe { event in
  print(event)
}

subject.onNext(3)
subject.onNext(56)

//Print output will be: next(3), next(56). onNext(1) event has no subscribers yet.

subject.dispose() 

subject.onNext(99) // is going to be ingnored. Our subject was disposed 2 lines above. Same in case of onComplete() func.
```

## BehaviorSubject

**EN:**

We can say that is similar to PublishSubject with this difference that BehaviorSubject emit last known value and also have to have an initial value. 

**PL:**

W skrócie jest to to samo co PublishSubject z tą różnica, że BehaviorSubject zwraca ostatnią znaną wartość. Musi również zostać zinicjalizowany z jakąś wartością domyślną (nie może być pusty)

```swift

let subject = BehaviorSubject(value: "Initial") 

subject.onNext("Value 2")

subject.subscribe { event in 
  print(event)
}

subject.onNext("Value 3")

//output 
"Value 2", "Value 3".

```

## ReplaySubject

**EN:**

Replay events based on buffor size we will set. Ex. if we set buffor on 3 than new subscribers will get last 3 values emited by this subject.  

**PL:**

Powtarza eventy w zależności od bufora jaki ustawimy. Jeśli nadamy mu wartość 3 to każdy nowy subskrybent "otrzyma" trzy ostatnie emitowane wartości.

```swift

let subject = ReplaySubject<String>.create(bufferSize: 3)

//emit events
subject.onNext("event 1")
subject.onNext("event 2")
subject.onNext("event 3")
subject.onNext("event 4")

//subscribe

subject.subscribe {
  print($0) // print event
}

//output
"event 2", "event 3", "event 4"
```

## Variables (Deprecated)

**EN:**

Variables wraps up BehaviorSubject and store values in state. To have access to stored data just use .value, however Variables are deprecated, but you might found it in older projects. (Variable -> BehaviorRelay).

It's cool that subscribe on variable fires every time when we made a change (Ex 2 below)

**PL:**

Variables opakowują BehaviorSubject i przechowują wartości, do których dostęp możesz uzyskać korzystająć z .value. Jednakże Variables są już nie używane, to może zdażyć się, że trafisz na nie w starszych projetach. (Zamiast Variable -> BehaviorRelay)

Subskrybcja Variable odpala się za każdym razem kiedy wprowadzimy jakąś zmianę. (Przykład 2 poniżej)

```swift

var variable = Variable("Initial")

variable.value // "Initial"
variable.value = "New Initial"

//how to get this value

variable.asObservable()
  .subscribe {
    print($0)
  }

//output 
next(New Initial)

```
**Example 2**

```swift

var variable  = Variable([String]()) // our variable is an empty array

variable.value.append("Value 1")

variable.asObservable()
  .subscribe {
    print($0)
}

//output1
next(["Value 1"])

variable.value.append("Value 2")

//output2

next(["Value 1", "Value 2"])

```
## BehaviorRelay

**EN:**

BehaviorRelay is a substitute of Variables mentionet above. To have access to it you need to have RxCocoa. 
The difference between BehaviorRelay and Variables is thay you cannot change value with .value. (know it sounds weird)

Example installation of RxCocoa: 

In your directory (project):
a) use open podfile command
b) add: pod 'RxCocoa', '~> version no' 
c) run pod install
d) import RxCocoa

**PL:**

BehaviorRelay jest substytutem Variables omawianych powyżej, żeby móc z niego skorzytsać trzeba mieć zainstalowny RxCocoa gdyż jest jego częścią. 
Różnica między BehaviorRelay i Variables jest taka, że poprzez .value nie można zmienić jego wartości. 

```swift
import RxSwift
import RxCocoa

let relay = BehaviorRelay(value: "Initial") // same like in Variable case

relay.value = "New Initial" // nope - you cannot change the value (read only)

relay.asObservable()
  .subscribe {
    print($0)
}

relay.accept("New Value") // it's new value, not change of old one

//output

next(Initial)
next(New Value) // new one 

```

**What if we have an array?**

```swift

let relay = BehaviorRelay(value: [String]()) // next([]) empty array

relay.value.append("New Value") // err 

relay.asObservable()
  .subscribe {
    print($0)
}

// output
Err - cannot append new value

Use:

relay.accept(["New Value"])

//output 
next(["New Value"])

//IMPORTANT - if our BehaviorRelay stores value it's going to be replaced!

let relay = BehaviorRelay(value: ["Initial"]) // next(["Initial"])

relay.accept(["New Value"]) // next(["New Value"]) instead of desired next(["Initial", "New Value"])

//How to deal with it? 

// a) add current value to accept func

relay.accept(relay.value + ["New Value"]) // array + array = ["Initial", "New Value"]

// b) store current value in variable

var ourArray = relay.value // ["Initial"]
ourArray.append("Something")
ourArray.append("SomethingElse")

relay.accept(ourArray) // accept our changes which we made above

//output
["Initial", "Something", "SomethingElse"]

```

**DON'T FORGET TO ADD RxCocoa to PODFILE! (and also install and import it)**

# Filtering Operators

## Ignore

**EN:** ignoreElements() filter ignore all elements within sequene, however, completed event is still triggered.

**PL:** ingoreElements() ignoruje wszystkie elementy w konkretnej sekwencji. Mimo, to że je pomijamy to wybrany event wciąż jest w toku. 

```swift

let sequenceElement = PublishSubject<String>() // create subject which publish elements of type string
let disposeBag = DisposeBag()

sequenceElement
    .ignoreElements()
    .subscribe { _ in
        print("Subscribe is fired!")
    }.disposed(by: disposeBag)

sequenceElement.onNext("Some") // nothing
sequenceElement.onNext("Values") // nothing
// even if you provide some values print statement will not be executed

sequenceElement.onCompleted() // Subscribe is fired!
// print statement will be executed only when our sequence is completed

```

## Element At

**EN:** elementAt(index) will provide value from selected index from whole sequence

**PL:** elementAt(index) zwraca wskazaną po indexie wartość z naszej sekwencji. 

```swift
let sequenceElement = PublishSubject<String>()
let disposeBag = DisposeBag()


sequenceElement
    .elementAt(1) // we select index no. 1 which is our 2nd 
    .subscribe { _ in
        print("Subscribe is fired!")
    }.disposed(by: disposeBag)

sequenceElement.onNext("First") // nothing happends - index 0
sequenceElement.onNext("Second") // our print statement is fired - index 1 which we selected on .elementAt()
sequenceElement.onNext("Third") // nothing happends - index 2

```

## Filter

**EN:** filter { } is just filtering values in sequence.

**PL:** filter { } po prostu filtruje wartości w sekwencji.

```swift
let disposeBag = DisposeBag()

Observable.of(1,2,3,4,5,6,7)
  .filter { $0 % 2 = 0 } // $0 - means our value
  .subscribe(onNext: {
     print($0) // we are going to print all even numbers from observable - 2,4,6
}).disposed(by: disposeBag)

```

## Skip

**EN:** skip(int) skips selected number of values

**PL:** skip(int) pomija wybraną ilość elementów w sekwencji. 

```swift
let disposeBag = DisposeBag()

Observable.of("Dog", "Cat", "Parrot", "Shark")
  .skip(2)
  .subscribe(onNext: {
     print($0) // we are going to print all elements despite of first 2 - print results are both Parrot and Shark
}).disposed(by: disposeBag)

```

## Skip While

**EN:** skipWhile { } skips elements until given conditon is met. Further elements which do not met given condition are still going to be a part of sequence.

**PL:** skipWhile { } pomija elementy w sekwencji póki nie zostanie spełniony podany warunek, później mimo iż kolejne elementy mogą go nie spełniać to i tak zostaną przekazane - już raz został spełniony.

```swift
let disposeBag = DisposeBag()

Observable.of(2,2,2,3,4,6)
  .skipWhile { $0 % 2 == 0} // skip if result of modulo is 0 
  .subscribe(onNext: {
    print($0) // print output (3,4,6). Skips all 2 until condition is false, then even if 4 and 6 fulfill condition, remains in sequence
}).disposed(by: disposeBag)

```

## Skip Until

**EN:** skipUntil operator is waiting for trigger. It skips all elements in sequence until something triggers it. All elements in sequence which are placed after trigger will go through. 

**PL:** skipUntil pomija wszystkie elementy w sekwencji, czekając na trigger, który pozwoli na przekazanie elementów dalej. Każdy element, który znajduje się w sekwencji po triggerze pójdzie dalej.

```swift
let disposeBag = DisposeBag()

let subject = PublishSubject<Int>()
let trigger = PublishSubject<Int>()

subject.skipUntil(trigger)
  .subscribe(onNext: {
    print($0) // print output will be 4 and 5
  }).disposed(by: disposeBag)

subject.onNext(1) // skipped
subject.onNext(2) // skipped

triggger.onNext(3) // trigger launch subscription

subject.onNext(4) // printed
subject.onNexnt(5) // printed
```

## Take 

**EN:** Take operator takes/pass through selected number of events/elements from sequence - counting from first one

**PL:** Take bierze określiną ilość elementów z sekwencji i przekazuje dale. Licząc od pierwszego elementu, który się w niej pojawi.

```swift
let disposeBag = DisposeBag()

Observable.of("A", "B", "C", "D", "E")
  .take(3) // takes first 3 elements
  .subscribe(onNext: {
    print($0) // print output "A", "B" and "C" our 3 first elements from sequence
}).disposed(by: disposeBag)

```

## Take While

**EN:** takeWhile takes all elements from sequence till they meet given condition. If even one element does not meet the condition, then takwWhile operator stops wokring.

**PL:** takeWhile wyciąga wszystkie elementy, dopóki spełniają one dany warunek. Jeśli natrafi na tak, który go nie spełni, wówczas przestaje się wykonywać.

```swift
let disposeBag = DisposeBag()

Observable.of(2,4,6,8,9,10,12,14)
  .takeWhile { return $0 % 2 == 0} // should return all even numbers?
  .subscribe(onNext: {
    print($0) // print output (2,4,6,8) without 10, 12, 14, because 9 appers and stops execution (in this case $0 % 2 == 1)
}).disposed(by: disposeBag)

```

## Take Until 

**EN:** takeUntil returns all values/elements which appear in sequence before trigger. 

**PL:** takeUntil zwraca wszystkie wartości/elementy z sekwencji, dopóki nie napotka na trigger - on zatrzymuje jego działanie. 

```swift
let disposeBag = DisposeBag()

let subject = PublishSubject<String>()
let trigger = PublishSubject<String>()

subject.takeUntil(trigger)
  .subscribe(onNext: {
    print($0) // print output is A and B
  }).disposed(by: disposeBag)

subject.onNext("A") // printed
subject.onNext("B") // printed

trigger.onNext("T") // fire trigger

subject.onNext("Y") // skipped
subject.onNext("Z") // skipped
```

# Transforming Operators

## To Array 

**EN:** toArray takes all single elements/values from sequence and then append them inside of array [ ] which can be later used for example to display data in tableView.

**PL:** toArray bierze każdy pojedyńczy element/wartość z sekwencji, po czym 'wkłada' je do listy [ ], którą można później wykorzytsać do chociażby wyświetlenia danych w tableView.

```swift
let disposeBag = DisposeBag()

Observable.of(2,4,6,8) // single elements
  .toArray
  .subscribe(onNext: {
    print($0) // print output [2, 4, 6, 8] array of elements
}).disposed(by: disposeBag)

```

## Map 

**EN:** map provides logic to each element in given sequence. It goes throug it and do 'something we want'.

**PL:** map przechodzi przez sekwencję i dodaje logikę, wykonuje działanie na każdym poszczególnym elemencie.

```swift
let disposeBag = DisposeBag()

Observable.of(2,4,6,8) 
  .map { return $0 / 2 } // takes every single element and divide it by 2
  .subscribe(onNext: {
    print($0) // print output 1, 2, 3, 4
}).disposed(by: disposeBag)

```

## Flat Map 

**EN:** flatMap takes observable value and transform it to observable target

**PL:** flatMap zamienia obserwowaną wartość na target. Co to właściwie znaczy?

```swift

struct Weather {
  var temp: BehaviorRelay<Int>
}

let today = Weather(temp: BehaviorRelay(value: 20))
let tomorrow = Weather(temp: BehaviorRelay(value: 25))

let weather = PublishSubject<Weather>

weather.asObservable()
  .flatMap { $0.temp.asObservable } // now our temp value is observable
  .subscribe(onNext: { // every time we trigger event than temp value will be returned
    print($0)
  }).disposed(by: disposeBag)

weather.onNext(today) // return 20
weather.today.accept(22) // return 22

weather.onNext(tomorrow) // return 25
weather.tomorrow.accept(30) // return 30

weather.today.accept(24) // return 24

// The thing is that even if we chance to tomorrow value, previous one were tracked all the time, so our final output for this actions is - 20, 22, 25, 30, 24
```

## Flat Map Latest 

**EN:** flatMapLatest cooperates only with latest observable. If we cange it, then old one will be ignored.

**PL:** flatMapLatest działa tylko z 'ostatim' osbervablem. Jeśli go zmienimy, wówczas przerzuci się na nowy, a ten stary będzie ignorownay. 

```swift

// same example as above 

weather.asObservable()
  .flatMapLatest { $0.temp.asObservable } // now our temp value is observable
  .subscribe(onNext: { // every time we trigger event than temp value will be returned
    print($0)
  }).disposed(by: disposeBag)

weather.onNext(today) // return 20
weather.today.accept(22) // return 22

weather.onNext(tomorrow) // return 25 - Here we change observable 
weather.tomorrow.accept(30) // return 30

weather.today.accept(24) // IGNORE - we chenge our observable from today to tomorrow and all actions taken on today are going to be ignored.

```

# Combining Operators

## Starts With 

**EN:** startsWith operator inserts given value to a first place in sequence.

**PL:** startsWith wstawia wybraną wartość na początek sekwencji. 

```swift

var numbers = Observable.of(6,7,8)
var observable = numbers.startsWith(2)

observable.subscribe(onNext: {
  print($0) // our print is 2,6,7,8 - startsWith insert 2 at the begining fo the sequence
}).disposed(by: disposeBag)

```

## Concat 

**EN:** concat two sequence into one.

**PL:** concat łączy dwie sekwencje w jedną.

```swift

var firstSequence = Observable.of(1,2,3)
var secondSequence = Observable.of(4,5,6)

var thirdSequence = Observable.concat([firstSequence, secondSequence])

thirdSequence.subscribe(onNext: {
  print($0) // print output is 1,2,3,4,5,6 
}).disposed(by: disposeBag)

```

## Merge 

**EN:** merge works similar like concat operator but with this difference that all values in new sequence are goint to be "ordered" by call/time. It means if we have firstSequence with value 1,2,3 and second with 4,5,6 and value 4 will be executed before 2 and 3 new sequence will have mixed order 1,4,2,3,5,6

**PL:** merge działa podobnie jak concat, z tą różnicą że nowa sekwencja będzie utworzona w sposób w jaki dane wartości zostały 'sięgnięte'. Przykładowo:  Pierwsza sekwencja będzie zawierała wartości 1,2 i 3 a druga 4,5,6. Z tą różnicą, że wartość 4 z drugiej sekwencji pojawi się wcześniej, wówczas nowa sekwencja będzie miała zmienoną kolejność na 1,4,2,3,5,6,

```swift


// firstSequence  --1---2---3------->
// secondSequence ----4-------5--6-->

var firstSequence = PublishSubject<Int>()
var secondSequence = PublishSubject<Int>()

var source = Observable.of(firstSequence.asObservable(), secondSequence.asObservable())

var observable = source.merge()

observable.subscribe(onNext: {
  print($0) // print output is 1,4,2,3,5,6 in this scenario we assumed that 4 appears before 2,3 from first sequence
}).disposed(by: disposeBag)

//if you add new elements than all of them will be merged into source. 

firstSequence.onNext(1)
secondSequence.onNext(4) // 4 appears before 2 and 3 from first sequence 
firstSequence.onNext(2)
firstSequence.onNext(3)
secondSequence.onNext(5)
secondSequence.onNext(6)

```

## Combine Latest 

**EN:** combineLatest returns latest values from both sequences which we choose to combine. 

**PL:** combineLatest zwraca ostatnie wartości z obu wybranych sekwencji. 

```swift

let firstSequence = PublishSubject<Int>()
let secondSequence = PublishSubject<Int>()

let observable = Observable.combineLatest(firstSequence, secondSequence, resultSelector: { lastFromFirst, lastFromSecond in 
  "\(lastFromFirst) and \(lastFromSecond)"
}) 

let disposable = observable.subscribe(onNext: { value in
  print(value)
}).disposed(by: disposeBag)

firstSequence.onNext(40) // 40 1
secondSequence.onNext(1) // 40 1
firstSequence.onNext(55) // 55 1
secondSequence.onNext(11) // 55 11
secondSequence.onNext(15) // 55 15

```

## With Latest Form 

**EN:** withLatestForm gives us latest value from sequence. In some way it's waiting until everything is done. To understand it better let's image that we have a button, and textfield and when we taps on button, textfield returns entered value. 

**PL:** withLatestForm zwraca nam ostatnią wartość z sekwencji. W pewnym sensie czeka, aż będzie ona kompletna. Żeby lepiej sobie to zobrazować, przyjmijmy, że mamy button, po którego naciśnięciu textfield zwraca wpisany w niego tekst. 

```swift

let button = PublishSubject<Void>()
let textField = PublishSubject<String>()

let observable = button.withLatestForm(textField) // so we connect button with textField

let disposable = observable.subscribe(onNext: {
  print($0)
})

textField.onNext("Lea") // wait
textField.onNext("Learn Rx") // wait
textField.onNext("Learn RxSwift") // done

button.onNext(()) // return "Learn RxSwift"
button.onNext(()) // return "Learn RxSwift"
```

## Reduce 

**EN:** reduce takes all elements from sequence and return them as one.

**PL:** reduce bierze wszystkie elementy z sekwencji i łączy je w jedną. 

```swift

// Example 1

let source = Observable.of(1,2,3)

source.reduce(0, accumulator: +) // 0 is a seed so our starting point, accumulator says that we want to add all elements
  .subscribe(onNext: {
    print($0) // our return is 6 which is a result of 1 + 2 + 3
}).disposed(by: disposeBag)

// Example 2

source.reduce(0, accumulator: { summary, newValue in
    return summary + newValue  
}).subscribe(onNext: {
    print($0) // our return is 6 which is a result of 1 + 2 + 3
}).disposed(by: disposeBag)

```

## Scan 

**EN:** scan works similar to reduce but with small difference, that it's adding each element one by one and return value immediately.

**PL:** scan działa podobnie jak reduce, ale z małą różnicą. Mianowicie taką, że wykonuje działanie na każdym elemencie jeden po drugim i zwraca ich nową wartość.

```swift

let source = Observable.of(1,2,3,5,6)

source.scan(0, accumulator: +)
  .subscribe(onNext: {
    print($0)
}).disposed(by: disposeBag)

// Result = result + value from source
// 1 = 0 + 1 // 0 is a seed value
// 3 = 1 + 2
// 6 = 3 + 3 
// 11 = 6 + 5 (last result was 6 and then another value in sequence is 5 - we dont have 4 in it)
// 17 = 11 + 6
```

# RxCocoa

**EN:** RxCocoa is a framework which provides custom wrappers for UI controls and some SDK classes to easier maintain reactive behaviour in our app. If RxCocoa do not contain desired wrapper we can easily create it. 

**PL:** RxCocoa zawiera wrappery dla kontrolek UI oraz niektórych klas w SDK. Dzięki nim łatwej jest dodać i utzymać reaktywność aplikacji. Jeśli w bibliorece RxCocoa nie znajdziemy pożądanego wrappera możemy je stworzyć sami. 

## Binding

**EN:** Producer provides data to Reciever (interface) but Reciever cannot have bind connection with producer like in other languages.

**PL:** Producer przez binding dostarcza dane do inferfejsu (Reciever). Jednakże interfejs nie ma połączenia z Producerem. Jest to połączenie jednostronne. 

```
Producer --- bindTo ---> Reciever 

Producer <--- xxx --- Reciever // do not exist - one way connection.
```
## Driver

**EN:** Main features of driver is: Driver works on units which can't error out, units are observed on main scheduler so I don't have to type .observeOn(MainScheduler.instance). Just use driver instead. You can also share side effects - bind or put into interface. 

**PL:** Główne zalety używania drivera to: Pracuje na jednostkach, które z automatu są obserwowane i subskrybowane na MainSchedulerze, więc nie trzeba nic dodawać (.observeOn(MainScheduler.instance). Można używać go zarówno do bindingu oraz dodawać do interfejsu. 

```swift 
 let weather = URLRequest.load(resource: resource)
            .observe(on: MainScheduler.instance)
            .asDriver(onErrorJustReturn: WeatherResult.empty)
        
        // Observable binding with driver 
        weather.map { "\($0.main.temp)" }
        .drive(self.temperatureLabel.rx.text) // .bind(to: self.temperatureLabel.rx.text)
        .disposed(by: disposeBag)
        
        weather.map { "\($0.main.humidity)" }
        .drive(self.humidityLabel.rx.text) // .bind(to: sefl.humidityLabel.rx.text)
        .disposed(by: disposeBag)
```

## Disposing with RxCocoa

**EN:** When to use weak, unknown or nothing?

nothing: in singleton vc when it's not going to be released. 

unknown (self cannot be nil): inside all vc which are going to be released after closure task is complete

weak (self can be nil): all other cases

**PL:** Kiedy użyć weak, unknown albo żadnego z nich?

nothing: w singletonach, które nigdy nie zostaną 'zamknięte'.

unknow (self nie może być nilem): kiedy 'zamknięcie' danego vc jest efektem działania domknięcia (closure)

weak (self może być nilem): wszystkie inne przypadki

# Error Handling

Observable ----> Error / Retry ----> Subscription

## Throwing Errors

Basic generic load func with error throw

```swift
 static func load<T: Decodable>(resource: Resource<T>) -> Observable<T> {
        
        return Observable.just(resource.url)
            .flatMap { url -> Observable<(response: HTTPURLResponse, data: Data)> in
                
                let request = URLRequest(url: url)
                return URLSession.shared.rx.response(request: request)
            
            }.map { response, data -> T in
                
                if 200..<300 ~= response.statusCode {
                    return try JSONDecoder().decode(T.self, from: data)
                } else {
                    throw RxCocoaURLError.httpRequestFailed(response: response, data: data)
                }
                
            }.asObservable()
    }
```

## Catch Error

Basic error catch

```swift

 let weather = URLRequest.load(resource: resource)
            .observe(on: MainScheduler.instance)
            .catch { error in
                print(error.localizedDescription)
                return Observable.just(WeatherResult.empty)
            }
            .asDriver(onErrorJustReturn: WeatherResult.empty)

```

## Retry 

```swift

 let weather = URLRequest.load(resource: resource)
            .observe(on: MainScheduler.instance)
            .retry(3) // just add retry and num of times  - retry 3 times in other case throw error. 
            .catch { error in
                print(error.localizedDescription)
                return Observable.just(WeatherResult.empty)
            }
            .asDriver(onErrorJustReturn: WeatherResult.empty)

```
