**Published by Arunprasadh C on 22 Apr 2022** • *Last Updated on 02 May 2022*

## Basic Input and Output in Swift
Basic I/O Functions are used to print output to the standard output (usually console on the screen) and to get input from the standard input (usually provided through keyboard on the console). As in every other programming language, Swift too has its own set of I/O functions.

### Output Function
Swift provides the `print()` function for printing output on the console. The `print()` function accepts three parameters. The prototype is as follows :
```swift
print(_ items: Any..., separator: String = " ", terminator: String = "\n")
```

- `items` - The variable argument object(s) of `Any` type to be printed.
- `separator` - The `String` to be used to separate multiple items while printing. The default value is a single whitespace `" "`.
- `terminator` - The `String` to be printed after printing the `items`. The default value is a newline escape sequence `"\n"`.

**Example 1 :**
```swift
print("Hello World")
```

**Output 1 :**
```
Hello World
```

**Example 2 :**
```swift
var name = "Kris"
print("Good morning",name,separator: ",",terminator: " ")
print("!")
```

**Output 2 :**
```
Good morning,Kris !
```

### Input Function
Swift uses a single function called `readLine()` for getting User Input from the Command Line. The `readLine()` function returns an `Optional<String>` as result. The value will be `nil` if no user Input was provided. The optional `Bool` argument `strippingNewline` strips away Newline Character `\n` if passed as `true`.

**Example 1 :**
```swift
print("Enter your name :")
var name = readLine() ?? "Anonymous"
print("Hello \(name) !")
```

When "Kris" is entered as Input, we get the following Output:

**Output 1 :**
```
Hello Kris !
```

If we want to get `Int` or any other Numerical Data Type input we need to first unwrap the result of `readLine()` and pass the `String` to the appropriate constructor.

**Example 2 :**
```swift
if let strVal = readLine(strippingNewline: true)
{
    let floatVal: Float = Float(strVal) ?? 0.0
    print("Float value : \(floatVal)")
    let intVal: Int = Int(floatVal)
    print("Int value : \(intVal)")
}
else
{
    fatalError("No User Input Provided !")
}
```

When "45.6" is entered as Input, we get the following Output:

**Output 2 :**
```
45.6
Float value : 45.6
Int value : 45
```

We can also get multiple inputs separated by some characters as input and split the resultant unwrapped `String` to access individual values and use them.

**Example 3 :**
```swift
var str = readLine() ?? ""
var elements = str.split(separator: ",")
var firstElement = Int(elements[0]) ?? 0
print("The first element is: \(firstElement) with type: \(type(of: firstElement))")
```

When "45,67,Hello" is entered as Input, we get the following Output:

**Output 3 :**
```
45,67,Hello
The first element is: 45 with type: Int
```

Now as we have seen about Basic I/O in Swift, we can move on to see about Operators in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/varconst.html">&larr; Variables, Literals and Constants</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/operators.html">Operators &rarr;</a>
</span>
