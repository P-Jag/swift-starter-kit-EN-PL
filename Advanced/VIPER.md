# VIPER

![viper](https://user-images.githubusercontent.com/58946631/137489198-cc408695-fded-4c3f-9275-223e35174dbf.png)

**EN:**

VIPER architectire pattern is composed of 5 elements (View, Interactor, Presenter, Entity and Router). Each of element have a special separated taks to do, what helps us to easiier manage our app structure, separate business logic and views. 

**PL:**

VIPER (architektura) składa się z 5 elementów (View, Interactor, Presenter, Entitny, Router). Każdy z elementów odpowiada z inną funkcję w naszej aplikacji. Dzięki temu łatwiej nam zarządzać strukturą i oddzielić logikę biznesową od widoków. 


## V - View

**EN:**

First element is a View. It might be a little bit confusing because our view contains a viewControllers either. In just few lines we can describe it as:
- view and viewController owner
- conform to specific protocol
- reference to presenter

**PL:**

Pierwszym elementem VIPERa jest View. Nazewnictwo może być w tym wypadku lekko mylące, gdyż View przechowuje też viewControllery, które chociażby w MVVM są osobną od View warstwą. 
- view i ViewControllery
- musi stosować się do specyficznego protokołu
- ma referencję do Presentera / odbiera dane

## I - Interactor

**EN:**

Interactor is a kind of a brain (or at least cerebral hemisphere) of our app. Here we have all of our magic happends. Interactor is processing data and then sends it to Presenter. 
- ojcect
- conform to specific protocol
- reference to presenter (only) / sending processed data 

(here we have or API requests for ex.)

**PL:**

Interaktor jest swego rodzaju mózgiem naszej aplikacji. Tutaj procesujemy całą logikę biznesową. Przerobione dane są później przesyłane przez Interactor do Presentera. 
- jest obiektem
- musi stosować się do specyficznego protokołu
- ma referencje do Presentera (tylkoe) / Przesyła przeprocesowane dane 

## P - Presenter

**EN:**

In simplest way - Presenter decides which kind of data (from Interactor) should be displayed or not. Then pass this data to View layer. 
- also a object
- confrom to specific protocol
- reference to view, interactor and router

**PL:**

Najprościej - Presenter decyduje, jakie dane (otrzymane z interactora) wyświetlić, a które nie. Jeśli mają zostać wyświetlone, wówczas przesyłane są do View. 
- jest obiektem
- musi stosować się do specyficznego protokołu
- ma referencje do Interactora, Routera i View

## E - Entitny

**EN:**

Entity is just a model - no more, no less

**PL:**

Entity to po prostu nasz model danych.

## R - Router

**EN:**

Router is our entry point for modules (module is for ex. a single tab)
- obcject
- entry point

**PL:**

Router jest naszym punktem wejściowym dla modułów (modułem może być np. pojedyńczy tab).
- jest obiektem
- punkt wejściowy dla modułów

### Useful links
* [VIPER in iOS App](https://medium.com/cr8resume/viper-architecture-for-ios-project-with-simple-demo-example-7a07321dbd29)
* [VIPER explanation](https://www.youtube.com/watch?v=hFLdbWEE3_Y)
