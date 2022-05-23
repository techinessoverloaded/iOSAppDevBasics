**Published by Arunprasadh C on 19 May 2022** • *Last Updated on 23 May 2022*

## Closures in Swift
Closures are self-contained blocks of functionality that can be passed around and used in our code (Similar to **Lambda Expressions** of **Java/C/C++/Python/Kotlin**). Closures can capture and store references to any Constants and Variables from the context in which they’re defined. This is known as closing over those Constants and Variables. Swift handles all of the memory management of capturing values. 

Global and nested functions, as introduced in [Functions](https://techinessoverloaded.github.io/iOSAppDevBasics/functions.html), are actually special cases of Closures. Closures take one of three forms:

- **Global functions** are closures that have a name and don’t capture any values.
- **Nested functions** are closures that have a name and can capture values from their enclosing function.
- **Closure expressions** are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.

Swift’s closure expressions have a clean and clear style, with optimizations that encourage brief, clutter-free syntax in common scenarios. These optimizations include:

- Inferring parameter and return value types from context.
- Implicit returns from single-expression closures.
- Shorthand argument names.
- Trailing closure syntax.

### Closure Expressions
Closure expression syntax has the following general form:

**Syntax :**
```swift
{ (parameters) -> returnType in
   // Set of statements
}
```

The `in` keyword is used to separate parameter declaration from the body of the closure. In-Out Parameters are allowed in Closures but Default Parameter values are not allowed in Closures. Named Variadic Parameters and Tuples can also be used with Closures. Closures make it easier to write **Higher Order Functions** (Functions which take Other Functions as Parameters). For example, consider the `sorted(by:)` Function from the Swift Standard Library for Arrays, which sorts the `Array` according to the comparison function given as parameter and returns the sorted array.
If we are to give this comparison function as a Function Object, it would look like:

**Example 1:**
```swift
func decreasingOrder(lhs: Int, rhs: Int) -> Bool
{
    lhs > rhs
}

let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted(by: decreasingOrder)
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

This looks too Verbose right ? We can simplify the above code using Closures:

**Example 1.1:**
```swift
let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted(by: { (lhs: Int, rhs: Int) -> Bool in
    lhs > rhs
})
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1.1:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

Notice that just like Functions, Closures can also use implicit return (No need to specify `return` keyword when there is only a single expression in the body of closure).

A more simpler way is to pass the operator function `>` to the `sorted(by:)` function. But, it is not preferred here as we are discussing about Closures.

#### Inferring Type from Context
Since the `sorted(by:)` function takes a closure as an argument, the type of parameter and return type of the Closure can be inferred by Swift.
Now, Example 1 can be modified as shown below:

**Example 1.2:**
```swift
let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted(by: { lhs, rhs in lhs > rhs })
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1.2:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

#### Shorthand Argument Names
Swift automatically provides shorthand argument names to inline closures, which can be used to refer to the values of the closure’s arguments by the names `$0`, `$1`, `$2` (upto `n-1` where `n` is the number of arguments), and so on. By doing so, the `in` keyword and argument list can be avoided.

**Example 1.3:**
```swift
let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted(by: { $0 > $1 })
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1.3:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

#### Trailing Closures
If you need to pass a closure expression to a function as the function’s final argument and the closure expression is long, it can be useful to write it as a trailing closure instead. You write a trailing closure after the function call’s parentheses, even though the trailing closure is still an argument to the function. When you use the trailing closure syntax, you don’t write the argument label for the first closure as part of the function call. A function call can even include multiple trailing closures.

Now, Example 1.3 can be modified as:

**Example 1.4:**
```swift
let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted() { $0 > $1 }
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1.4:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

Now, since the closure is the only argument provided to the function, the code can be further simplified as:

**Example 1.5:**
```swift
let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted { $0 > $1 }
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1.5:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

Notice how using Closure simplified the large expression in Example 1 to a single line Expression in Example 1.5.

If a function takes multiple closures, you omit the argument label for the first trailing closure and you label the remaining trailing closures. For example, the function below loads a picture for a photo gallery:

**Example 2:**
```swift
func loadPicture(from server: Server, completion: (Picture) -> Void, onFailure: () -> Void) {
    if let picture = download("photo.jpg", from: server) {
        completion(picture)
    } else {
        onFailure()
    }
}
```

When you call this function to load a picture, you provide two closures. The first closure is a completion handler that displays a picture after a successful download. The second closure is an error handler that displays an error to the user. Now, to call the `loadPicture(from:completion:onFailure:)`, we can write the following code.

**Example 2.1:**
```swift
loadPicture(from: someServer) { picture in
    someView.currentPicture = picture
} onFailure: {
    print("Couldn't download the next picture.")
}
```

In this example, the `loadPicture(from:completion:onFailure:)` function dispatches its network task into the background, and calls one of the two completion handlers when the network task finishes. Writing the function this way lets you cleanly separate the code that’s responsible for handling a network failure from the code that updates the user interface after a successful download, instead of using just one closure that handles both circumstances.


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/functions.html">&larr; Functions</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
