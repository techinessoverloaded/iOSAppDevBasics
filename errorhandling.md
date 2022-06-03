**Published by Arunprasadh C on 03 June 2022** • *Last Updated on 03 June 2022*

## Error Handling in Swift
Error handling is the process of responding to and recovering from error conditions in your program. Swift provides first-class support for throwing, catching, propagating, and manipulating recoverable errors at runtime.

Some operations aren’t guaranteed to always complete execution or produce a useful output. Optionals are used to represent the absence of a value, but when an operation fails, it’s often useful to understand what caused the failure, so that your code can respond accordingly.

As an example, consider the task of reading and processing data from a file on disk. There are a number of ways this task can fail, including the file not existing at the specified path, the file not having read permissions, or the file not being encoded in a compatible format. Distinguishing among these different situations allows a program to resolve some errors and to communicate to the user any errors it can’t resolve.

**NOTE:** Error handling in Swift interoperates with error handling patterns that use the `NSError` class in Cocoa and Objective-C. 

### Representing and Throwing Errors
In Swift, errors are represented by values of types that conform to the `Error` protocol. This empty protocol indicates that a type can be used for error handling.

Swift enumerations are particularly well suited to modeling a group of related error conditions, with associated values allowing for additional information about the nature of an error to be communicated. For example, here’s how you might represent the error conditions of operating a vending machine inside a game:

**Example 1:**
```swift
enum VendingMachineError: Error
{
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

Throwing an error lets you indicate that something unexpected happened and the normal flow of execution can’t continue. You use a `throw` statement to throw an error. For example, the following code throws an error to indicate that five additional coins are needed by the vending machine:

**Example 1.1:**
```swift
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```

### Handling Errors
When an error is thrown, some surrounding piece of code must be responsible for handling the error—for example, by correcting the problem, trying an alternative approach, or informing the user of the failure.

There are four ways to handle errors in Swift. You can propagate the error from a function to the code that calls that function, handle the error using a `do-catch` statement, handle the error as an optional value, or assert that the error will not occur. Each approach is described in a section below.

When a function throws an error, it changes the flow of your program, so it’s important that you can quickly identify places in your code that can throw errors. To identify these places in your code, write the `try` keyword—or the `try?` or `try!` variation—before a piece of code that calls a function, method, or initializer that can throw an error. These keywords are described in the sections below.

**NOTE:** Error handling in Swift resembles exception handling in other languages, with the use of the try, catch and throw keywords. Unlike exception handling in many languages—including Objective-C—error handling in Swift doesn’t involve unwinding the call stack, a process that can be computationally expensive. As such, the performance characteristics of a throw statement are comparable to those of a `return` statement.

#### Propagating Errors Using Throwing Functions
To indicate that a function, method, or initializer can throw an error, you write the `throws` keyword in the function’s declaration after its parameters. A function marked with `throws` is called a throwing function. If the function specifies a return type, you write the `throws` keyword before the return arrow (`->`). A throwing function propagates errors that are thrown inside of it to the scope from which it’s called. Only throwing functions can propagate errors. Any errors thrown inside a nonthrowing function must be handled inside the function.

**Example 2:**
```swift
enum DivisionError: Error
{
    case divideByZero(cause: String)
}

