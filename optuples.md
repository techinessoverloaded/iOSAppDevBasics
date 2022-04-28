**Published by Arunprasadh C on 25 Apr 2022** • *Last Updated on 28 Apr 2022*

## Tuples and Optionals in Swift

### Tuples
Tuples are used to group multiple values in a single compound value. The values can be of different Data Types. The basic syntax of `Tuple` is as follows:
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

I have used **String Interpolation** in the above example. It will be covered in the Basic I/O Functions Page.<br>
The elements of a `Tuple` can also be given Labels. When such Labels are used, the elements can be accessed with the Labels instead of Index Values. And even a combination of Index Values and Labels can be used.

**Example :**
```swift
var tup1 = (a: (c: 4,d: 5),"Hello")
print(tup1.a.d,tup1.1,separator: ", ")
```

**Output :**
```
5, Hello
```

There may be some situations where we might want to prefer using `Tuple` over `struct` or `class` to keep the code simpler. But, if we want to reuse the `Tuple` again and again, declaring a `Tuple` again and again might not be the best solution. Instead, we can use `typealias` for declaring the `Tuple` structure once and then reuse the structure like a data type anywhere. Consider the situation where we want to use `Tuple` for storing the attributes of a Circle. We can use `typealias` in the following way :

**Example :**
```swift
typealias Circle = (center: (x: Double, y: Double), radius: Double)
let unitCircle: Circle = Circle(center: (0.0, 0.0), radius: 1.0)
var circleTwo: Circle = Circle((4.5, 3.5), 10.5)
print(type(of: circleTwo))
print(unitCircle.center == circleTwo.center)
```
**Output :**
```
(center: (x: Double, y: Double), radius: Double)
false
```

### Optionals
`Optional` is a Data Type which is used in situations where either there can be a Value or there can be no Value at all. When there is no value, it is represented as `nil` (Just like `NULL` in **C/C++** or like `null` in **Java**. But `nil` is not a Pointer as in other languages). `nil` can be assigned only to variables/constants of `Optional` type. 

#### Why there are no explicit pointers in Swift ?
There are no explicit pointers in Swift (just like other modern languages). The reasons are quite obvious :
- **Pointers can violate Type Safety :** For example, in C language, the `malloc()` function returns a `void*` pointer which does not refer to any specific Data Type pointer. The value stored at the address can an `int` or `char` or any other Data Type. This causes ambiguity in the type of value stored at the location. It can lead to loss of data when incompatible typecasting is done.

- **Pointers can violate Memory Safety :** Again consider the `malloc()` function in C language. It returns a `void*` pointer after allocating memory blocks dynamically. Suppose, if `free(pointer)` function is not called after the use of the pointer is over, the memory block reserved by `malloc()` remains reserved throughout the execution of the program, thus depriving other programs/threads/variables of the access to that memory block, thus causing a memory leak.

- **Pointers can be potentially unsafe to use :** When wrong addresses are referenced via pointers, it may even lead to accessing of the global variables of the OS and can lead to system crashes.

But, Swift does provide some ways to access pointers (which is known as unsafe Swift) like `UnsafeRawPointer` class which should be used with caution.

General Syntax of declaring an `Optional` variable is as follows:

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
#### Using Optional Binding
**Optional Binding** is similar to using an `if`-`else` block. The only difference is that if the `Optional` value is not `nil`, the unwrapped value is assigned to a new constant and further operations are performed on the constant. It can be done using `if`-`let` block :
**Example 4 :**
```swift
var sample:String? = "Hello"
if let unwrappedSample = sample
{
print("Sample is \(unwrappedSample)")
}
```
**Output 4 :**
```
Sample is Hello
```

#### Using `nil` Coalescing Operator `??`
The `nil` Coalescing Operator `??` is like a shorthand for `if`-`else` Block. If the Optional has a value, that value will be used. Else, a provided Default Value will be used.
**Example 5 :**
```swift
var str1: String?
var str2: String = str1 ?? "Default"
print(str2)
str1 = "Provided"
str2 = str1 ?? "Default"
print(str2)
```
**Output 5 :**
```
Default
Provided
```
#### Using Optional Chaining
This method will be discussed after seeing about Classes in Swift.

Now that we have seen about Optionals and Tuples in Swift, we can see about Variables, Literals and Constants in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/charstrings.html">&larr; Characters and Strings in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/varconst.html">Variables, Literals and Constants &rarr;</a>
</span>
