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

### Impact of Access Levels on Protocols
If you want to assign an explicit access level to a protocol type, do so at the point that you define the protocol. This enables you to create protocols that can only be adopted within a certain access context.

The access level of each requirement within a protocol definition is automatically set to the same access level as the protocol. You can’t set a protocol requirement to a different access level than the protocol it supports. This ensures that all of the protocol’s requirements will be visible on any type that adopts the protocol.

**NOTE:** If you define a public protocol, the protocol’s requirements require a public access level for those requirements when they’re implemented. This behavior is different from other types, where a public type definition implies an access level of internal for the type’s members.

If you define a new protocol that inherits from an existing protocol, the new protocol can have at most the same access level as the protocol it inherits from. For example, you can’t write a public protocol that inherits from an internal protocol.

A type can conform to a protocol with a lower access level than the type itself. For example, you can define a public type that can be used in other modules, but whose conformance to an internal protocol can only be used within the internal protocol’s defining module.

The context in which a type conforms to a particular protocol is the minimum of the type’s access level and the protocol’s access level. For example, if a type is public, but a protocol it conforms to is internal, the type’s conformance to that protocol is also internal.

When you write or extend a type to conform to a protocol, you must ensure that the type’s implementation of each protocol requirement has at least the same access level as the type’s conformance to that protocol. For example, if a public type conforms to an internal protocol, the type’s implementation of each protocol requirement must be at least internal.

**NOTE:** In Swift, as in Objective-C, protocol conformance is global—it isn’t possible for a type to conform to a protocol in two different ways within the same program.

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

### Mutating Method Requirements
If you define a protocol instance method requirement that’s intended to mutate instances of any type that adopts the protocol, mark the method with the `mutating` keyword as part of the protocol’s definition. This enables structures and enumerations to adopt the protocol and satisfy that method requirement. It is important to note that, if you mark a protocol instance method requirement as `mutating`, you don’t need to write the `mutating` keyword when writing an implementation of that method for a class. The `mutating` keyword is only used by structures and enumerations.

**Example 3:**
```swift
protocol Togglable
{
    mutating func toggle()
}

enum Switch: Togglable
{
    case on, off
    
    mutating func toggle()
    {
        switch self
        {
        case .on:
            self = .off
        case .off:
            self = .on
        }
    }
}

var fanSwitch = Switch.off
print("State of Fan: \(fanSwitch)")
print("Turning on Fan...")
fanSwitch.toggle()
print("State of Fan: \(fanSwitch)")
```
**Output 3:**
```
State of Fan: off
Turning on Fan...
State of Fan: on
```

### Initializer Requirements
Protocols can require specific initializers to be implemented by conforming types. You write these initializers as part of the protocol’s definition in exactly the same way as for normal initializers, but without curly braces or an initializer body.

#### Class Implementations of Protocol Initializer Requirements
You can implement a protocol initializer requirement on a conforming class as either a designated initializer or a convenience initializer. In both cases, you must mark the initializer implementation with the `required` modifier. The use of the `required` modifier ensures that you provide an explicit or inherited implementation of the initializer requirement on all subclasses of the conforming class, such that they also conform to the protocol. If a subclass overrides a designated initializer from a superclass, and also implements a matching initializer requirement from a protocol, mark the initializer implementation with both the `required` and `override` modifiers.

#### Failable Initializer Requirements
Protocols can define failable initializer requirements for conforming types. A failable initializer requirement can be satisfied by a failable or nonfailable initializer on a conforming type. A nonfailable initializer requirement can be satisfied by a nonfailable initializer or an implicitly unwrapped failable initializer.

**Example 4:**
```swift
protocol AnonymousPerson
{
    var name: String { get set }
    var age: UInt { get set }
    init(age: UInt)
}

struct Person: AnonymousPerson
{
    var name: String
    var age: UInt
    
    init(age: UInt)
    {
        name = "Anonymous"
        self.age = age
    }
    
    init(name: String, age: UInt)
    {
        self.name = name
        self.age = age
    }
}

let unnamedPerson = Person(age: 21)
print(unnamedPerson)
```
**Output 4:**
```
Person(name: "Anonymous", age: 21)
```

### Protocols as Types
Protocols don’t actually implement any functionality themselves. Nonetheless, you can use protocols as a fully fledged types in your code. Using a protocol as a type is sometimes called an existential type, which comes from the phrase “there exists a type T such that T conforms to the protocol”.

You can use a protocol in many places where other types are allowed, including:

- As a parameter type or return type in a function, method, or initializer.
- As the type of a constant, variable, or property.
- As the type of items in an array, dictionary, or other container.

