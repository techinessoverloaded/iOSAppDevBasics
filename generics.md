**Published by Arunprasadh C on 03 June 2022** • *Last Updated on 03 June 2022*

## Generics
Generic code enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define. You can write code that avoids duplication and expresses its intent in a clear, abstracted manner.

Generics are one of the most powerful features of Swift, and much of the Swift standard library is built with generic code. For example, Swift’s `Array` and `Dictionary` types are both generic collections. You can create an array that holds `Int` values, or an array that holds `String` values, or indeed an array for any other type that can be created in Swift. Similarly, you can create a dictionary to store values of any specified type, and there are no limitations on what that type can be.

### Impact of Access Levels on Generics
The access level for a generic type or generic function is the minimum of the access level of the generic type or function itself and the access level of any type constraints on its type parameters.

### The Problem That Generics Solve
Let's take the example of swapping two variables. If we want to do that in a non-generic approach, we have to write separate functions for swapping each Type of data.

**Example 1:**
```swift
func swapInt(_ a: inout Int, _ b: inout Int)
{
    (a, b) = (b, a) // Using Tuple Syntax for swapping
}

func swapString(_ a: inout String, _ b: inout String)
{
    (a, b) = (b, a) // Using Tuple Syntax for swapping
}

var a = 5, b = 6
print("a = \(a), b = \(b)")
print("After swapping...")
swapInt(&a, &b)
print("a = \(a), b = \(b)")

var x = "Hello", y = "World"
print("x = \(x), y = \(y)")
print("After swapping...")
swapString(&x, &y)
print("x = \(x), y = \(y)")
```
**Output 1:**
```
a = 5, b = 6
After swapping...
a = 6, b = 5
x = Hello, y = World
After swapping...
x = World, y = Hello
```

You can notice that the bodies of both the `swapInt(_:_:)` and `swapString(:_,:_)` are same. We can write a single generic function in such cases.

### Generic Functions
In Swift, we can create a function that can be used with any type of data. Such a function is known as a Generic Function.

**Syntax:**
```swift
func someFunction<T>(data: T)
{
   //function body
}
```

Here, the `T` inside angular brackets `<>` is known as **Type Parameter**.
And based on the type of the value passed to the function, the `T` is replaced by that data type (`Int`, `String`, and so on).

Now, let's write a generic function for swapping two variables.

**Modified Example 1:**
```swift
func swap<T>(_ a: inout T, _ b: inout T) // Generic Function for swapping two variables
{
    (a, b) = (b, a) // Using Tuple Syntax for swapping
}

var a = 5, b = 6
print("a = \(a), b = \(b)")
print("After swapping...")
swap(&a, &b)
print("a = \(a), b = \(b)")

var x = "Hello", y = "World"
print("x = \(x), y = \(y)")
print("After swapping...")
swap(&x, &y)
print("x = \(x), y = \(y)")

```
**Output 1:**
```
a = 5, b = 6
After swapping...
a = 6, b = 5
x = Hello, y = World
After swapping...
x = World, y = Hello
```

### Type Parameters
Type parameters specify and name a placeholder type, and are written immediately after the function’s name, between a pair of matching angle brackets (such as `<T>`). Once you specify a type parameter, you can use it to define the type of a function’s parameters (such as the `a` and `b` parameters of the `swap(_:,_:)` function) or as the function’s return type, or as a type annotation within the body of the function. In each case, the type parameter is replaced with an actual type whenever the function is called. (In the `swap(_:,_:)` example above, `T` was replaced with `Int` the first time the function was called, and was replaced with `String` the second time it was called.)

You can provide more than one type parameter by writing multiple type parameter names within the angle brackets, separated by commas `,`.

#### Naming Type Parameters
In most cases, type parameters have descriptive names, such as `Key` and `Value` in `Dictionary<Key, Value>` and `Element` in `Array<Element>`, which tells the reader about the relationship between the type parameter and the generic type or function it’s used in. However, when there isn’t a meaningful relationship between them, it’s traditional to name them using single letters such as `T`, `U`, and `V`, such as `T` in the `swap(_:,_:)` function above.

### Generic Types
In addition to generic functions, Swift enables you to define your own generic types. These are custom classes, structures, and enumerations that can work with any type, in a similar way to `Array` and `Dictionary`. The following syntax shows how to define a generic `struct`. The same syntax can be used with `class` and `enum` too, just by replacing `struct` with the appropriate keyword.

**Syntax:**
```swift
struct<T>
{
   //Methods and Properties
}
```

**Example 2:**
```swift
struct Stack<Element>
{
    private var values: [Element] = []
    
    var count: Int
    {
        values.count
    }
    
    mutating func push(_ newElement: Element)
    {
        values.append(newElement)
    }
    
    mutating func pop()
    {
        values.removeLast()
    }
    
    func peek() -> Element?
    {
        values.last
    }
    
    func printStack()
    {
        print("\(values[values.endIndex - 1]) <- Top")
        var i = values.endIndex - 2
        while i >= values.startIndex
        {
            print(values[i])
            i -= 1
        }
    }
}

var intStack = Stack<Int>()
intStack.push(5)
intStack.push(4)
intStack.push(3)
intStack.push(2)
intStack.push(1)
print("The stack has: \(intStack.count) Elements.")
print("Original Stack:")
intStack.printStack()
print("Top element: \(intStack.peek()!)")
intStack.pop()
print("Top element after popping: \(intStack.peek()!)")
intStack.pop()
intStack.pop()
print("Now, the stack has: \(intStack.count) Elements.")
print("Stack's present state:")
intStack.printStack()

var stringStack: Stack<String> = Stack()
stringStack.push("Day")
stringStack.push("Good")
stringStack.push("World")
stringStack.push("Hello")
print("String stack:")
stringStack.printStack()
```
**Output 2:**
```
The stack has: 5 Elements.
Original Stack:
1 <- Top
2
3
4
5
Top element: 1
Top element after popping: 2
Now, the stack has: 2 Elements.
Stack's present state:
4 <- Top
5
String stack:
Hello <- Top
World
Good
Day
```

The above declared `Stack<Element>` can work with any Data Type.

### Extending a Generic Type
When you extend a generic type, you don’t provide a type parameter list as part of the extension’s definition. Instead, the type parameter list from the original type definition is available within the body of the extension, and the original type parameter names are used to refer to the type parameters from the original definition. The following Example adds extensions to the `Stack<Element>` type from the above example:

**Example 3:**
```swift
extension Stack
{
    var isEmpty: Bool
    {
        count == 0
    }
    
    mutating func clearStack()
    {
        values.removeAll()
    }
}

var intStack = Stack<Int>()
intStack.push(5)
intStack.push(4)
intStack.push(3)
intStack.push(2)
intStack.push(1)
print("The stack has: \(intStack.count) Elements.")
print("Original Stack:")
intStack.printStack()
print("Top element: \(intStack.peek()!)")
intStack.pop()
print("Top element after popping: \(intStack.peek()!)")
intStack.pop()
intStack.pop()
print("Now, the stack has: \(intStack.count) Elements.")
print("Stack's present state:")
intStack.printStack()
intStack.clearStack()
print("Is intStack empty now ? \(intStack.isEmpty)")
```
**Output 2:**
```
The stack has: 5 Elements.
Original Stack:
1 <- Top
2
3
4
5
Top element: 1
Top element after popping: 2
Now, the stack has: 2 Elements.
Stack's present state:
4 <- Top
5
Is intStack empty now ? true
```



<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html">&larr; Protocols</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
