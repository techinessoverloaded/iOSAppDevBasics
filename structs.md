**Published by Arunprasadh C on 24 May 2022** • *Last Updated on 27 May 2022*

## Structures in Swift
In Swift, a `struct` (Keyword for Structure) is used to store variables of different data types. It is used to create a new type out of existing types and also define functionalities (through methods) for the new type. Structures are value types in Swift, meaning they are always passed by value in functions and new copies of them are created whenever they are assigned or reassigned. This means that at any point of time, each instance of a `struct` will be stored at an unique location in the memory even when the contained value is same.

**Syntax :**
```swift
struct StructureName 
{
  // structure definition 
}
```

When variables/constants are declared as a part of the `struct` Type, they are known as Properties. Similarly when Functions are declared as a part of the `struct` Type, they are known as Methods. The `struct` is just like a blueprint or template. In order to use the `struct`, we must create an instance of the `struct`. This is where initializers come in. Initializers are the special methods of the `struct` that are used to initialize the properties of the `struct` (Known as Constructors in other languages). The Swift Compiler automatically generates an Initializer taking all the property values as parameters. The Initializer can be called like `StructName(propertyName: value,...)` or `StructName.init(propertyName: value,...)`. The Initializer returns a new Instance of the `struct` which can be assigned to a variable/constant.
The Properties and Methods of the Structure can be accessed via the instance with dot `.` syntax.

**Example 1:**
```swift
struct Student
{
    var rollNo: Int //Property
    var name: String //Property
    
    func printDetails() // Method
    {
        print("Student(rollNo: \(rollNo), name: \"\(name)\")")
    }
}

var student = Student(rollNo: 1, name: "Kris") // Calling default Initializer
student.rollNo = 2
student.printDetails()
print(student)
```
**Output 1:**
```
Student(rollNo: 2, name: "Kris")
Student(rollNo: 2, name: "Kris")
```

You can observe that both `student.printDetails()` and `print(student)` are giving the same output. It is so because, I have tried to mimic the default `String` representation of `struct` in the `student.printDetails()` method. Actually, the Swift `print(_ items:separator:terminator)` function calls the `String(describing:)` Initializer when any instance is passed directly to the `print(_ items:separator:terminator)` 
function to get the textual Represenation of the Object (Just like how `System.out.print()` calls `String.valueOf()` method on the object to be printed in **Java**). Swift compiler generates default textual representation for `struct`. Hence, we are able to get the textual representation. In order to provide a Custom String Representation, the `struct` has to conform to the `CustomStringConvertible` Protocol (Protocols will be discussed in detail later) and provide the value for the `description` property (Similar to overriding `toString()` method in Java).

**Example 1.1:**
```swift
struct Student: CustomStringConvertible
{
    var rollNo: Int //Property
    var name: String //Property
    var description: String
    {
        "Student (rollNo = \(rollNo) ; name = \(name))" // Textual Representation Property
    }
    
    func printDetails() // Method
    {
        print(description)
    }
}

var student = Student(rollNo: 1, name: "Kris")
student.rollNo = 2
student.printDetails()
print(student) // Using Custom Description
```
**Output 1.1:**
```
Student (rollNo = 2 ; name = Kris)
Student (rollNo = 2 ; name = Kris)
```

We can also provide custom Initializers to our `struct` using `init` keyword. We can even create overloaded Initializers and have default values. Initializers can be declared like regular functions except that the `func` keyword, function name and return type are not required and simply `init` keyword is used. The `self` keyword is used to refer to the current instance of the Type (Similar to `self` keyword of **Python** Classes and `this` keyword of **Java/C++** Classes).

