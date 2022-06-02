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

### Adopting a Protocol Using a Synthesized Implementation
Swift can automatically provide the protocol conformance for `Equatable`, `Hashable`, and `Comparable` in many simple cases. Using this synthesized implementation means you don’t have to write repetitive boilerplate code to implement the protocol requirements yourself.

Swift provides a synthesized implementation of `Equatable` for the following kinds of custom types:
- Structures that have only stored properties that conform to the `Equatable` protocol.
- Enumerations that have only associated types that conform to the `Equatable` protocol.
- Enumerations that have no associated types.

To receive a synthesized implementation of `==`, declare conformance to `Equatable` in the file that contains the original declaration, without implementing an `==` operator yourself. The `Equatable` protocol provides a default implementation of `!=`.

Swift provides a synthesized implementation of `Hashable` for the following kinds of custom types:
- Structures that have only stored properties that conform to the `Hashable` protocol.
- Enumerations that have only associated types that conform to the `Hashable` protocol.
- Enumerations that have no associated types.

To receive a synthesized implementation of `hash(into:)`, declare conformance to `Hashable` in the file that contains the original declaration, without implementing a `hash(into:)` method yourself.

Swift provides a synthesized implementation of `Comparable` for enumerations that don’t have a raw value. If the enumeration has associated types, they must all conform to the `Comparable` protocol. To receive a synthesized implementation of `<`, declare conformance to `Comparable` in the file that contains the original enumeration declaration, without implementing a `<` operator yourself. The `Comparable` protocol’s default implementation of `<=`, `>`, and `>=` provides the remaining comparison operators.

### Protocol Inheritance
A protocol can inherit one or more other protocols and can add further requirements on top of the requirements it inherits. The syntax for protocol inheritance is similar to the syntax for class inheritance, but with the option to list multiple inherited protocols, separated by commas.

An example can be found in the Swift Standard Library, where the `Hashable` Protocol inherits from the `Equatable` Protocol. Only by means of Protocols, Multiple Inheritance can be implemented.

### Class-Only Protocols
You can limit protocol adoption to class types (and not structures or enumerations) by adding the `AnyObject` protocol to a protocol’s inheritance list.
Use a class-only protocol when the behavior defined by that protocol’s requirements assumes or requires that a conforming type has reference semantics rather than value semantics.

**Example 9:**
```swift
protocol AbstractList: AnyObject
{
    func addNewNode(_ newData: Int)
    func addMultipleNodes(_ newData: Int...)
}

class Node: CustomStringConvertible
{
    var next: Node?
    var data: Int
    var description: String
    {
        var text = ""
        if let n = next
        {
            text = n.description
        }
        else
        {
            text = "nil"
        }
        return "\(data) -> \(text)"
    }

    init(data: Int, next: Node? = nil)
    {
        self.data = data
        self.next = next
    }
}

class LinkedList: AbstractList
{
    var root: Node

    init(root: Node)
    {
        self.root = root
    }

    func addNewNode(_ newData: Int)
    {
        var head = root
        let newNode = Node(data: newData)
        while head.next != nil
        {
            head = head.next!
        }
        head.next = newNode
    }

    func addMultipleNodes(_ newData: Int...)
    {
        for x in newData
        {
            addNewNode(x)
        }
    }

    func printList()
    {
        print(root)
    }
}

var list = LinkedList(root: Node(data: 9))
list.addMultipleNodes(8, 7, 6, 5, 4, 3, 2, 1)
list.printList()
```
**Output 9:**
```
9 -> 8 -> 7 -> 6 -> 5 -> 4 -> 3 -> 2 -> 1 -> nil
```

### Protocol Composition
It can be useful to require a type to conform to multiple protocols at the same time. You can combine multiple protocols into a single requirement with a protocol composition. Protocol compositions behave as if you defined a temporary local protocol that has the combined requirements of all protocols in the composition. Protocol compositions don’t define any new protocol types.

Protocol compositions have the form `SomeProtocol & AnotherProtocol`. You can list as many protocols as you need, separating them with ampersands (`&`). In addition to its list of protocols, a protocol composition can also contain one class type, which you can use to specify a required superclass.

