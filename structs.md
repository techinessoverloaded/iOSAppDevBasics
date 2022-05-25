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

**Modified Example 1:**
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
**Output 1:**
```
Student (rollNo = 2 ; name = Kris)
Student (rollNo = 2 ; name = Kris)
```



<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/closures.html">&larr; Closures</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
