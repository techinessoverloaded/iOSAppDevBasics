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


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/basicio.html">&larr; Basic I/O in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
