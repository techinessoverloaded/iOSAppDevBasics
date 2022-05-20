**Published by Arunprasadh C on 19 May 2022** • *Last Updated on 20 May 2022*

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

The `in` keyword is used to separate parameter declaration from the body of the function. In-Out Parameters are allowed in Closures but Default Parameter values are not allowed in Closures. Named Variadic Parameters and Tuples can also be used with Closures. Closures make it easier to write **Higher Order Functions** (Functions which take Other Functions as Parameters). For example, consider the `sorted(by:)` Function from the Swift Standard Library for Arrays, which sorts the `Array` according to the comparison function given as parameter and returns the sorted array.
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

**Modified Example 1:**
```swift
let arr = [34, 99, 56, 12, 10, 108, 543, 7]
print("Original Array: \(arr)")
let sortedArr = arr.sorted { lhs, rhs in
    lhs > rhs
}
print("Array sorted in Descending Order: \(sortedArr)")
```
**Output 1:**
```
Original Array: [34, 99, 56, 12, 10, 108, 543, 7]
Array sorted in Descending Order: [543, 108, 99, 56, 34, 12, 10, 7]
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/functions.html">&larr; Functions</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
