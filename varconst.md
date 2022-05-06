**Published by Arunprasadh C on 21 Apr 2022** • *Last Updated on 06 May 2022*

## Variables, Literals and Constants in Swift
### Literals
Literals are used to represent data values like Int or any other Data Type value in the Source Code. 

**Example :**
```swift
45 // Int Literal
"Hello World" // String Literal
3.14 // Floating-point Literal
```
We can assign values to Variables and Constants by means if Literals.

### Variables
In the previous Topic Pages, you would have seen the word "Variable" in many places. In fact, it is quite hard to write a program without using variables. Why is it so ? It is so because, a Variable as its name suggests, is used for storing a named variable value (value that can be changed). In Swift, variables can be declared by using `var` Keyword. 

**Example :**
```swift
var a = 45 // Statement 1
var b: String = "Hello" // Statement 2
```
As we saw in the Previous Topic, Swift can infer the Data Type of variable using the assigned Literal. This kind of declaration is used in Statement 1 above. On the other hand, in Statement 2, the Data Type of the Variable is explicitly specified in the Declaration. This kind of explicit Type Specification is called as **Type Annotation** in Swift. The general syntax of **Type Annotation** is as shown below:
```swift
var variableName:<data type> = <optional initial value>
```
**Type Annotation** is not compulsory in Swift as Data Types are inferred automatically. Usually, **Type Annotations** are used for enhancing the readability of the code. **Type Annotations** also allow the variables to be declared without any initial value. These variables can be assigned with value in the later part of the code.

**Example :**
```swift
var word:String
// Some statements
word = "Hello"
```
#### Defining Multiple Variables on a single line
Multiple variables can be declared/defined with/without initialization in a single line provided that the variables are annotated with their types.

**Syntax :**
```swift
var v1:DataType1 = optInitialValue1, v2:DataType2 = optInitialValue1, v3:DataType3 = optInitialValue1, ...
```
**Example :**
```swift
var name: String = "Kris", age: Int = 22, native: String = "Chennai"
print("\(name), who is \(age) years old, is from \(native).")
```

**Output :**
```
Kris, who is 22 years old, is from Chennai.
```

#### Initializing/Assigning values to Multiple Variables using Tuple Syntax
Multiple variables can be reassigned to values at once using the Tuple Syntax:

**Syntax :**
```swift
(v1, v2, v3, ...) = (value1, value2, value3, ...)
```
**Example :**
Consider the variables declared in the previous example
```swift
(name, age, native) = ("Kris", 21, "Madras")
native = "Chennai"
print("\(name) is a \(age) year old boy whose native is \(native)")
```
**Output :**
```
Kris is a 21 year old boy whose native is Chennai
```

### Constants
Constants can be considered as **Immutable** (or **read-only**) Variables. Constants allow the values to be assigned only once. After assignment, the value can't be changed. It can only be accessed.  In Swift, constants can be declared by using `let` Keyword. The general syntax of declaring constants is as follows:
```swift
let constantName = <initial value>
```
**Example :**
```swift
let pi = 3.14 // CONSTANT
var radius = 7 // VARIABLE
var area = pi*radius*radius // VARIABLE
```
As with variables, **Type Annotations** can also be used with Constants in Swift (Simply replace `var` with `let`). Also, like variables, many constants can also be declared at once in a single line and be can initialized using tuple syntax.
<br><br>
The next Topic will cover about Basic I/O Functions in Swift. 

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/datatypes.html">&larr; Data Types available in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/basicio.html">Basic I/O in Swift &rarr;</a>
</span>