**Example 1.2:**
```swift
struct Student: CustomStringConvertible
{
    var rollNo: Int
    var name: String
    var description: String
    {
        "Student \(name) has roll number: \(rollNo)."
    }
    
    init(rollNo: Int, name: String)
    {
        self.rollNo = rollNo
        self.name = name
    }
    
    init(_ name: String)
    {
        rollNo = Int.random(in: 1...100)
        self.name = name
    }
    
}

var student = Student(rollNo: 1, name: "Kris")
var student2 = Student("Jai") // Using alternate Initializer
print(student)
print(student2)
```
**Output 1.2:**
```
Student Kris has roll number: 1.
Student Jai has roll number: 13.
```

You would have noticed in all the examples above that all the properties of the Student Structure are accessible from outside. Does that mean that no access modifiers were used ? It is not so. Let's see about the Access Levels available in Swift.

### Access Levels in Swift
Swift supports four kinds of access levels:

1. `open` and `public` Levels: `open` and `public` are the least restrictive access levels. Both `open` and `public` modifiers enable the specific function or entity to be accessible from any file within the same module or from any file present in the module which imports the defining module. The only difference between `open` and `public` is that `open` is reserved specifically for Classes (About which we will learn later) and allows the Class to be inherited by other Classes outside the defining module in addition to every benefit the `public` Modifier gives. 
2. `internal` Level: It is the default access level when no levels are specified. It enables entities to be used within any source file from their defining module, but not in any source file outside of that module. 
3. `fileprivate` Level: It restricts the use of an entity to its own defining source file. 
4. `private` Level: It restricts the use of an entity to the enclosing declaration, and to extensions of that declaration that are in the same file. 

Access levels in Swift follow an overall guiding principle: **No entity can be defined in terms of another entity that has a lower (more restrictive) access level.** For example:
- A public variable can’t be defined as having an internal, file-private, or private type, because the type might not be available everywhere that the public variable is used.
- A function can’t have a higher access level than its parameter types and return type, because the function could be used in situations where its constituent types are unavailable to the surrounding code.

Access Control is done by placing the Access control keywords like `private` before property and method declaration (And even in Initializer declaration sometimes). When custom Types like `struct`, `class` or `enum` are defined, the Types' Access Levels apply to their Properties and Methods unless they have Explicit Access Levels.

**Example 1.3**
```swift
struct Student: CustomStringConvertible
{
    var rollNo: Int
    var name: String
    private var department: String
    
    var description: String
    {
        "Student \(name) of \(department) Department has roll number: \(rollNo)."
    }
    
    init(rollNo: Int, name: String, department: String)
    {
        self.rollNo = rollNo
        self.name = name
        self.department = department
    }
    
    func getDepartment() -> String
    {
        department
    }
    
}

var student = Student(rollNo: 1, name: "Kris", department: "CSE")
print(student.getDepartment())
```
**Output 1.3:**
```
CSE
```


In the above example, since the property `department` is having `private` access level, trying to access it from the instance will generate a compile-time error. Hence, a function named `getDepartment()` is used to access the value of `department`.

