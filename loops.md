**Published by Arunprasadh C on 04 May 2022** • *Last Updated on 05 May 2022*

## Loops in Swift
As in any other language, Loops in Swift are used to execute a set of statements repeatedly until a given condition is true or until a termination condition or control statement is not reached. Swift supports three kind of loops :

### `for`-`in` Loop
In Swift, the `for`-`in` loop is used to run a block of code for a certain number of times. It is used to iterate over any sequences such as an `Array`, `Range`, `String`, etc.

**Syntax :**
```swift
for val in sequence
{
  // statements
}
```

Here, `val` accesses each item of the sequence on each iteration. Loop continues until we reach the last item in the sequence.

**Example 1:**
```swift
let languages = ["Swift", "Java", "Kotlin", "C++"]
for language in languages
{
    print(language, terminator: ", ")
}
```

**Output 1:**
```
Swift, Java, Kotlin, C++,
```

The `where` clause can be used to add conditions to filter out the elements to be iterated.

**Example 2:**
```swift
let languages = ["Swift", "Java", "Kotlin", "C++"]

for language in languages where language != "C++"
{
    print(language, terminator: ", ")
}
```

**Output 2:**
```
Swift, Java, Kotlin,
```

We can also use `Range` in `for`-`in` Loop. But, if we want to increment by some fixed amount instead of 1, we can use the `stride()` function.

**Example 3:**
```swift
print("Even numbers from 2 to 20 : ", terminator: "")
for evenNum in stride(from: 2, to: 21, by: 2)
{
    print(evenNum, terminator: ", ")
}
```

**Output 3:**
```
Even numbers from 2 to 20 : 2, 4, 6, 8, 10, 12, 14, 16, 18, 20,
```

### `while` Loop
In Swift, the `while` loop is used to run a specific code as long as a certain condition is met.

**Syntax :**
```swift
while(condition)
{
//loop body
}
```

**Example :**
```swift
var it = 2
print("Even numbers from 2 to 20 : ", terminator: "")
while(it <= 20)
{
    print(it, terminator: ", ")
    it += 2
}
```

**Output :**
```
Even numbers from 2 to 20 : 2, 4, 6, 8, 10, 12, 14, 16, 18, 20,
```

### `repeat`-`while` Loop
In Swift, the `repeat`-`while` loop is similar to `while` loop with one key difference. The body of `repeat`-`while` loop is executed at least once before the test expression is checked (It is similar to `do`-`while` loop of C/C++/Java).

**Syntax :**
```swift
repeat 
{
  // body of loop
} while (condition)
```

**Example :**
```swift
var it = 22
print("Even numbers from 2 to 20 : ", terminator: "")
repeat
{
    print(it, terminator: ", ")
    it += 2
} while (it <= 20)
```

**Output :**
```
Even numbers from 2 to 20 : 22, //22 is shown although 22 > 20 as it is a repeat-while loop
```

A `while` or `repeat`-`while` loop should be used when the exact number of iterations is not known. When the number of iterations is known beforehand or when a sequence needs to be iterated, the `for`-`in` loop should be used.

#### Infinite while loop
An infinite while loop will keep on executing inifinitely until the program is terminated explicitly. It can be constructed by giving an always `true` condition and by not providing any loop control statements inside the body. However, giving a termination condition or using a loop constrol statement is required in realtime situations.

**Example :**
```swift
var count = 0
while(true)
{
    print(count)
    count += 1
}
```

**Output :**
```
0
1
2
3
.
.
.
.
```

As we have seen about Loops in Swift, let's move on to see about Functions in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/decision.html">&larr; Decision-making Constructs</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
