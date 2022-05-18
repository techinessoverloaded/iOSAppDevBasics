**Published by Arunprasadh C on 12 May 2022** • *Last Updated on 18 May 2022*

## Functions and Closures in Swift
### Functions
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

In the above example, the function `sum()` is called without specifying any argument label because we have used `_` before the parameter `numbers` in the function definition. The most common example of a function using a combination of argument labels and `_` is the `print(_ items: Any..., separator: String = " ", terminator: String = "\n")` where the items to be printed are given without labels and separator and terminator are given when required. Do note that while calling the function, the order of parameters should match the order given in function definition and should not be shuffled.

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

#### Variadic Parameters
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

#### Return Types of Functions
The Return Type of the function decides the Type of result returned by the function. The Return Type is specified by an arrow `->` after the parantheses of the function. When a function does not require a Return Type, it can be simply ignored and the Swift Compiler will infer the Return Type as `Void` meaning nothing (Represented by an Empty Tuple `()`).

Consider the program given in Example 6. It is actually contradicting in meaning that the Arithmetic Sum function has no Return Type. It would be more meaningful if the Arithmetic Sum function would actually return the sum rather than printing it.

**Example 7:**
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

**Output 7:**
```
Array<Int>
87
```

##### Optional Types as Return Types
We can also declare an Optional Types as Return Type for a Function that is expected to return `nil` in one or more cases.

Consider Example 7's Program. When the Variadic Parameter `numbers` contains no value, `0` is returned. But it is also possible that sum of some numbers can lead to zero. So, we can change the return type to `Int?` and return `nil` when `numbers` is empty.

**Example 8:**
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

**Output 8:**
```
The sum is: 87.
No parameter was passed !
```



**Example 9:**
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
**Output 9:**
```
Min: 10
Max: 108
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/collections.html">&larr; Collections</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
