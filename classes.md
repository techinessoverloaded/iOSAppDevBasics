**Published by Arunprasadh C on 26 May 2022** • *Last Updated on 30 May 2022*

## Classes in Swift
A Class is considered as a blueprint of objects. In Swift, a Class is similar to a Structure in most of the aspects. However, Swift Classes have the following unique properties and additional capabilities as compared to Structures:
- Classes are **Reference Types** unlike Structures. This means that the Objects of a Class are passed by Reference. Also, ARC allows multiple references of a class instance to exist.
- Classes support Inheritance.
- Classes support Typecasting.
- Classes can have Deinitializers (similar to **C++** Destructors) in addition to Initializers.

Due to the above mentioned capabilities, Classes in Swift can leverage all the benefits of Object-oriented Programming. Classes in Swift are marked by the `class` keyword.

**Syntax :**
```swift
class ClassName
{
   //Class Properties and Methods
}
```

It is similar to `struct` declaration, right ? So, when to choose Class over Structure ?

### Choosing between Classes and Structures
The [Apple Developer Documentation](https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes) suggests the following Recommendations (Quoted from the Documentation):
- **Choose Structures by Default:** Using structures makes it easier to reason about a portion of your code without needing to consider the whole state of your app. Because structures are value types—unlike classes—local changes to a structure aren't visible to the rest of your app unless you intentionally communicate those changes as part of the flow of your app. As a result, you can look at a section of code and be more confident that changes to instances in that section will be made explicitly, rather than being made invisibly from a tangentially related function call. That is why even the Swift Standard Library uses Structures throughout and the usage of Classes is minimalized.

- **Use Classes When You Need Objective-C Interoperability:** If you use an Objective-C API that needs to process your data, or you need to fit your data model into an existing class hierarchy defined in an Objective-C framework, you might need to use classes and class inheritance to model your data. For example, many Objective-C frameworks expose classes that you are expected to subclass.

- **Use Classes When You Need to Control Identity and Structures otherwise:** Classes in Swift come with a built-in notion of identity because they're reference types. This means that when two different class instances have the same value for each of their stored properties, they're still considered to be different by the identity operator (`===`). It also means that when you share a class instance across your app, changes you make to that instance are visible to every part of your code that holds a reference to that instance. Use classes when you need your instances to have this kind of identity. Use structures when you're modeling data that contains information about an entity with an identity that you don't control.

- **Use Structures and Protocols to Model Inheritance and Share Behavior:** Structures and classes both support a form of inheritance. Structures and protocols can only adopt protocols; they can't inherit from classes. However, the kinds of inheritance hierarchies you can build with class inheritance can be also modeled using protocol inheritance and structures. If you're building an inheritance relationship from scratch, prefer protocol inheritance. Protocols permit classes, structures, and enumerations to participate in inheritance, while class inheritance is only compatible with other classes. When you're choosing how to model your data, try building the hierarchy of data types using protocol inheritance first, then adopt those protocols in your structures.

### Object Creation and Accessing Members
Object creation, accessing properties and methods of a `class` and  are all similar to `struct`.

**Example 1:**
```swift
class Student
{
    var rollNo: Int
    var name: String
    
    init(rollNo: Int, name: String)
    {
        self.rollNo = rollNo
        self.name = name
    }
}

let student = Student(rollNo: 1, name: "Kris")
print(student.rollNo)
print(student.name)
print(student)
```
**Output 1:**
```
1
Kris
helloworld.Student
```

You can immediately notice that I have defined a member-wise Initializer. I have done so because, classes don't generate Member-wise initializer on their own, unlike Structures which do so as Classes allow Inheritance and it is difficult for the compiler to decide how the Initializer should be generated. If Initializer is not defined manually for the Class, the code won't compile and the compiler will throw an error `Class 'ClassName' has no initializers`.

You can also notice that when I printed the `student` object, I didn't get a standard `String` representation of the object like Structures. This is because `class` in Swift doesn't conform to `CustomStringConvertible` Protocol by default unlike Structures and even this can be attributed to Inheritance because only at runtime, the type of object is decided.

### Protocol Conformance
Classes can also conform to Protocols like Structures and use the same syntax as Structures for conforming. We will see more about Protocols in a separate Topic Page.

