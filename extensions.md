**Published by Arunprasadh C on 02 June 2022** • *Last Updated on 02 June 2022*

## Extensions in Swift
Extensions add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you don’t have access to the original source code (known as retroactive modeling). Extensions are similar to categories in **Objective-C** and **Kotlin** Extensions. 

Extensions in Swift can:
- Add computed instance properties and computed type properties.
- Define instance methods and type methods.
- Provide new initializers.
- Define subscripts.
- Define and use new nested types.
- Make an existing type conform to a protocol (will be covered in [Protocols](https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html)).
- Add new Functionality to Protocols, that conforming types can make use of (will be covered in [Protocols](https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html)).

It is important to note that Extensions can add new functionality to a type, but can’t override existing functionality.

Extensions can be declared by using the keyword `extension` followed by the Type name to which the extension is to be added.

**Syntax:**
```swift
extension Type
{
  // Functionality to be added
}
```

### Impact of Access Levels on Extensions
You can extend a class, structure, or enumeration in any access context in which the class, structure, or enumeration is available. Any type members added in an extension have the same default access level as type members declared in the original type being extended. If you extend a `public` or `internal` type, any new type members you add have a default access level of `internal`. If you extend a `fileprivate` type, any new type members you add have a default access level of `fileprivate`. If you extend a `private` type, any new type members you add have a default access level of `private`.

Alternatively, you can mark an extension with an explicit access-level modifier (for example, `private`) to set a new default access level for all members defined within the extension. This new default can still be overridden within the extension for individual type members.

You can’t provide an explicit access-level modifier for an extension if you’re using that extension to add protocol conformance. Instead, the protocol’s own access level is used to provide the default access level for each protocol requirement implementation within the extension.

#### Private Members in Extensions
Extensions that are in the same file as the class, structure, or enumeration that they extend behave as if the code in the extension had been written as part of the original type’s declaration. As a result, you can:

- Declare a `private` member in the original declaration, and access that member from extensions in the same file.
- Declare a `private` member in one extension, and access that member from another extension in the same file.
- Declare a `private` member in an extension, and access that member from the original declaration in the same file.

This behavior means you can use extensions in the same way to organize your code, whether or not your types have `private` entities. 

### Computed Properties
Extensions can add computed instance properties and computed type properties to existing types. 

**NOTE:** Extensions can add new computed properties, but they can’t add stored properties, or add property observers to existing properties.

**Example 1:**
```swift
extension Double
{
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
}

let oneInch = 25.4.mm
print("One inch is \(oneInch) meters")
let threeFeet = 3.ft
print("Three feet is \(threeFeet) meters")
```
**Output 1:**
```
One inch is 0.0254 meters
Three feet is 0.914399970739201 meters
```

The above example adds computed properties to the existing `Double` Type for representing various units of length.

### Initializers
Extensions can add new initializers to existing types. This enables you to extend other types to accept your own custom types as initializer parameters, or to provide additional initialization options that were not included as part of the type’s original implementation.

Extensions can add new convenience initializers to a class, but they can’t add new designated initializers or deinitializers to a class. Designated initializers and deinitializers must always be provided by the original class implementation.

If you use an extension to add an initializer to a value type that provides default values for all of its stored properties and doesn’t define any custom initializers, you can call the default initializer and memberwise initializer for that value type from within your extension’s initializer. This wouldn’t be the case if you had written the initializer as part of the value type’s original implementation.

If you use an extension to add an initializer to a structure that was declared in another module, the new initializer can’t access `self` until it calls an initializer from the defining module.

**NOTE:** If you provide a new initializer with an extension, you are still responsible for making sure that each instance is fully initialized once the initializer completes.

**Example 2:**
```swift
struct Size
{
    var width = 0.0, height = 0.0
}

struct Point
{
    var x = 0.0, y = 0.0
}

struct Rect
{
    var origin = Point()
    var size = Size()
}

extension Rect
{
    init(center: Point, size: Size)
    {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}

let centerRect = Rect(center: Point(x: 4.0, y: 4.0), size: Size(width: 3.0, height: 3.0))

print(centerRect)
```
**Output 2:**
```
Rect(origin: helloworld.Point(x: 2.5, y: 2.5), size: helloworld.Size(width: 3.0, height: 3.0))
```

### Methods
Extensions can add new instance methods and type methods to existing types.

**Example 3:**
```swift
extension Int
{
    func loop(_ action: () -> Void) // Extension Instance Method
    {
        for _ in 0..<self
        {
            action()
        }
    }
    
    static func checkPrimality(of number: Int) -> Bool //Extension Type Method
    {
        if number <= 1
        {
            return false
        }
        
        if number == 2
        {
            return true
        }
        
        if number > 2 && number.isMultiple(of: 2)
        {
            return false
        }
        
        for x in 3...Int(floor(sqrt(Double(number/2))))
        {
            if number.isMultiple(of: x)
            {
                return false
            }
        }
        return true
    }
}

5.loop  // Execute Loop Closure for 5 times
{
    let r = Int.random(in: 1...100)
    print("Is \(r) a Prime Number ? \(Int.checkPrimality(of: r))")
}
```
**Output 3:**
```
Is 96 a Prime Number ? false
Is 10 a Prime Number ? false
Is 44 a Prime Number ? false
Is 34 a Prime Number ? false
Is 71 a Prime Number ? true
```

#### Mutating Instance Methods
Instance methods added with an extension can also modify (or mutate) the instance itself. Structure and enumeration methods that modify `self` or its properties must mark the instance method as `mutating`, just like mutating methods from an original implementation.

**Example 4:**
```swift
extension Int
{
    mutating func square()
    {
        self *= self
    }
}

var num = 81
num.square()
print(num)
```
**Output 4:**
```
6561
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/typecasting.html">&larr; Type Casting</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html">Protocols &rarr;</a>
</span>
