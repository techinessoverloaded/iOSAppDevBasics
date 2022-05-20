**Published by Arunprasadh C on 12 May 2022** • *Last Updated on 20 May 2022*

## Functions in Swift
A Function is a block of code that performs a specific task. In other words, it is a set of statements which can be repeatedly called and executed as and when required. Functions increase the modularity, reusability and flexibility of the overall code. Swift allows both User-defined Functions and Standard Library Functions. We would have seen about two Standard Library Functions `print()` and `readLine()` in [Basic I/O](https://techinessoverloaded.github.io/iOSAppDevBasics/basicio.html). Now, let's see about User-defined Functions in Swift. User-defined Functions in Swift are declared using `func` keyword (As opposed to `fun` in **Kotlin**, `def` in **Python** and conventional functional declaration of C/C++/Java).

**Syntax :**
```swift
func functionName(paramterName1: ParameterType1, parameterName2: ParameterType2, ....) -> ReturnType
{
// Body of function
}
```

Parameters and Return Type are optional and can be given only when required. The function can be called by using the name of the function followed by `()` and any required parameters within parantheses.

**Example 1:**
```swift
func greet()
{
    print("Hello World !")
}
greet()
```
**Output 1:**
```
Hello World !
```

When the function is called, the control of the program goes to the function definition. All codes inside the function are executed. The control of the program jumps to the next statement after the function call.

When parameters are provided, the function call should mention each paramterName followed by a colon `:` and the actual value passed as parameter. Parameters are separated from one another by means of comma `,`.

**Example 2:**
```swift
func greet(name: String)
{
    print("Hello \(name) !")
}
greet(name: "Kris")
```
**Output 2:**
```
Hello Kris !
```

The parameters can also have **Argument Labels** which are the names used when passing arguments to a function. The Argument Label can be specified before the parameter name and they are separated by space. The Argument Label is used only during function call and parameter name is used in function definition. Many parameters can have the same label, but it is recommended to give unique labels for semantic purposes. When an Argument Label is not given, the parameter name is used as the label too.

**Example 3:**
```swift
func greet(name: String, from native: String)
{
    print("Hello \(name) ! Nice to know that you are from \(native) !")
}
greet(name: "Kris", from: "Chennai")
```
**Output 3:**
```
Hello Kris ! Nice to know that you are from Chennai !
```

When we don't want to force the function caller to specify argument labels while calling functions, we can use underscore `_` before parameter name.

**Example 4:**
```swift
func sum(_ numbers: [Int])
{
    var s = 0
    for x in numbers
    {
        s += x
    }
    print("Sum of passed Numbers is: \(s)")
}
sum([1, 2, 4, 10, 11, 20, 39])
```
**Output 4:**
```
Sum of passed Numbers is: 87
```

In the above example, the function `sum()` is called without specifying any argument label because we have used `_` before the parameter `numbers` in the function definition. The most common example of a function using a combination of argument labels and `_` is the `print(_ items: Any..., separator: String = " ", terminator: String = "\n")` where the items to be printed are given without labels and separator and terminator are given when required. Do note that while calling the function, the order of parameters should match the order given in function definition and should not be shuffled. Also, recursive functions are also supported Swift like other languages.

#### Default Parameter values in Functions
Swift allows us to provide default values to parameters (unlike **Java** which allows overloading and like **C/C++/Python/Kotlin** which allow default values to parameters). When default values are set for parameters, it is not compulsory for the caller to pass values to those parameters. If the values are passed, they are used. If not, the default values are used.

**Example 5:**
```swift
func greet(name: String  = "Anonymous", postively: Bool = true)
{
  if postively
  {
    print("Hello \(name) ! Hope you are doing well !")
  }
  else
  {
    print("Hey \(name) ! Please go out !")
  }
}
greet()
greet(name: "Kris")
greet(postively: false)
greet(name: "Anush", postively: false)
```
**Output 5:**
```
Hello Anonymous ! Hope you are doing well !
Hello Kris ! Hope you are doing well !
Hey Anonymous ! Please go out !
Hey Anush ! Please go out !
```

### Variadic Parameters
Variadic Parameters allow zero or more comma-separated values of a Type to be passed as parameter values. They are declared by appending Parameter Type name with three period characters `...` (Example: `Int...`). The Variadic Parameter can be accessed as an `Array` inside the function. When calling a function having Variadic Parameters, zero or more comma-separated values can be passed. 

Consider the program from Example 4. The same program can be implemented with Variadic Parameters.

**Example 6:**
```swift
func sum(_ numbers: Int...)
{
    print(type(of: numbers))
    if numbers.isEmpty
    {
      print("No parameters passed !")
      return
    }
    var s = 0
    for x in numbers
    {
        s += x
    }
    print("Sum of passed Numbers is: \(s)")
}
sum()
sum(1, 2, 4, 10, 11, 20, 39)
```

**Output 6:**
```
Array<Int>
No parameters passed !
Array<Int>
Sum of passed Numbers is: 87
```

### In-Out Parameters
In Swift, the parameters passed to functions are treated as `let` constants by default. So, they cannot be modified anywhere inside the function body. But, they can be assigned with some modification to any new `var`/`let` values (Example: `var newVar = nonInoutLet + 1`). Even a normal Call by Value `swap()` function can't be written (unlike **C/C++/Java**) since `let` constants are used.

**Erroneous Code:**
```swift
func swap(_ x: Int, _ y: Int)
{
    (x, y) = (y, x) // Results in Compile-time error saying y is a let constant
}
```

So, how to make the parameters as `var` variables ? We have to use the `inout` keyword before the annotated type to denote that the parameters are treated as `var` variables inside the function. The caller must insert the ampersand symbol `&` before the variable name while passing values to the In-Out parameter in a function to denote that it is an In-Out parameter. Now, see the following example:

**Example 7.1:**
```swift
func swap(_ x: inout Int, _ y: inout Int)
{
    (x, y) = (y, x) // Using Tuple syntax to swap values (like Python)
}
var a = 5, b = 6
print("Original a and b: (\(a),\(b))")
swap(&a, &b)
print("After swapping a and b: (\(a),\(b))")
```
**Output 7.1:**
```
Original a and b: (5,6)
After swapping a and b: (6,5)
```

You can notice that the swapped values are retained as such even outside the scope of the function. You may wonder how a Value Type like `Int` behaves like a Reference Type. It behaves so because of the `inout` Keyword. The In-Out Parameters work in the following way:

- When the function is called, the value of the argument is copied.
- In the body of the function, the copy is modified.
- When the function returns, the copy’s value is assigned to the original argument.

This behavior is known as **copy-in copy-out** or **Call by Value** result. For example, when a computed property or a property with observers is passed as an In-Out parameter, its getter is called as part of the function call and its setter is called as part of the function return.

As an optimization, when the argument is a value stored at a physical address in memory, the same memory location is used both inside and outside the function body. The optimized behavior is known as **Call by Reference**. It satisfies all of the requirements of the **copy-in copy-out** model while removing the Overhead of Copying.

Do Note that In-Out Parameters cannot have default values and Variadic Parameters cannot be In-Out Parameters in Swift. And, only `var` variables can be passed as arguments to functions accepting In-Out Parameters and `let` constants are not allowed for obvious reasons. Also, the Original variable which was passed as In-Out parameter should NOT be accessed inside the function even if it is available in the scope. Attempting to do so will result in a Fatal error as it is a violation of Swift's Memory Exclusivity Guarantee. For the same reason, the same variable should not be passed to multiple In-Out parameters at once. Attempting to do so will result in a compile-time error.

**Erroneous Code:**
```swift
func swap(_ x: inout Int, _ y: inout Int)
{
    (x, y) = (y, x)
    print(a) // Cause of Error
}
var a = 5, b = 6
print("Original a and b: (\(a),\(b))")
swap(&a, &b)
print("After swapping a and b: (\(a),\(b))")
```
**Output :**
```
Original a and b: (5,6)
Simultaneous accesses to 0x100008070, but modification requires exclusive access.
Previous access (a modification) started at helloworld`main + 708 (0x1000039d4).
Current access (a read) started at:
0    libswiftCore.dylib                 0x00007ff81cee0080 swift::runtime::AccessSet::insert(swift::runtime::Access*, void*, void*, swift::ExclusivityFlags) + 442
1    libswiftCore.dylib                 0x00007ff81cee02e0 swift_beginAccess + 66
2    helloworld                         0x0000000100003ce0 swap(_:_:) + 106
3    helloworld                         0x0000000100003710 main + 755
(lldb) 
```

The same **Call by Reference** Behaviour can be achieved by means of the `UnsafeMutablePointer` `struct`, although it is not recommended to do so as Pointers are involved (That's why it is termed as Unsafe in Swift). Note that when Pointer arguments are expected, the caller must specify `&` before the name of the variable which is passed as arguments.

**Example 7.2**
```swift
func swapUsingPointer(_ a: UnsafeMutablePointer<Int>, _ b: UnsafeMutablePointer<Int>)
{
    (a.pointee, b.pointee) = (b.pointee, a.pointee) //pointee gives the value pointed by the pointer
}
var a = 5, b = 6
print("Original a and b: (\(a),\(b))")
swapUsingPointer(&a, &b)
print("After swapping a and b: (\(a),\(b))")
```
**Output 7.2:**
```
Original a and b: (5,6)
After swapping a and b: (6,5)
```

### Return Types of Functions
The Return Type of the function decides the Type of result returned by the function. The Return Type is specified by an arrow `->` after the parantheses of the function. When a function does not require a Return Type, it can be simply ignored and the Swift Compiler will infer the Return Type as `Void` meaning nothing (Represented by an Empty Tuple `()`).

Consider the program given in Example 6. It is actually contradicting in meaning that the Arithmetic Sum function has no Return Type. It would be more meaningful if the Arithmetic Sum function would actually return the sum rather than printing it.

**Example 8:**
```swift
func sum(_ numbers: Int...) -> Int
{
    print(type(of: numbers))
    if numbers.isEmpty
    {
      return 0
    }
    var s = 0
    for x in numbers
    {
        s += x
    }
    return s
}
print(sum(1, 2, 4, 10, 11, 20, 39))
```

**Output 8:**
```
Array<Int>
87
```

#### Optional Types as Return Types
We can also declare an Optional Types as Return Type for a Function that is expected to return `nil` in one or more cases.

Consider Example 7's Program. When the Variadic Parameter `numbers` contains no value, `0` is returned. But it is also possible that sum of some numbers can lead to zero. So, we can change the return type to `Int?` and return `nil` when `numbers` is empty.

**Example 9:**
```swift
func sum(_ numbers: Int...) -> Int?
{
    if numbers.isEmpty
    {
      return nil
    }
    var s = 0
    for x in numbers
    {
        s += x
    }
    return s
}
if let result = sum(1, 2, 4, 10, 11, 20, 39)
{
  print("The sum is: \(result).")
}
else
{
  print("No parameter was passed !")
}
if let result = sum()
{
  print("The sum is: \(result).")
}
else
{
  print("No parameter was passed !")
}
```

**Output 9:**
```
The sum is: 87.
No parameter was passed !
```

#### Functions with Multiple Return Values
A Swift Function can return more than one value by means of a Tuple. The Return Type can be specified as a Tuple of values or even as an `Optional` Tuple of values.

**Example 10:**
```swift
func getMinMax(_ numbers: Int...) -> (min: Int?, max: Int?)?
{
    if numbers.isEmpty
    {
      return nil
    }
    return (numbers.min(), numbers.max())
}
if let result = getMinMax(34, 10, 99, 108)
{
  let min = result.min ?? Int.min
  let max = result.max ?? Int.max
  print("Min: \(min)")
  print("Max: \(max)")
}
else
{
  print("No parameter was passed !")
}
```
**Output 10:**
```
Min: 10
Max: 108
```

#### Functions with Implicit Return
If the entire body of the function is a **Single Expression**, the function implicitly returns that expression and there's no need to use the `return` Keyword (Like **Kotlin**). For example, both the functions below have the same behavior:

**Example 11:**
```swift
func checkDivisibilityBy2(of number: Int) -> Bool
{
    return number%2 == 0
}

func checkDivisibilityBy2Again(of number: Int) -> Bool
{
    number%2 == 0 // Implicitly returns a Bool. return keyword not used.
}

print(checkDivisibilityBy2(of: 46) ? "46 is Divisible by 2" : "46 is not Divisible by 2")
print(checkDivisibilityBy2Again(of: 46) ? "46 is Divisible by 2" : "46 is not Divisible by 2")
```
**Output 11:**
```
46 is Divisible by 2
46 is Divisible by 2
```

### Function Types
Every Function in Swift has a specific Function Type, made up of the Parameter Types and the Return Type of the Function. With the support for Function Types comes the support for Function Objects (Just like **C/C++/Python** Function Objects or **Java** Functional Interfaces or **C#** Delegates). So, functions can also be assigned to `var` or `let` and used like Other Types. Even the Function Type returned by the `type(of: )` Function can be compared to check the type just like how it is done with `Int` or other types and even `typealias` can be used with Function Types. A Function Type is represented by means of Tuples for Parameters and Return Type and an Arrow `->` for showing Return Type. As mentioned earlier, the `Void` type is represented as an empty Tuple `()`.

**Example 12.1:**
```swift
func swap(_ x: inout Int, _ y: inout Int)
{
    (x, y) = (y, x)
}
print(type(of: swap))
print(type(of: swap) == ((inout Int, inout Int) -> ()).self)
```
**Output 12.1:**
```
(inout Int, inout Int) -> ()
true
```

Function Types can be assigned/reassigned and used like other types.

**Example 12.2:**
```swift
func addition(_ numbers: Int...) -> Int
{
    var s = 0
    numbers.forEach{
        s += $0
    }
    return s
}

func multiplication(_ numbers: Int...) -> Int
{
    var p = 1
    numbers.forEach{
        p *= $0
    }
    return p
}

var performOperation: (Int...) -> Int = addition // Assigning performOperation to Addition Function
print("Sum: \(performOperation(99, 88, 77, 55, 33))")
performOperation = multiplication // Assigning performOperation to Multiplication Function
print("Product: \(performOperation(99, 88, 77, 55, 33))")
```
**Output 12.2:**
```
Sum: 352
Product: 1217545560
```

Function Types can also be used as Parameters in other functions. This facilitates developers to write higher order functions.

**Example 12.3:**
```swift
func addition(_ numbers: Int...) -> Int
{
    var s = 0
    numbers.forEach{
        s += $0
    }
    return s
}

func printAdditionResult(additionFn: (Int...) -> Int)
{
    print("The sum is: \(additionFn(78, 99, 12, 34, 56))")
}

printAdditionResult(additionFn: addition)
```
**Output 12.3:**
```
The sum is: 279
```

Function Types can also be used as Return Type of other functions.

**Example 12.4:**
```swift
typealias functionTemplate = (Int) -> Int

func incrementAndReturn(_ value: Int) -> Int
{
    value + 1
}

func decrementAndReturn(_ value: Int) -> Int
{
    value - 1
}

func chooseIncOrDec(shouldDecrement: Bool = false) -> functionTemplate
{
    shouldDecrement ? decrementAndReturn : incrementAndReturn
}

print(type(of: incrementAndReturn) == functionTemplate.self)
var a = 5
print("Moving 5 towards zero...")
let chosenFunction = chooseIncOrDec(shouldDecrement: true)
while a >= 0
{
    print(a)
    a = chosenFunction(a)
}
```
**Output 12.4:**
```
true
Moving 5 towards zero...
5
4
3
2
1
0
```

### Nested Functions
Till now, we have seen about functions declared at the **Global Scope**. We can also declare functions inside the scope of other functions. These are known as **Nested Functions**. We can rewrite the program from Example 12.4 using Nested Functions as shown below.

**Example 13:**
```swift
typealias functionTemplate = (Int) -> Int

func chooseIncOrDec(shouldDecrement: Bool = false) -> functionTemplate
{
    func incrementAndReturn(_ value: Int) -> Int
    {
        value + 1
    }
    func decrementAndReturn(_ value: Int) -> Int
    {
        value - 1
    }
    return shouldDecrement ? decrementAndReturn : incrementAndReturn
}

var a = 5
print("Moving 5 towards zero...")
let chosenFunction = chooseIncOrDec(shouldDecrement: true)
while a >= 0
{
    print(a)
    a = chosenFunction(a)
}
```
**Output 13:**
```
Moving 5 towards zero...
5
4
3
2
1
0
```

### Function Overloading
Swift allows Compile-time Polymorphism a.k.a Function Overloading where a function with the same name can be called with varying arguments.
The overloaded function can deiffer by:
- The number of arguments
- The type of arguments
- The ordering of arguments
- The Argument Labels

Note that the Return types don't matter for overloading a function.

**Example 14:**
```swift
func println2(_ items: Any...)
{
    for x in items
    {
        print(x, terminator: " ")
    }
    print("\n")
}

func println2(_ items: Any..., separator: String)
{
    for x in items
    {
        print(x, terminator: separator)
    }
    print("\n")
}

func println2(separator: String, _ items: Any...)
{
    for x in items
    {
        print(x, terminator: separator)
    }
    print("\n")
}

println2("Hello","World")
println2("Hope you are doing well !")
println2("This is from an overloaded function !",45,60,39,57.5,separator: ", ")
println2(separator: " -> ","This is from another overloaded function !",99,66,"Hello",154.9)
```
**Output 13:**
```
Hello World 

Hope you are doing well ! 

This is from an overloaded function !, 45, 60, 39, 57.5, 

This is from another overloaded function ! -> 99 -> 66 -> Hello -> 154.9 ->
```


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/collections.html">&larr; Collections</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/closures.html">Closures &rarr;</a>
</span>
