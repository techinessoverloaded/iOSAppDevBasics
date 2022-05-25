**Published by Arunprasadh C on 19 May 2022** • *Last Updated on 25 May 2022*

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

#### Capturing Values
A closure can capture constants and variables from the surrounding context in which it’s defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.

In Swift, the simplest form of a closure that can capture values is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.

**Example 3:**
```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int
{
    var runningTotal = 0
    func incrementer() -> Int
    {
        runningTotal += amount // runningTotal and amount captured by closure
        return runningTotal
    }
    return incrementer
}
let incrementBy10 = makeIncrementer(forIncrement: 10)
for _ in 0...3
{
    print("Incremented by 10: \(incrementBy10())")
}
let incrementBy20 = makeIncrementer(forIncrement: 20)
for _ in 0...3
{
    print("Incremented by 20: \(incrementBy20())")
}
print("Sum of both incrementers: \(incrementBy10() + incrementBy20())")
```
**Output 3:**
```
Incremented by 10: 10
Incremented by 10: 20
Incremented by 10: 30
Incremented by 10: 40
Incremented by 20: 20
Incremented by 20: 40
Incremented by 20: 60
Incremented by 20: 80
Sum of both incrementers: 150
```

The return type of `makeIncrementer(forIncrement:)` is `() -> Int`. This means that it returns a function, rather than a simple value. The function it returns has no parameters, and returns an `Int` value each time it’s called. The `makeIncrementer(forIncrement:)` function defines an integer variable called `runningTotal`, to store the current running total of the incrementer that will be returned. This variable is initialized with a value of 0. The `makeIncrementer(forIncrement:)` function has a single `Int` parameter with an argument label of `forIncrement`, and a parameter name of `amount`. The argument value passed to this parameter specifies how much `runningTotal` should be incremented by each time the returned incrementer function is called. The `makeIncrementer(forIncrement:)` function defines a nested function called incrementer, which performs the actual incrementing. This function simply adds `amount` to `runningTotal`, and returns the result.

The `incrementer()` function doesn’t have any parameters, and yet it refers to `runningTotal` and `amount` from within its function body. It does this by capturing a reference to `runningTotal` and `amount` from the surrounding function and using them within its own function body. Capturing by reference ensures that `runningTotal` and `amount` don’t disappear when the call to `makeIncrementer(forIncrement:)` ends, and also ensures that `runningTotal` is available the next time the `incrementer()` function is called.

**NOTE:** If you assign a closure to a property of a class instance, and the closure captures that instance by referring to the instance or its members, you will create a strong reference cycle between the closure and the instance. Swift uses **Capture Lists** to break these strong reference cycles. By means of Capture Lists, we can specify whether the captured references should be `weak` or `unowned` references, thereby preventing Strong Reference Cycles. Capture Lists can be defined before closure parameters within square brackets `[]` separated by commas `,`.

#### Closures are Reference Types 
In the example above, `incrementBy10` and `incrementBy20` are constants, but the closures these constants refer to are still able to increment the `runningTotal` variables that they have captured. This is because functions and closures are reference types.

Whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a reference to the function or closure. In the example above, it’s the choice of closure that `incrementBy10` refers to that’s constant, and not the contents of the closure itself. This also means that if you assign a closure to two different constants or variables, both of those constants or variables refer to the same closure.

#### Escaping Closures
A Closure is called as an Escaping Closure when it is passed as an argument to a function but is called only after the function execution completes. Escaping Closures are denoted by placing `@escaping` attribute (Attributes in Swift are like Annotations in Java) before the closure type. Escaping Closures can be used to handle events like completion of a function.

**Example 4:**
```swift
var completionHandlers: [Int : (Int) -> Void] = [:]
func functionWithCompletionTracker(seed: Int, completionHandler: @escaping (Int) -> Void)
{
    if seed.isMultiple(of: 2)
    {
        completionHandlers[seed] = completionHandler
    }
}
let sampleCompletionHandler: (Int) -> Void  = {
    print("functionWithCompletionTracker() completed successfully for seed \($0) !")
}
for x in 0..<4
{
    let random = Int.random(in: x...40)
    functionWithCompletionTracker(seed: random, completionHandler: sampleCompletionHandler)
    if let handler = completionHandlers[random]
    {
        handler(random)
    }
    else
    {
        print("No Completion Handler for \(random) !")
    }
}
```
**Output 4:**
```
No Completion Handler for 15 !
No Completion Handler for 27 !
functionWithCompletionTracker() completed successfully for seed 10 !
functionWithCompletionTracker() completed successfully for seed 10 !
```

Normally, a closure captures variables implicitly by using them in the body of the closure, but in this case you need to be explicit. If you want to capture `self`, write `self` explicitly when you use it, or include `self` in the closure’s capture list. Writing `self` explicitly lets you express your intent, and reminds you to confirm that there isn’t a reference cycle. If `self` is an instance of a structure or an enumeration, you can always refer to `self` implicitly. However, an escaping closure can’t capture a mutable reference to `self` when `self` is an instance of a structure or an enumeration. 

#### Autoclosures
An autoclosure is a closure that’s automatically created to wrap an expression that’s being passed as an argument to a function. It doesn’t take any arguments, and when it’s called, it returns the value of the expression that’s wrapped inside of it. This syntactic convenience lets you omit braces around a function’s parameter by writing a normal expression instead of an explicit closure.

An autoclosure lets you delay evaluation, because the code inside isn’t run until you call the closure. Delaying evaluation is useful for code that has side effects or is computationally expensive, because it lets you control when that code is evaluated. The code below shows how a closure delays evaluation.

**Example 5:**
```swift
var customersInLine = ["Kris", "Hari", "Shiv", "Sunder", "Sathya"]
print(customersInLine.count)
let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
print("Now serving \(customerProvider())!")
print(customersInLine.count)
```
**Output 5:**
```
5
5
Now serving Kris!
4
```

Even though the first element of the `customersInLine` array is removed by the code inside the closure, the array element isn’t removed until the closure is actually called. If the closure is never called, the expression inside the closure is never evaluated, which means the array element is never removed. Note that the type of `customerProvider` isn’t String but `() -> String` —a function with no parameters that returns a `String`.

Now, when I use an AutoClosure (denoted by `@autoclosure` attribute) as a function parameter, I can directly pass an expression for the closure instead of a closure.

**Modified Example 5:**
```swift
var customersInLine = ["Kris", "Hari", "Shiv", "Sunder", "Sathya"]
print(customersInLine.count)
func serveCustomer(customerProvider: @autoclosure () -> String)
{
    print("Now serving \(customerProvider())!")
}
serveCustomer(customerProvider: customersInLine.remove(at: 0)) // Using autoclosure
print(customersInLine.count)
```
**Output 5:**
```
5
Now serving Kris!
4
```

Now that we have seen about closures, let's move on to see about Structures in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/functions.html">&larr; Functions</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/structs.html">Structures &rarr;</a>
</span>
