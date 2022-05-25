**Published by Arunprasadh C on 24 May 2022** • *Last Updated on 25 May 2022*

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
But, this is not the right practice in Swift. You can notice that for `description` property, I have used curly braces to indicate the value to be returned. This is because of two reasons: One is that I have used values of other properties inside the string and other is that I am trying to leverage the benefits of Swift Structure Properties. Properties are not like normal variables/constants in Swift. They can have computed Getter and Setter functions (Like **C#** and **Kotlin**). Such properties are known as Computed Properties. Getter is denoted by `get` keyword and Setter is denoted by `set` keyword. The setter provides the updated value through an immutable value called `newValue` (It is the value assigned to the property via dot `.` syntax) and even a custom name can be used for the same. By means of `set` and `get` Access and Mutation of values can be easily done via the dot `.` Syntax. And some computation can also be done before accessing or mutating the property.



<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/closures.html">&larr; Closures</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