### Computed Properties
But, this is not the right practice in Swift. You can notice that for `description` property, I have used curly braces to indicate the value to be returned. This is because of two reasons: One is that I have used values of other properties inside the string and other is that I am trying to leverage the benefits of Swift Structure Properties. Properties are not like normal variables/constants in Swift. They can have computed Getter and Setter functions (Like **C#** and **Kotlin**). Such properties are known as Computed Properties. Getter is denoted by `get` keyword and Setter is denoted by `set` keyword. The setter provides the updated value through an immutable value called `newValue` (It is the value assigned to the property via dot `.` syntax) and even a custom name can be used for the same. By means of `get` and `set` Access and Mutation of values can be easily done via the dot `.` Syntax. And some computation can also be done before accessing or mutating the property.

**Example 1.4:**
```swift
struct Student: CustomStringConvertible
{
    private let _rollNo: Int // No need of mutation, hence let is used
    private var _name: String
    private var _department: String
    
    var rollNo: Int // Get-Only Property
    {
        get
        {
            _rollNo // Return Type is inferred. So, no need of return keyword
        }
    }
    
    var name: String
    {
        get
        {
            _name
        }
        set
        {
            _name = newValue
        }
    }
    
    var department: String
    {
        get
        {
            _department
        }
        set
        {
            _department = newValue
        }
    }
    
    
    var description: String
    {
        "Student \(_name) of \(_department) Department has roll number: \(_rollNo)."
    }
    
    init(rollNo: Int, name: String, department: String)
    {
        self._rollNo = rollNo
        self._name = name
        self._department = department
    }
    
}

var student = Student(rollNo: 1, name: "Kris", department: "CSE")
print(student.rollNo)
student.name = "Sri"
print(student.name)
print(student.department)
```
**Output 1.4:**
```
1
Sri
CSE
```

You can immediately notice that I have used underscore `_` while naming backing fields as it is the common convention. Also, I have used `let` constant for backing the `rollNo` Property as no mutation is needed. However, while declaring the computed property, I have used `var`. It is so because, Swift doesn't allow `let` constants to have computed getters. And, you should also note that get-only Properties are allowed in Swift. Get-only properties can also be declared without using the `get` keyword. But, it is not possible to define setter only. Swift forces us to define a computed getter when a computed setter is defined. 

#### Property Observers
Swift allows two Property Observers to track the process of Mutation:
- `willSet` is called just before the value is stored and has the `newValue` as a parameter.
- `didSet` is called immediately after the new value is stored and has the `oldValue` as a parameter.

Property Observers can be used only in the following places:
- Stored properties that you define
- Stored properties that you inherit (In Classes)
- Computed properties that you inherit (In Classes)

**Example 1.5:**
```swift
struct Student: CustomStringConvertible
{
    private let _rollNo: Int // No need of mutation, hence let is used
    private var _name: String
    {
        willSet
        {
            print("Going to set the New Name: \(newValue)...")
        }
        didSet
        {
            print("Have set the New Name: \(_name) and disposed off the Old Name: \(oldValue) !")
        }
    }
    private var _department: String
    
    var rollNo: Int // Get-Only Property
    {
        _rollNo
    }
    
    var name: String
    {
        get
        {
            _name
        }
        set
        {
            
            _name = newValue
        }
    }
    
    var department: String
    {
        get
        {
            _department
        }
        set
        {
            _department = newValue
        }
    }
    
    
    var description: String
    {
        "Student \(_name) of \(_department) Department has roll number: \(_rollNo)."
    }
    
    init(rollNo: Int, name: String, department: String)
    {
        self._rollNo = rollNo
        self._name = name
        self._department = department
    }
    
}

var student = Student(rollNo: 1, name: "Kris", department: "CSE")
print(student.rollNo)
student.name = "Sri"
print(student.name)
print(student.department)
```
**Output 1.5:**
```
1
Going to set the New Name: Sri...
Have set the New Name: Sri and disposed off the Old Name: Kris !
Sri
CSE
```

### Structure Behaviour with `let`
When the `let` keyword is used to declare an instance of a `struct` as a Constant, reassigning to another value is prevented (regular behaviour of `let` constants). Additionally, the properties of the `struct` also become immutable and can't be altered thereafter. This is because Structures are Value Types in Swift and each time a mutation is done, a new value is reassigned (If not the full Structure, at least for the mutated property, a new value is created) and reassigning is not possible with `let` Constants. However, when Classes are used as `let` Constants, their properties can be mutated as Classes are Reference Types.

### Mutating Methods
Due to the reasons mentioned above, any Method that attempts to mutate a property inside the Structure must be denoted by the `mutating` keyword and such methods are called Mutating Methods. When such Methods are not denoted by the `mutating` Keyword, the Compiler generates an error saying that `self` is immutable. It can be inferred that the Setters of Structure Properties are internally Mutating Methods.

**Example 1.5:**
```swift
struct Student: CustomStringConvertible
{
    private let _rollNo: Int // No need of mutation, hence let is used
    private var _name: String
    {
        willSet
        {
            print("Going to set the New Name: \(newValue)...")
        }
        didSet
        {
            print("Have set the New Name: \(_name) and disposed off the Old Name: \(oldValue) !")
        }
    }
    private var _department: String
    
    var rollNo: Int // Get-Only Property
    {
        _rollNo
    }
    
    var name: String
    {
        get
        {
            _name
        }
        set
        {
            _name = newValue
        }
    }
    
    var department: String
    {
        get
        {
            _department
        }
        set
        {
            _department = newValue
        }
    }
    
    
    var description: String
    {
        "Student \(_name) of \(_department) Department has roll number: \(_rollNo)."
    }
    
    init(rollNo: Int, name: String, department: String)
    {
        self._rollNo = rollNo
        self._name = name
        self._department = department
    }
    
    mutating func changeNameAndDepartment(newName: String, newDepartment: String)
    {
        _name = newName
        _department = newDepartment
    }
    
}

var student = Student(rollNo: 1, name: "Kris", department: "CSE")
print(student)
student.changeNameAndDepartment(newName: "Shiv", newDepartment: "IT")
print(student)
```
**Output 1.6:**
```
Student Kris of CSE Department has roll number: 1.
Going to set the New Name: Shiv...
Have set the New Name: Shiv and disposed off the Old Name: Kris !
Student Shiv of IT Department has roll number: 1.
```

### Protocol Conformance
Structures can conform to Protocols although they can't take part in Inheritance like Classes can. An example for Protocol Conformance is conforming to the `CustomStringConvertible` Protocol as shown above.

### Equality Logic
Structures can be compared via the Comaprison Operators and Equality can be checked via the Is Equal to Operator `==`. The `==` checks if two values are the same and doesn't care about the memory location of the values.

### Static Properties and Methods
Like Static Variables and Methods in other Languages, Swift too supports Static Properties and Methods for Structures, Classes and Enumeration Types. They are indicated by using `static` keyword before Property or Function declaration. Static Propeerties and Methods are available at the Type level and don't map to any particular instance of the Type. Static Properties and Methods of a Structure can be accessed using dot operator `.` like `StructureName.Property`/`StructureName.Method()`. Static Methods of a Type cannot access non-static Properties/Methods inside them. Static Properties can't be Computed Properties since they don't belong to an Instance. The following example the use of Static Properties and also Static Methods for Operator Overloading:

**Example 2:**
```swift
struct Point
{
    var x: Int
    var y: Int
    static let origin: Self = Self(x: 0, y:0)
    
    static func +(lhs: Self, rhs: Self) -> Self
    {
        Point(x: lhs.x + rhs.x, y: lhs.y + rhs.y)
    }
    
    static func -=(lhs: inout Self, rhs: Self)
    {
        lhs.x -= rhs.x
        lhs.y -= rhs.y
    }
}
let point1 = Point(x: 5, y: 6)
print("Point 1: \(point1)")
let point2 = Point(x: 2, y: 10)
print("Point 2: \(point2)")
var point3 = point1 + point2
print("Sum of Point 1 and Point 2: \(point3)")
let point4 = Point(x: 3, y: 9)
print("Point 4: \(point4)")
point3 -= point4
print("Point 3 after subtracting Point 4 from it: \(point3)")
print("The origin is always located at: \(Point.origin)") // Accessing Static Property
```
**Output 2:**
```
Point 1: Point(x: 5, y: 6)
Point 2: Point(x: 2, y: 10)
Sum of Point 1 and Point 2: Point(x: 7, y: 16)
Point 4: Point(x: 3, y: 9)
Point 3 after subtracting Point 4 from it: Point(x: 4, y: 7)
The origin is always located at: Point(x: 0, y: 0)
```

### Lazy Stored Properties
A Lazy stored property is a property whose initial value isn’t calculated until the first time it’s used. You indicate a Lazy stored property by writing the `lazy` modifier before its declaration. 

**NOTE :** You must always declare a `lazy` property as a variable (with the `var` keyword), because its initial value might not be retrieved until after instance initialization completes. Constant properties must always have a value before initialization completes, and therefore can’t be declared as `lazy`.

Lazy properties are useful when the initial value for a property is dependent on outside factors whose values aren’t known until after an instance’s initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that shouldn’t be performed unless or until it’s needed.

**NOTE :** If a property marked with the `lazy` modifier is accessed by multiple threads simultaneously and the property hasn’t yet been initialized, there’s no guarantee that the property will be initialized only once.

**Example 3:**
```swift
struct Person
{
    var name: String
    var age: Int
}

struct Game
{
    var players: [Person]
    var value: Int
    {
        didSet
        {
            print("old value \(value)")
        }
    }
    lazy var mostRecentlyAddedPlayer = players.last!
}

let player1 = Person(name: "Kris", age: 21)
let player2 = Person(name: "Sundar", age: 21)
let player3 = Person(name: "Ram", age: 22)
let player4 = Person(name: "Shiv", age: 25)

let allPlayers = [player1, player2, player3, player4]

var game =  Game(players: allPlayers, value: 5)
print(game)
print(game.mostRecentlyAddedPlayer)
game.players.append(Person(name: "Skand", age: 22))
print(game.mostRecentlyAddedPlayer) // Lazy variable does not get computed after the first time
game.mostRecentlyAddedPlayer = game.players.last! //Manually Reassigning to get updated value
print(game.mostRecentlyAddedPlayer)
```
**Output 3:**
```
Game(players: [helloworld.Person(name: "Kris", age: 21), helloworld.Person(name: "Sundar", age: 21), helloworld.Person(name: "Ram", age: 22), helloworld.Person(name: "Shiv", age: 25)], value: 5, $__lazy_storage_$_mostRecentlyAddedPlayer: nil)
Person(name: "Shiv", age: 25)
Person(name: "Shiv", age: 25)
Person(name: "Skand", age: 22)
```

Do note that Lazy Properties are not computed everytime you access them like Computed Properties. Lazy Properties get computed on first access and store the computed value and do not update their values on subsequent access.

### Property Wrappers 
A property wrapper adds a layer of separation between code that manages how a property is stored and the code that defines a property. For example, if you have properties that provide thread-safety checks or store their underlying data in a database, you have to write that code on every property. When you use a property wrapper, you write the management code once when you define the wrapper, and then reuse that management code by applying it to multiple properties.

To define a property wrapper, you make a structure, enumeration, or class that defines a `wrappedValue` property and add `@propertyWrapper` attribute to the entity. The property wrapper is then applied to a property using the attribute `@propertyName` before the property declaration.

**Example 4:**
```swift
@propertyWrapper struct Capitalized
{
    private var originalValue: String = ""
    
    var wrappedValue: String
    {
        get
        {
            originalValue
        }
        set
        {
            originalValue = capitalizeString(newValue)
        }
    }
    
    private func capitalizeString(_ value: String) -> String
    {
        let first = value[value.startIndex].uppercased()
        let remaining = String(value.dropFirst())
        return first + remaining
    }
    
    init(wrappedValue: String)
    {
        self.wrappedValue = wrappedValue
    }
}

struct Person: CustomStringConvertible
{
    @Capitalized var firstName: String
    @Capitalized var lastName: String
    
    var fullName: String
    {
        firstName + " " + lastName
    }
    
    var description: String
    {
        "Person(firstName: \(firstName), lastName: \(lastName), fullName: \(fullName))"
    }
}

var person1 = Person(firstName: "ashwin", lastName: "kumar")
print(person1) // Capitalized Version got updated
person1.firstName = "tharun"
print(person1.firstName) // Capitalized Version got updated
```
**Output 4:**
```
Person(firstName: Ashwin, lastName: Kumar, fullName: Ashwin Kumar)
Tharun
```

Now that we have seen about Structures in Swift, let's move on to see about Classes in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/closures.html">&larr; Closures</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/classes.html">Classes &rarr;</a>
</span>
