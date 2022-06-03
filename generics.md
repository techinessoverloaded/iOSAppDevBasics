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

### Type Constraints
In general, the type parameter can accept any data type (`Int`, `String`, `Double`, ...).

However, if we want to use generics for some specific types (such as accepting data of number types) only, then we can use type constraints.

You write type constraints by placing a single class or protocol constraint after a type parameter’s name, separated by a colon, as part of the type parameter list. The basic syntax for type constraints on a generic function is shown below (although the syntax is the same for generic types):

**Syntax:**
```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U)
{
  // Function Body
}
```

The hypothetical function above has two type parameters. The first type parameter, `T`, has a type constraint that requires `T` to be a subclass of `SomeClass`. The second type parameter, `U`, has a type constraint that requires `U` to conform to the protocol `SomeProtocol`.

**Example 3:**
```swift
func sum<T: SignedNumeric>(_ values: T...) -> T
{
    var result: T = 0
    values.forEach {
        result += $0
    }
    
    return result
}

print(sum(99, 57, 86, 89.6, -98.2, 563, -42))
```
**Output 3:**
```
754.4000000000001
```

The above example defines a function `sum(_:)` which requires variadic arguments of any Type that conforms to the `SignedNumeric` Protocol of the Swift Standard Library. `SignedNumeric` Protocol is used to represent any number that can have sign. So, types like `Int`, `Double` conform to the protocol. Hence, when multiple numbers are passed, the result is obtained. However, trying to pass a `String` value to the function will throw an error as `String` does not conform to the `SignedNumeric` Protocol.

### Associated Types
When defining a protocol, it’s sometimes useful to declare one or more associated types as part of the protocol’s definition. An associated type gives a placeholder name to a type that’s used as part of the protocol. The actual type to use for that associated type isn’t specified until the protocol is adopted. Associated types are specified with the `associatedtype` keyword.

**Example 4:**
```swift
protocol Container
{
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

struct Stack<Element>: Container
{
    // Basic Implementation
    private var values: [Element] = []
    
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
    
    // Implementation of Container Protocol
    typealias Item = Element
    
    mutating func append(_ item: Element)
    {
        self.push(item)
    }
    
    var count: Int
    {
        values.count
    }
        
    subscript(i: Int) -> Element
    {
        values[i]
    }
}
```

#### Extending an Existing Type to Specify an Associated Type
You can extend an existing type to add conformance to a protocol. This includes a protocol with an associated type.

**Example 5:**
```swift
extension Array: Container {}
```

#### Adding Constraints to an Associated Type
You can add type constraints to an associated type in a protocol to require that conforming types satisfy those constraints. For example, the following code defines a version of `Container` that requires the items in the container to be `Equatable`.

**Example 6:**
```swift
protocol Container 
{
    associatedtype Item: Equatable
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

### Generic Where Clauses
Type constraints enable you to define requirements on the type parameters associated with a generic function, subscript, or type. It can also be useful to define requirements for associated types. You do this by defining a generic `where` clause. A generic `where` clause enables you to require that an associated type must conform to a certain protocol, or that certain type parameters and associated types must be the same. A generic `where` clause starts with the `where` keyword, followed by constraints for associated types or equality relationships between types and associated types. You write a generic `where` clause right before the opening curly brace of a type or function’s body.

**Example 7:**
```swift
protocol Container
{
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

struct Stack<Element>: Container
{
    // Basic Implementation
    private var values: [Element] = []
    
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
    
    // Implementation of Container Protocol
    typealias Item = Element
    
    mutating func append(_ item: Element)
    {
        self.push(item)
    }
    
    var count: Int
    {
        values.count
    }
        
    subscript(i: Int) -> Element
    {
        values[i]
    }
}

extension Array: Container {}

func allItemsMatch<C1: Container, C2: Container>
    (_ someContainer: C1, _ anotherContainer: C2) -> Bool where C1.Item == C2.Item, C1.Item: Equatable
{
    // Check that both containers contain the same number of items.
    if someContainer.count != anotherContainer.count
    {
        return false
    }

    // Check each pair of items to see if they're equivalent.
    for i in 0..<someContainer.count
    {
        if someContainer[i] != anotherContainer[i]
        {
            return false
        }
    }

    // All items match, so return true.
    return true
}

typealias StrStack = Stack<String>

var strStack = StrStack()
strStack.push("dos")
strStack.push("windows")
strStack.push("unix")
strStack.push("linux")
let arr = ["dos", "windows", "unix", "linux"]
print("Do all the items match ? \(allItemsMatch(strStack, arr))")
```
**Output 7:**
```
Do all the items match ? true
```

### Extensions with a Generic Where Clause
You can also use a generic where clause as part of an extension. The example below extends the generic `Stack<Element>` structure from the previous examples to add an `isTop(_:)` method.

**Example 8:**
```swift
extension Stack where Element: Equatable
{
    func isTop(_ item: Element) -> Bool
    {
        guard let topItem = values.last else
        {
            return false
        }
        return topItem == item
    }
}

typealias StrStack = Stack<String>

var strStack = StrStack()
strStack.push("dos")
strStack.push("windows")
strStack.push("unix")
strStack.push("linux")
print("Is linux the top item ? \(strStack.isTop("linux"))")
```
**Output 8:**
```
Is linux the top item ? true
```

If you try to call the `isTop(_:)` method on a stack whose elements aren’t `Equatable`, you’ll get a compile-time error.

### Contextual Where Clauses
You can write a generic where clause as part of a declaration that doesn’t have its own generic type constraints, when you’re already working in the context of generic types. For example, you can write a generic `where` clause on a subscript of a generic type or on a method in an extension to a generic type. The `Container` structure is generic, and the `where` clauses in the example below specify what type constraints have to be satisfied to make these new methods available on a container.

**Example 9:**
```swift
extension Container
{
    func average() -> Double where Item == Int
    {
        var sum = 0.0
        for index in 0..<count
        {
            sum += Double(self[index])
        }
        return sum / Double(count)
    }
    
    func endsWith(_ item: Item) -> Bool where Item: Equatable
    {
        return count >= 1 && self[count-1] == item
    }
}
let numbers = [1260, 1200, 98, 76, 37]
print(numbers.average())
print(numbers.endsWith(37))
```
**Output 9:**
```
534.2
true
```

### Associated Types with a Generic Where Clause
You can include a generic where clause on an associated type. For example, suppose you want to make a version of `Container` that includes an iterator, like what the Sequence protocol uses in the standard library. Here’s how you write that:

**Example 10:**
```swift
protocol Container
{
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
    associatedtype Iterator: IteratorProtocol where Iterator.Element == Item
    func makeIterator() -> Iterator
}
```

For a protocol that inherits from another protocol, you add a constraint to an inherited associated type by including the generic where clause in the protocol declaration. For example, the following code declares a `ComparableContainer` protocol that requires `Item` to conform to `Comparable`:

**Example 11:**
```
protocol ComparableContainer: Container where Item: Comparable {}
```

### Generic Subscripts
Subscripts can be generic, and they can include generic `where` clauses. You write the placeholder type name inside angle brackets after subscript, and you write a generic `where` clause right before the opening curly brace of the subscript’s body. For example:

**Example 12:**
```swift
extension Container
{
    subscript<Indices: Sequence>(indices: Indices) -> [Item]
        where Indices.Iterator.Element == Int
    {
        var result: [Item] = []
        for index in indices
        {
            result.append(self[index])
        }
        return result
    }
}
```

Now that we have seen about Generics in Swift, let's move on to see about Error Handling in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html">&larr; Protocols</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/errorhandling.html">Error Handling &rarr;</a>
</span>