**Example 10:**
```swift
protocol Named
{
    var name: String { get }
}

protocol Aged
{
    var age: Int { get }
}

struct Person: Named, Aged
{
    var name: String
    var age: Int
}

func wishHappyBirthday(to celebrator: Named & Aged)
{
    print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
}

let birthdayPerson = Person(name: "Ian Malcolm", age: 21)
wishHappyBirthday(to: birthdayPerson)
```
**Output 10:**
```
Happy birthday, Ian Malcolm, you're 21!
```

### Checking for Protocol Conformance
You can use the `is` and `as` operators described in [Type Casting](https://techinessoverloaded.github.io/iOSAppDevBasics/typecasting.html) to check for protocol conformance, and to cast to a specific protocol. Checking for and casting to a protocol follows exactly the same syntax as checking for and casting to a type.

### Optional Protocol Requirements
You can define optional requirements for protocols. These requirements don’t have to be implemented by types that conform to the protocol. Optional requirements are prefixed by the optional modifier as part of the protocol’s definition. Optional requirements are available so that you can write code that interoperates with Objective-C. Both the protocol and the optional requirement must be marked with the `@objc` attribute. Note that `@objc` protocols can be adopted only by classes that inherit from Objective-C classes or other `@objc` classes. They can’t be adopted by structures or enumerations.

When you use a method or property in an optional requirement, its type automatically becomes an optional. For example, a method of type `(Int) -> String` becomes `((Int) -> String)?`. Note that the entire function type is wrapped in the optional, not the method’s return value.

An optional protocol requirement can be called with optional chaining, to account for the possibility that the requirement was not implemented by a type that conforms to the protocol. You check for an implementation of an optional method by writing a question mark after the name of the method when it’s called, such as `someOptionalMethod?(someArgument)`.

**Example 11:**
```swift
@objc protocol CounterDataSource 
{
    @objc optional func increment(forCount count: Int) -> Int
    @objc optional var fixedIncrement: Int { get }
}
```

### Protocol Extensions
Protocols can be extended to provide method, initializer, subscript, and computed property implementations to conforming types. This allows you to define behavior on protocols themselves, rather than in each type’s individual conformance or in a global function. By creating an extension on the protocol, all conforming types automatically gain this method implementation without any additional modification. Protocol extensions can add implementations to conforming types but can’t make a protocol extend or inherit from another protocol. Protocol inheritance is always specified in the protocol declaration itself.

#### Providing Default Implementations
You can use protocol extensions to provide a default implementation to any method or computed property requirement of that protocol. If a conforming type provides its own implementation of a required method or property, that implementation will be used instead of the one provided by the extension. Protocol requirements with default implementations provided by extensions are distinct from optional protocol requirements. Although conforming types don’t have to provide their own implementation of either, requirements with default implementations can be called without optional chaining.

**Example 12:**
```swift
protocol StringRepresentation: CustomStringConvertible
{
    var asString: String { get }
}

extension StringRepresentation
{
    var asString: String
    {
        return description
    }
}

class Point: StringRepresentation
{
    var x: Int, y: Int
    var description: String
    {
        "Point(x: \(x), y: \(y))"
    }
    
    init(_ x: Int, _ y: Int)
    {
        self.x = x
        self.y = y
    }
}
print(Point(8, 10).asString)
```
**Output 12:**
```
Point(x: 8, y: 10)
```

#### Adding Constraints to Protocol Extensions
When you define a protocol extension, you can specify constraints that conforming types must satisfy before the methods and properties of the extension are available. You write these constraints after the name of the protocol you’re extending by writing a generic `where` clause. For more about generic `where` clauses, see [Generics](https://techinessoverloaded.github.io/iOSAppDevBasics/generics.html).

**Example 13:**
```swift
extension Collection where Element: Equatable
{
    func allEqual() -> Bool
    {
        for element in self
        {
            if element != self.first
            {
                return false
            }
        }
        return true
    }
}
let equalNumbers = [100, 100, 100, 100, 100]
print(equalNumbers.allEqual())
```
**Output 13:**
```
true
```

Now that we have seen about Protocols in Swift, let's move on to see about Generics in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/extensions.html">&larr; Extensions</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/generics.html">Generics &rarr;</a>
</span>
