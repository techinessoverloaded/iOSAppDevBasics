**Published by Arunprasadh C on 25 Apr 2022** • *Last Updated on 25 Apr 2022*

## Tuples and Optionals in Swift

### Tuples
Tuples are used to group multiple values in a single compound value. The values can be of different Data Types. Type Annotation cannot be used with Tuples as they are statically defined. The basic syntax of `Tuple` is as follows:
```swift
var TupleName = (value1, value2,… any number of values) // for Variables
```
**OR**
```swift
let TupleName = (value1, value2,… any number of values) // for Constants
```
The elements of a `Tuple` can be accessed using Index value starting from `0` till `n-1` where `n` is the number of elements in the `Tuple`.

**Example :**
```swift
let error = (404, "Not Found")
print("The error code is : \(error.0)")
print("The error description is : \(error.1)")
```

**Output :**
```
The error code is : 404
The error description is : Not Found
```

I have used **String Interpolation** in the above example. It will be covered in the Next Topic Page.

### Optionals
`Optional` is a Data Type which is used in situations where either there can be a Value or there can be no Value at all. When there is no value, it is represented as `nil` (Just like `NULL` in **C/C++** or like `null` in **Java**. But `nil` is not a Pointer as in other languages). `nil` can be assigned only to variables/constants of `Optional` type. General Syntax of declaring an `Optional` variable is as follows:

```swift
var name: DataType? 
```
The type of the variable will be `Optional<DataType>`.

**Example 1 - Nillable String :**
```swift
var nillableString: String?
print(nillableString)
nillableString = "Hello"
print(nillableString)
print(type(of: nillableString))
print(nillableString!)
print(type(of: nillableString!))
```

**Output 1 :**
```
nil
Optional("Hello")
Optional<String>
Hello
String
```
In the above example, when an `Optional<String>` is not initialized, `nil` is taken as the default value. But, if it is not `Optional`, then the program will not compile as the variable is not initialized. Notice that when I called the `type(of: )` function on `nillableString`, it showed the Type as `Optional<String>`. But, when I called `type(of: )` function on `nillableString!`, it showed the Type as `String` ! No, it was not magic or error of compiler. It happened because of the **Forced Unwrapping** Operator `!`. So, what is **Unwrapping** ? The **Type Casting** of the `Optional` object to the Actual Type of  object is known as **Unwrapping**. **Unwrapping** can be done in many ways:

#### Using `if`-`else` Block  :
**Example 2 :**
```swift
var variable:String? //evaluates to nil
if variable != nil {
 print("Not Nil")
}
else{
 print("Nil")
}
```
**Output  2 :**
```
Nil
```
#### Using Forced Unwrapping Operator `!` :
Refer Example 1 for **Forced Unwrapping Operator** usage. If the `Optional` having `nil` value is tried to be unwrapped, an error `Unexpectedly found nil while unwrapping an Optional value` will be thrown at Runtime.

#### Using Automatic Unwrapping /Implicitly Unwrapped Optionals:
Declaring Optionals with `!` instead of `?` will make the variable to be automatically unwrapped during usage.

**Example 3 :**
```swift
var nillableString: String! = "Hello"
print(nillableString)
print(type(of: nillableString))
let finalString: String = nillableString  // no need of using ! here
print(finalString)
print(type(of: finalString))
```
**Output 3 :**
```
Optional("Hello")
Optional<String>
Hello
String
```
Small

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/varconst.html">&larr; Variables, Literals and Constants in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/basicio.html">Basic I/O in Swift &rarr;</a>
</span>