func divide(_ dividend: Int, _ divisor: Int) throws -> Int // Propagating error using throws
{
    guard divisor != 0 else
    {
        throw DivisionError.divideByZero(cause: "Divisor is Zero !")
    }
    return dividend/divisor
}
```

Because the `divide(_:,_:)` function propagates any errors it throws, any code that calls this method must either handle the errors—using a `do-catch` statement, `try?`, or `try!` —or continue to propagate them. 

**Example 2.1:**
```swift
print(try divide(90, 0))
```
**Output 2.1:**
```
Swift/ErrorType.swift:200: Fatal error: Error raised at top level: helloworld.DivisionError.divideByZero(cause: "Divisor is Zero !")
2022-06-03 13:03:24.722211+0530 helloworld[18394:181436] Swift/ErrorType.swift:200: Fatal error: Error raised at top level: helloworld.DivisionError.divideByZero(cause: "Divisor is Zero !")
```

#### Handling Errors Using Do-Catch
You use a `do-catch` statement to handle errors by running a block of code. If an error is thrown by the code in the `do` clause, it’s matched against the `catch` clauses to determine which one of them can handle the error.

**Syntax:**
```swift
do 
{
    try expression
    statements
} 
catch pattern 1 
{
    statements
} 
catch pattern 2 where condition 
{
    statements
} catch pattern 3, pattern 4 where condition 
{
    statements
} 
catch 
{
    statements
}
```

You write a pattern after `catch` to indicate what errors that clause can handle. If a `catch` clause doesn’t have a pattern, the clause matches any error and binds the error to a local constant named `error`. 

**Example 3:**
```swift
enum DivisionError: Error
{
    case divideByZero(cause: String)
}

func divide(_ dividend: Int, _ divisor: Int) throws -> Int
{
    guard divisor != 0 else
    {
        throw DivisionError.divideByZero(cause: "Divisor is Zero !")
    }
    return dividend/divisor
}

do
{
    let quotient = try divide(90, 0)
    print("Quotient is: \(quotient)")
}
catch
{
    print(error)
}
```
**Output 3:**
```
divideByZero(cause: "Divisor is Zero !")
```

#### Converting Errors to Optional Values
You use `try?` to handle an error by converting it to an optional value. If an error is thrown while evaluating the `try?` expression, the value of the expression is `nil`.

**Example 4:**
```swift
enum DivisionError: Error
{
    case divideByZero(cause: String)
}

func divide(_ dividend: Int, _ divisor: Int) throws -> Int
{
    guard divisor != 0 else
    {
        throw DivisionError.divideByZero(cause: "Divisor is Zero !")
    }
    return dividend/divisor
}

var result = try? divide(90, 0)
if let quotient = result
{
    print("Quotient: \(quotient)")
}
else
{
    print("Error occurred ! Zero was found as divisor !")
}
```
**Output 4:**
```
Error occurred ! Zero was found as divisor !
```

#### Disabling Error Propagation
Sometimes you know a throwing function or method won’t, in fact, throw an error at runtime. On those occasions, you can write `try!` before the expression to disable error propagation and wrap the call in a runtime assertion that no error will be thrown. If an error actually is thrown, you’ll get a runtime error.

**Example 5:**
```swift
enum DivisionError: Error
{
    case divideByZero(cause: String)
}

func divide(_ dividend: Int, _ divisor: Int) throws -> Int
{
    guard divisor != 0 else
    {
        throw DivisionError.divideByZero(cause: "Divisor is Zero !")
    }
    return dividend/divisor
}

var result = try! divide(90, 45) // It is known beforehand that 90/45 won't throw an error. So, use try!.
print("Quotient = \(result)")
```
**Output 5:**
```
Quotient = 2
```

### Specifying Cleanup Actions
You use a `defer` statement to execute a set of statements just before code execution leaves the current block of code. This statement lets you do any necessary cleanup that should be performed regardless of how execution leaves the current block of code—whether it leaves because an error was thrown or because of a statement such as `return` or `break`. For example, you can use a `defer` statement to ensure that file descriptors are closed and manually allocated memory is freed.

A `defer` statement defers execution until the current scope is exited. This statement consists of the `defer` keyword and the statements to be executed later. The deferred statements may not contain any code that would transfer control out of the statements, such as a `break` or a `return` statement, or by throwing an error. Deferred actions are executed in the reverse of the order that they’re written in your source code. That is, the code in the first `defer` statement executes last, the code in the second `defer` statement executes second to last, and so on. The last `defer` statement in source code order executes first.

**Example 6:**
```swift
func processFile(filename: String) throws 
{
    if exists(filename) 
    {
        let file = open(filename)
        defer 
        {
            close(file)
        }
        while let line = try file.readline() 
        {
            // Work with the file.
        }
        // close(file) is called here, at the end of the scope.
    }
}
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/generics.html">&larr; Generics</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
