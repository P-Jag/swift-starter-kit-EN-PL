# String Interpolation


**EN:**

String interpolation let us combine variables and constants (var and let) into a string. 

**PL:**

Pozwala nam na łączenie zmiennych ze stringiem - Inaczej dzięki String interpolation możemy użyć naszych zmiennych wewnątrz stringa. 

```swift

var name = "John McClane"
var year = 1988

"Die Hard and it's main character \(name) was introduced in \(year)"

The output will be: 

"Die Hard and it's main character John McClane was introduced in 1988"

```

**EN:**

You can manipulate string with tripple " (""") to make multiple lines in current string

**PL:**

Możesz użyć potrójnego " ("""), żeby móc tworzyć kilka lini w ramach jednego stringa. 

```swift

let quotation = """
This is a first line
and this is 2nd one
yo can also add
3rd, 4th etc. it's totally up to You
"""

```
