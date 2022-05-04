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

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/basicio.html">&larr; Basic I/O in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