When Protocol is used as a Type, only the members of Protocol can be accessed from the instance. To access all the members, downcasting to the actual Type must be done.

**Example 5:**
```swift
protocol Identifiable
{
    var id: UInt { get }
    mutating func regenerateId()
}

struct User: Identifiable, CustomStringConvertible
{
    private var _id: UInt
    var name: String
    var age: Int
    var description: String
    {
        "User(id: \(_id), name: \(name), age: \(age))"
    }
    
    var id: UInt
    {
        _id
    }
    
    mutating func regenerateId()
    {
        _id = UInt.random(in: 1...100)
    }
    
    init(name: String, age: Int)
    {
        _id = UInt.random(in: 1...100)
        self.name = name
        self.age = age
    }
}

struct Subject: Identifiable, CustomStringConvertible
{
    private var _id: UInt
    var name: String
    var department: String
    var description: String
    {
        "Subject(id: \(_id), name: \(name), department: \(department))"
    }
    
    var id: UInt
    {
        _id
    }
    
    mutating func regenerateId()
    {
        _id = UInt.random(in: 1...100)
    }
    
    init(name: String, department: String)
    {
        _id = UInt.random(in: 1...100)
        self.name = name
        self.department = department
    }
}

var dsa: Identifiable = Subject(name: "Data Structures and Algorithms", department: "CSE")
var student: Identifiable = User(name: "Kris", age: 21)
print("ID of DSA Subject: \(dsa.id)")
print("Regenerating ID of DSA...")
dsa.regenerateId()
print("ID of DSA Subject: \(dsa.id)")
print("Department of DSA is: \((dsa as! Subject).department)") // Downcasting to access department
print(dsa)
print(student)
```
**Output 5:**
```
ID of DSA Subject: 62
Regenerating ID of DSA...
ID of DSA Subject: 29
Department of DSA is: CSE
Subject(id: 29, name: Data Structures and Algorithms, department: CSE)
User(id: 55, name: Kris, age: 21)
```

### Adding Protocol Conformance with an Extension
You can extend an existing type to adopt and conform to a new protocol, even if you don’t have access to the source code for the existing type. Extensions can add new properties, methods, and subscripts to an existing type, and are therefore able to add any requirements that a protocol may demand.

**NOTE:** Existing instances of a type automatically adopt and conform to a protocol when that conformance is added to the instance’s type in an extension.

**Example 6:**
```swift
protocol StringRepresentation
{
    var asString: String { get }
}

class Point
{
    var x: Int, y: Int
    
    init(_ x: Int, _ y: Int)
    {
        self.x = x
        self.y = y
    }
}

extension Point: StringRepresentation
{
    var asString: String
    {
        "Point(x = \(x), y = \(y))"
    }
}

let point = Point(8, 11)
print(point.asString)
```
**Output 6:**
```
Point(x = 8, y = 11)
```

### Conditionally Conforming to a Protocol
A generic type may be able to satisfy the requirements of a protocol only under certain conditions, such as when the type’s generic parameter conforms to the protocol. You can make a generic type conditionally conform to a protocol by listing constraints when extending the type. Write these constraints after the name of the protocol you’re adopting by writing a generic `where` clause (It will be discussed in detail in [Generics](https://techinessoverloaded.github.io/iOSAppDevBasics/generics.html)).

**Example 7:**
```swift
protocol StringRepresentation
{
    var asString: String { get }
}

class Point
{
    var x: Int, y: Int

    init(_ x: Int, _ y: Int)
    {
        self.x = x
        self.y = y
    }
}

extension Point: StringRepresentation
{
    var asString: String
    {
        "Point(x = \(x), y = \(y))"
    }
}

extension Array: StringRepresentation where Element: StringRepresentation
{
    var asString: String
    {
        let itemsAsString = self.map { $0.asString }
        return "[" + itemsAsString.joined(separator: ", ") + "]"
    }
}

let points = [Point(2, 4), Point(6, 7)]
print(points.asString)
```
**Output 7:**
```
[Point(x = 2, y = 4), Point(x = 6, y = 7)]
```

### Declaring Protocol Adoption with an Extension
If a type already conforms to all of the requirements of a protocol, but hasn’t yet stated that it adopts that protocol, you can make it adopt the protocol with an empty extension.

**Example 8:**
```swift
protocol StringRepresentation
{
    var asString: String { get }
}

struct Person
{
    var name: String
    var age: UInt
    var asString: String
    {
        "Person(name = \(name), age = \(age))"
    }
}

extension Person: StringRepresentation{}

print(Person(name: "Kris", age: 21) is StringRepresentation)
```
**Output 8:**
```
true
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/enums.html">&larr; Enumerations</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/generics.html">Generics &rarr;</a>
</span>