### Behaviour with `let` Constants
As mentioned earlier in [Structures](https://techinessoverloaded.github.io/iOSAppDevBasics/structs.html), `let` Constants behave differently with Classes. The regular behaviour of preventing reassigning of objects is maintained. However, the properties of Class object can be mutated even when using `let`, as Classes are Reference Types.

**Example 2:**
```swift
class Student: CustomStringConvertible
{
    var rollNo: Int
    var name: String
    var description: String
    {
        "Student(rollNo = \(rollNo), name = \(name))"
    }
    
    init(rollNo: Int, name: String)
    {
        self.rollNo = rollNo
        self.name = name
    }
}
let student = Student(rollNo: 1, name: "Kris")
print(student.description)
print(student.rollNo)
student.name = "Shiv" // Modifying the property of a let constant object
print(student.name)
print(student)
```
**Output 2:**
```
Student(rollNo = 1, name = Kris)
1
Shiv
Student(rollNo = 1, name = Shiv)
```

You can see that the name was changed even though `student` is a `let` constant.

### No need of `mutating` Keyword for Mutating Methods
Unlike `struct`, the Mutating Methods of `class` don't need the `mutating` keyword, as Classes are Reference Types.

**Example 3:**
```swift
class Student: CustomStringConvertible
{
    var rollNo: Int
    var name: String
    var description: String
    {
        "Student(rollNo = \(rollNo), name = \(name))"
    }
    
    init(rollNo: Int, name: String)
    {
        self.rollNo = rollNo
        self.name = name
    }
    
    func changeRollNoAndName(newRollNo:Int, newName: String)
    {
        rollNo = newRollNo
        name = newName
    }
}

let student = Student(rollNo: 1, name: "Kris")
print("Original Value: \(student)")
student.changeRollNoAndName(newRollNo: 2, newName: "Shiv")
print("After calling changeRollNoAndName() Method: \(student)")
```
**Output 3:**
```
Original Value: Student(rollNo = 1, name = Kris)
After calling changeRollNoAndName() Method: Student(rollNo = 2, name = Shiv)
```

### Deinitializer
In addition to Initializers, Swift Classes can also have a single Deinitializer, which is called just before the Object of the Class is deallocated (Similar to **C++** Destructors). These can be used for performing additional tasks like closing a file or any held resource, thereby freeing up the memory before the class object itself is deallocated. Messages printed inside Deinitializer block can generally be realized when the object is being deallocated.

**Example 4:**
```swift
class Student: CustomStringConvertible
{
    var rollNo: Int
    var name: String
    var description: String
    {
        "Student(rollNo = \(rollNo), name = \(name))"
    }
    
    init(rollNo: Int, name: String)
    {
        self.rollNo = rollNo
        self.name = name
    }
    
    func changeRollNoAndName(newRollNo:Int, newName: String)
    {
        rollNo = newRollNo
        name = newName
    }
    
    deinit
    {
        print("Student: \(name) is being deinitialized...")
    }
}

var student: Student? = Student(rollNo: 1, name: "Kris")
print(student!)
student = nil // Deinitializing the object
let _ = Student(rollNo: 2, name: "Siva") // Using '_' to indicate ignored or unused object. Hence it is deallocated immediately.
```
**Output 4:**
```
Student(rollNo = 1, name = Kris)
Student: Kris is being deinitialized...
Student: Siva is being deinitialized...
```

When `nil` is assigned to the Optional `student` object, it means that it can be deallocated and hence the deinitializer is called. Underscore `_` is used for Wildcard Pattern Matching in Swift. It is used whenever a variable or constant is ignored or unwanted. It is also used when the return type of a function is ignored. It is used in for loops too when the iterating variable can be ignored. In the Above example, the `_` indicates that the object can be ignored or is not going to be used. Hence, the scope of the object gets over as soon as it is created and hence, the deinitializer is called.

### Equality and Identity Logic
Unlike Structures, the Identity Operators (`===` and `!==`) can be used with Classes. Identity Operators compare the memory uniqueness of two class instances. They don't check if the values are equal. They instead check if the two instances point to the same reference in the memory. In order 

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/structs.html">&larr; Structures</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
