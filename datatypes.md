**Published by Arunprasadh C on 21 Apr 2022** • *Last Updated on 21 Apr 2022*

## Data Types available in Swift
In any programming language, Data Types are quite important as they decide the amount of memory to be allocated to a variable/constant. Swift supports the following **Built-in Data Types** :

- **Int or UInt** − This is used for whole numbers. More specifically, you can use Int32, Int64 to define 32 or 64 bit signed integer, whereas UInt32 or UInt64 to define 32 or 64 bit unsigned integer variables. For example, 42 and -23. On 32-bit Platforms, Int or UInt will automatically refer to Int32 or UInt32 respectively. Similar reference is done on 64-bit Platforms. Even 8-bit and 16-bit versions of Int/Uint types are available.
- **Float** − This is used to represent a 32-bit floating-point number and numbers with smaller decimal points. For example, 3.14159, 0.1, and -273.158.
- **Double** − This is used to represent a 64-bit floating-point number and used when floating-point values must be very large. For example, 3.14159874897578.
- **Bool** − This represents a Boolean value which is either `true` or `false`.
- **String** − This is an ordered collection of characters. For example, "Hello, World!".
- **Character** − This is a single-character string literal. For example, "C".
- **Optional** − This represents a variable that can hold either a value or no value.
- **Tuples** − This is used to group multiple values in single Compound Value.

Now that we have seen the various Data types, let's see how much space is allocated for variables of each Data Type and the range of values that can be represented using each data type:

| Data Type | Space required for a single Variable | Range of values that can be represented |
| :---: | :---: | :---: |
| Int8 | 1 byte | -128 to 127 |
| UInt8 | 1 byte | 0 to 255 |
| Int16 | 2 bytes | -32768 to 32767 |
| UInt16 | 2 bytes | 0 to 65535 |
| Int32 | 4 bytes | -2147483648 to 2147483647 |
| UInt32 | 4 bytes | 0 to 4294967295 |
| Int64 | 8 bytes | -9223372036854775808 to 9223372036854775807 |
| UInt64 | 8 bytes | 0 to 18446744073709551615 |
| Float | 4 bytes | 1.2E-38 to 3.4E+38 (~6 digits) |
| Double | 8 bytes | 2.3E-308 to 1.7E+308 (~15 digits) |
| Bool | 1 byte | Range not Applicable. Can hold either `true` or `false` |

### Type Aliases
Swift allows us to define new names for existing Data Types. These new names can be used as actual Data Type Names. Type Aliases can be defined using the following Syntax:

```swift
typealias newname = type
```

**Example :**
```swift
typealias Number = Int
var x: Number = 56
```

### Type Safety
Swift is a type-safe language, which means that we can't assign a literal or object of a different type to a variable/constant of some other type. For example, the following code will produce the error `error: cannot assign value of type 'String' to type 'Int'` at Compile time :
```swift
var a: Int = 5
a = "Hello"
```

### Type Inference
Swift can infer the Data Type from the type of literal/object assigned to a variable/constant.

**Example :**
```swift
var a = 4 // Inferred as Int
var b = "Hello World" // Inferred as String
```

Now that we have seen about Data types in Swift, we can move on to learn about Variables, Literals and Constants in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/swiftintro.html">&larr; Introduction to Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html">Variables, Literals and Constants &rarr;</a>
</span>
