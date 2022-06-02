**Published by Arunprasadh C on 02 June 2022** • *Last Updated on 02 June 2022*

## Enumerations in Swift
An Enumeration defines a common type for a group of related values and enables you to work with those values in a type-safe way within your code.

If you are familiar with **C**, you will know that **C** enumerations assign related names to a set of integer values. Enumerations in Swift are much more flexible, and don’t have to provide a value for each case of the enumeration. If a value (known as a raw value) is provided for each enumeration case, the value can be a string, a character, or a value of any integer or floating-point type.

Alternatively, enumeration cases can specify associated values of any type to be stored along with each different case value, much as unions or variants do in other languages. You can define a common set of related cases as part of one enumeration, each of which has a different set of values of appropriate types associated with it.

Enumerations are **Value Types** like Structures. Enumerations are declared by using the `enum` keyword in Swift. The `case` keyword is used to declare values inside an Enumeration. Cases can appear on multiple lines or can be defined in a single line, separated by comma `,`.

**NOTE :** Swift enumeration cases don’t have an integer value set by default, unlike languages like C and Objective-C. In the CompassPoint example above, north, south, east and west don’t implicitly equal 0, 1, 2 and 3. Instead, the different enumeration cases are values in their own right, with an explicitly defined type of Enumeration.

Variables/Constants can hold any one case of the Enumeration. The cases can be changed when `var` is used. When the `var`/`let` is type annotated with the Enumeration, the right hand of assignment statement can directly access cases using Dot syntax `.` without the need of specifying the name of Enumeration.

Enumerations can also have Instance methods, Instance `mutating` methods and Type Methods like Structures.

**Example 1:**
```swift
enum Direction
{
    case north, south, east, west
}

var directionToMove = Direction.east
print("Direction to Move: \(directionToMove)")
print(type(of: directionToMove) == Direction.self)
let preferredDirection: Direction = .north
print("Preferred Direction: \(preferredDirection)")
directionToMove = preferredDirection
print("Direction to Move changed to Preferred Direction: \(directionToMove)")
```
**Output 1:**
```
Direction to Move: east
true
Preferred Direction: north
Direction to Move changed to Preferred Direction: north
```

### Matching Enumeration Values with a `switch` statement
Swift allows us to match individual `enum` cases using `switch` statement.

**Example 2:**
```swift
enum Gender
{
    case male, female, other
}

var gender: Gender = .male

switch(gender)
{
case .male:
    print("MALE")
case .female:
    print("FEMALE")
case .other:
    print("OTHER")
}
```
**Output 1:**
```
MALE
```

Note that, there's no default case in the above `switch` statement. However, when you want to skip some `enum` cases from `switch` statement, you can use `default` for the purpose.

### Iterationg over Enumeration Cases
In Swift, an `enum` can conform to the `CaseIterable` Protocol to which adds a property called `allCases`, which is a collection of all the `enum` cases. By means of `allCases`, the cases of `enum` can be iterated.

**Example 3:**
```swift
enum Beverage: CaseIterable
{
    case coffee, tea, juice, milkshake
}

print("\(Beverage.allCases.count) Beverages are available. They are:")

for x in Beverage.allCases
{
    print(x)
}
```
**Output 3:**
```
4 Beverages are available. They are:
coffee
tea
juice
milkshake
```

### Raw Values
In Swift, we can also assign values to each enum case. These are known as **Raw Values** and are accessed from a case via the `rawValue` property. All the cases must have raw values of the same Type. Raw values are set in the `enum` declaration and remain the same and don't change. When `Int` or `String` is used as Raw Value type, Swift can implicitly assign values for each case. When `Int` raw value is used, each case takes the number next to the previous case's `rawValue`. When `String` is used as raw value type, the case names are used as raw value. Raw value types can be denoted by colon `:` operator just like conforming to protocols. An `enum` instance can be initialized using `rawValue`. Raw values can be strings, characters, or any of the integer or floating-point number types. Each raw value must be unique within its enumeration declaration.

**Example 4:**
```swift
enum Planet: Int, CaseIterable
{
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}

print("Planets of Milky Way are:")

for x in Planet.allCases
{
    print("\(x.rawValue) : \(x)")
}

let earth = Planet(rawValue: 3)
print(earth!)
```
**Output 4:**
```
Planets of Milky Way are:
1 : mercury
2 : venus
3 : earth
4 : mars
5 : jupiter
6 : saturn
7 : uranus
8 : neptune
earth
```

### Associated Values
In Swift, we can also attach additional information to an `enum` case. It is known as an Associated Value. It can be of different type for different cases. It is denoted inside parantheses `()` after `case` name. This definition doesn’t provide any actual values. It just defines the type of associated values. The actual values are given during instantiation. While matching cases in `switch` statement, each associated value of a `case` can be marked with `let` or `var` as needed to be used in the code. If all of the associated values for an enumeration case are extracted as constants, or if all are extracted as variables, you can place a single `var` or `let` annotation before the case name, for brevity. Associated values can also be given labels if needed.

**Example 5:**
```swift
enum Transaction
{
    case card(cardNo: String, pin: UInt, amount: Double)
    case upi(upiId: String, upiPin: UInt, amount: Double)
    case cash(amount: Double)
}

func makeTransaction(txn: Transaction)
{
    switch(txn)
    {
    case let .card(cardNo, pin, amount):
        print("\(amount) transacted from Card: \(cardNo) having PIN: \(pin)")
    case let .upi(upiId, upiPin, amount):
        print("\(amount) transacted from account using UPI ID: \(upiId) having PIN: \(upiPin)")
    case let .cash(amount):
        print("\(amount) was transacted as liquid cash")
    }
}

let upiPayment: Transaction = .upi(upiId: "abc@upi", upiPin: 1234, amount: 1000)
makeTransaction(txn: upiPayment)
```
**Output 5:**
```
1000.0 transacted from account using UPI ID: abc@upi having PIN: 1234
```

### Raw Values vs Associated Values
- Raw values are predefined constant values provided to each `enum` value whereas Associated Values are more like variables associated with the `enum` values.
- An `enum` cannot have both raw values and associated values at the same time.
- The raw values of an enum must be of the same data type. But associated values can be of any type.

### Recursive Enumerations
A recursive enumeration is an enumeration that has another instance of the enumeration as the associated value for one or more of the enumeration cases. You indicate that an enumeration case is recursive by writing `indirect` before it, which tells the compiler to insert the necessary layer of indirection.
You can also write `indirect` before the beginning of the enumeration to enable indirection for all of the enumeration’s cases that have an associated value. A recursive function is a straightforward way to work with a recursive `enum`. The following example shows a recursive function which is used to evaluate an Arithmetic Expression:

**Example 6:**
```swift
indirect enum ArithmeticExpression
{
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}

func evaluate(_ expression: ArithmeticExpression) -> Int
{
    switch expression
    {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

let nine = ArithmeticExpression.number(9)
let five = ArithmeticExpression.number(5)
let sum = ArithmeticExpression.addition(five, nine)
let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(81))
print(evaluate(product))
```
**Output 6:**
```
1134
```

Now that we have seen about Enumerations in Swift, let's move on to see about Protocols in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/classes.html">&larr; Classes</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html">Protocols &rarr;</a>
</span>
