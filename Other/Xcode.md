# Xcode tips and tricks

## Regexp search

```Find Navigator -> Text -> Regular Expressions```

You can use it to search places where Dictionary keys are accessed using strings 


```swift
if let .*\[
```

* ## Faster testing 

Use ```⌃ ⌥ ⌘ G``` to run last test or **⌘ + click** to select test you want to re-run. 

## Doubling text for UI test

a) ```Asisstant editor -> Change Automatic to Preview```

b) Change language (right-bottom corner) to double-lenght pesudolanguage

* ## Open xcode

Use ```xed .``` command in terminal (inside project folder) to run workspace.

* ## Generated interface

When you are in struct or class just press ```⌃ ⌘ ↑``` to see it's external properties and methods

* ## Clean up some space

Run command below to delete old, not supported simulators to save space on your Mac

``` xcrun simctl delete unavailable ```

* ## Identifying contrains

To identify constrains give them specific name - identifier, for easier debugging. 

Via code:

```swift
selectedConstrain.identifier = "uniqueIdentifierName"
```

Via interface builder 

Select constrain and edit identifier field on right-hand side panel. 

* ## Measuring distances

When you are working on storyboard select element, hold ```Option``` key and hover on other elements to see distances between them.

* ## Renaming code 

If you want to rename variable/constane etc. in all places at once, just select it go to: ```Editor -> Refactor -> Rename```

* ## Fix all issues

New versions of swift can cause some errors - changes in UIKit apis names. To fix that go to: ```Editor -> Fix all issuess```
