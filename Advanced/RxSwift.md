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

**EN:**

**PL:**

```swift

```

## Element at

**EN:**

**PL:**

```swift

```

## Filter

**EN:**

**PL:**

```swift

```

## Skip

**EN:**

**PL:**

```swift

```

## Skip while

**EN:**

**PL:**

```swift

```

## Skip until

**EN:**

**PL:**

```swift

```

## Take 

**EN:**

**PL:**

```swift

```

## Take while

**EN:**

**PL:**

```swift

```

## Take until 

**EN:**

**PL:**

```swift

```

# Transforming Operators

# Combining Operators

# RxCocoa

# Error Handling

# MVVM in RxSwift
