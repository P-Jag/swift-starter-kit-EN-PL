# RxSwift

## Observables

**EN:**

Basic concept of **Observables/Sequence** is that every time when we emit event (tap, scorll etc) the value is changing and subscribing to observables let us control it and get the changed value and to something with it.

**PL:**

Najprościej rzecz ujmująć **Observable/Sequence** pozwala nam kontrolować zmiany wywołane przez jakiś event np. kliknięcie czy scrollowanie ekranu. Dzięki ich subskrybcji możemy wyłapać zmianę danej wartości.

**Implementing Observable - most common cases**

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

### Subscribe 

**Implemening Subscription**

```swift 

observable4.subscribe = { event in 
  print(event) // in that case our print will be: next(A), next(B)... complete - So those are events with observable value. 
}
```

**How to get values?**

```swift
observable4.subscribe = { event in
  if let element = event.element {
    print(element) // print output A, B, C, D, E - our values
  }
}
```

**onNext:**

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

**Create function - for subscription** 

```swift

let disposeBag = DisposeBag()

Observable<String>.create = { observer in

  observer.onNext("H") // return H
  observer.onCompleted() // what to do when complete
  observer.onNext("A") // never gets run - its after onCompleted
  
  return Disposables.create() // always call it

}.subscribe(onNext: { }, onError: { }, onCompleted: { }, onDisposed: { }).dispose(by: disposeBag)

```
### Dispose

**Disposing and Terminating**

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

## Subjects

**EN:**

Subjects are both observable and observer. What does it mean? Subjects are getting events and then forward result to subscribers. 

**PL:**

Subjects są zarówno obserwatorami jak i obserwującymi. Otrzymują one jakiś określony event po czym przekazują jego rezultat dalej - do subskrybentów. 

**Publish Subject**

```swift
```

**Behavior Subject**

```swift
```

**Replay Subject**

```swift
```

**Variables** (Deprecated)

```swift
```

**BehaviorRelay**

```swift
```

## Filtering Operators

## Transforming Operators

## Combining Operators

## RxCocoa

## Error Handling

## MVVM in RxSwift
