**Published by Arunprasadh C on 02 May 2022** • *Last Updated on 04 May 2022*

## Operators in Swift
Operators are the special symbols that perform operations on variables and values. Swift Operators can be divided into various categories :
1. Arithmetic Operators
2. Assignment Operators
3. Comparison Operators
4. Logical Operators
5. Bitwise Operators
6. Miscellaneous Operators

### Arithmetic Operators
Arithmetic operators are used to perform mathematical operations like addition, subtraction, multiplication, etc. Swift supports the following Arithmetic Operators:

| Operator | Operation | Example |
| :---: | :---: | :---: |
| `+` | Addition | `5 + 2 = 7` |
| `-` | Subtraction | `5 - 2 = 3` |
| `*` | Multiplication | `5 * 2 = 10` |
| `/` | Division | `4 / 2 = 2` |
| `%` | Modulo | `5 % 2 = 1` |

**Example :**
```swift
var a = 99
var b = 999
let c:Float
c = Float(a + b)
print("\(a).0 + \(b).0 = \(c)")
```

**Output :**
```
99.0 + 999.0 = 1098.0
```

### Assignment Operators
Assignment operators are used to assign values to variables. Swift supports the following Assignment Operators:

| Operator | Name | Example |
| :---: | :---: | :---: |
| `=` | Assignment Operator | `a = 5` |
| `+=` | Addition Assignment | `a += 2 // a = a + 2 = 7` |
| `-=` | Subtraction Assignment | `a -= 2 // a = a - 2 = 5` |
| `*=` | Multiplication Assignment | `a *= 2 // a = a * 2 = 10` |
| `/=` | Division Assignment | `a /= 2 // a = a * 2 = 5` |
| `%=` | Remainder Assignment | `a %= 2 // a = a % 2 = 1` |

**Example :**
```swift
var a = 99
var b = 999
let oldB = b
b %= a
print("\(oldB) %= \(a) = \(b)")
```

**Output :**
```
999 %= 99 = 9
```
Note that for the arithmetic assignment combo operators, the operands should be mutable variables declared with `var` keyword.

### Comparison Operators
Comparison operators compare two operands and return either boolean `true` or `false`. The following Comparison operators are supported in Swift:

| Operator | Description | Example |
| :---: | :---: | :---: |
| `==` | Is Equal To | `5 == 2 //false` |
| `!=` | Is Not Equal To | `5 != 2 //true` |
| `>` | Greater Than | `5 > 2 //true` |
| `<` | Less Than | `5 < 2 //false` |
| `>=` | Greater Than or Equal To | `2 >= 2 //true` |
| `<=` | Less Than or Equal To | `5 <= 2 //false` |

**Example :**
```swift
var greeting1 = "Good morning"
var greeting2 = "Good afternoon"
var hour = 13
if hour > 12
{
    print(greeting2)
}
else
{
    print(greeting1)
}
```

**Output :**
```
Good afternoon
```

### Logical Operators
Logical operators are used to check whether an expression is `true` or `false`. They are used in decision-making. Swift supports the following Logical Operators:

| Operator | Description | Example |
| :---: | :---: | :---: |
| `&&` | Logical AND | `5 == 2 //false` |
| `||` | Logical OR | `5 != 2 //true` |
| `!` | Logical NOT | `5 > 2 //true` |

**Example :**
```swift
var age: UInt = 16
if age >= 18 && age <= 100
{
    print("You are eligible to vote !")
}
else
{
    print("You are not eligible to vote !")
}
```

**Output :**
```
You are not eligible to vote !
```

### Bitwise Operators
Bitwise operators perform operations on integer data at the individual bit-level. These operations include testing, setting, or shifting the actual bits. The following Bitwise operators are supported in Swift:

| Operator | Description | Example |
| :---: | :---: | :---: |
| `&` | Bitwise AND | `5 & 2 //0` |
| `|` | Bitwise OR | `5 | 2 //7` |
| `^` | Bitwise XOR | `5 ^ 2 //7` |
| `~` | Bitwise NOT | `~5 //-6` |
| `<<` | Bitwise Left Shift | `5 << 2 //20` |
| `>>` | Bitwise Right Shift | `5 >> 2 //1` |

**Example :**
```swift
print("Quotient of dividing 5 by 4 is : \(5 >> 2)") // equivalent to 5 / 2^2
//101
//0 -> 101 -> 1
//0 -> 010 -> 0
//001 = 1
print("Product of multiplying 5 by 4 is : \(5 << 2)") // equivalent to 5 * 2^2
//101
//101 <- 0
//1010 <- 0
//10100 = 20
```

**Output :**
```
Quotient of dividing 5 by 4 is : 1
Product of multiplying 5 by 4 is : 20
```

A combo of assignment and bitwise operators can also be used (like `<<=`).

### Miscellaneous Operators
These are the other operators available in Swift:

#### Ternary Operator
The ternary operator represented by `? :` is used to evaluate a condition and execute some code based on the condition. It is like a shorthand for `if`-`else` block.

**Syntax :**
```swift
condition ? expression1 : expression2
```

**Example :**
```swift
var marks = 90
let result = (marks > 45) ? "Pass" : "Fail"
print("Result : \(result)")
```

**Output :**
```
Result : Pass
```
#### Nil Coalescing Operator `??` and Forced Unwrapping Operator `!`
We have seen about these operators in [Optionals and Tuples](https://techinessoverloaded.github.io/iOSAppDevBasics/optuples.html).

#### Range Operators
Swift allows to generate Numeric ranges using Range Operators. When floating point numbers are used, the range can't be iterated through as there can be infinite possible numbers. Similarly, for character ranges, they can't be iterated as they don't conform to the `Strideable` Protocol. But, other methods can be used. When integers are used, they can be iterated through using a `for`-`in` loop. There are three kinds of Ranges:

##### Closed Range
When the `...` operator is used, a range is generated between `lowerBound` and `upperBound` with both the bounds inclusive.

**Example :**
```swift
let intRange = 1...10
for x in intRange
{
    print(x, terminator: ", ")
}
```

**Output :**
```
1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
```

##### Half-Open Range
When the `..<` operator is used, a range is generated between `lowerBound` and `upperBound`, inclusive of the `lowerBound` and exclusive of the `upperBound`.

**Example :**
```swift
let floatRange = 4.0..<9.0
print("Is 9.0 present in \(floatRange) ? \(floatRange.contains(9.0))")
```

**Output :**
```
Is 9.0 present in 4.0..<9.0 ? false
```

##### One-sided Range
We can create a one-sided range using either `...` or `..<` operator. A one-sided range contains range from one bound upto infinity in one direction.

**Example :**
```swift
let minusInfinity = ..<10
let plusInfinity = 1...
print(minusInfinity.contains(-999999))
print(plusInfinity.contains(65535))
```

**Output :**
```
true
true
```
Now that we have seen about Operators in Swift, let's move on to see about Decision-making Constructs in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/basicio.html">&larr; Basic I/O in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/decision.html">Decision-making Constructs &rarr;</a>
</span>
