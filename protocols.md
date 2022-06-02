**Published by Arunprasadh C on 02 June 2022** • *Last Updated on 02 June 2022*

## Protocols
A Protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality (Known as Interfaces in other languages). It is used to achieve abstraction. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to **conform** to that protocol.

In addition to specifying requirements that conforming types must implement, you can extend a protocol to implement some of these requirements or to implement additional functionality that conforming types can take advantage of. Protocol declaration is denoted by the `protocol` Keyword.

**Syntax:**
```swift
protocol ProtocolName
{
   //Methods and Properties
}
```

Custom types state that they adopt a particular protocol by placing the protocol’s name after the type’s name, separated by a colon, as part of their definition. Multiple protocols can be listed, and are separated by commas `,`. We have seen some examples of Protocol Conformance already in [Structures](https://techinessoverloaded.github.io/iOSAppDevBasics/structs.html), [Classes](https://techinessoverloaded.github.io/iOSAppDevBasics/classes.html) and [Enumerations](https://techinessoverloaded.github.io/iOSAppDevBasics/enums.html), where we had conformed to Protocols like `CustomStringConvertible`, `Equatable` and `CaseIterable` which are available in the Swift Standard Library. In the case of classes, if a class has a super class as its parent, the name of the super class is mentioned before the protocols to which the class conforms to.

### Property Requirements
A protocol can require any conforming type to provide an instance property or type property with a particular name and type. The protocol doesn’t specify whether the property should be a stored property or a computed property—it only specifies the required property name and type. The protocol also specifies whether each property must be gettable or gettable and settable.

If a protocol requires a property to be gettable and settable, that property requirement can’t be fulfilled by a constant stored property or a read-only computed property. If the protocol only requires a property to be gettable, the requirement can be satisfied by any kind of property, and it’s valid for the property to be also settable if this is useful for your own code.

Property requirements are always declared as variable properties, prefixed with the var keyword. Gettable and settable properties are indicated by writing `{ get set }` after their type declaration, and gettable properties are indicated by writing `{ get }`.

Always prefix type property requirements with the `static` keyword when you define them in a protocol. This rule pertains even though type property requirements can be prefixed with the `class` or `static` keyword when implemented by a class.

**Example 1:**
```swift
protocol FullyNamed
{
    var fullName: String { get }
}

struct Person: FullyNamed
{
    var firstName: String
    var lastName: String
    var fullName: String
    {
        "\(firstName) \(lastName)"
    }
}

let person = Person(firstName: "Kris", lastName: "Sri")
print(person.fullName)
```
**Output 1:**
```
Kris Sri
```

### Method Requirements
Protocols can require specific instance methods and type methods to be implemented by conforming types. These methods are written as part of the protocol’s definition in exactly the same way as for normal instance and type methods, but without curly braces or a method body. Variadic parameters are allowed, subject to the same rules as for normal methods. Default values, however, can’t be specified for method parameters within a protocol’s definition.

As with type property requirements, you always prefix type method requirements with the static keyword when they’re defined in a protocol. This is true even though type method requirements are prefixed with the `class` or `static` keyword when implemented by a class.

**Example 2:**
```swift
protocol EvenNumberGenerator
{
    static func randomEven() -> (number: Int, tries: Int)
}

extension Int: EvenNumberGenerator
{
    static func randomEven() -> (number: Int, tries: Int)
    {
        var result = Int.random(in: 1...100)
        var count = 1
        while !result.isMultiple(of: 2)
        {
            count += 1
            result = Int.random(in: 1...100)
        }
        return (result,count)
    }
}
let result = Int.randomEven()
print("Got even number \(result.number) after \(result.tries) tries.")
```
**Output 2:**
```
Got even number 20 after 3 tries.
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/enums.html">&larr; Enumerations</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
