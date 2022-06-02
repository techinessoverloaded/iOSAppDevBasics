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

###


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/typecasting.html">&larr; Type Casting</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/protocols.html">Protocols &rarr;</a>
</span>
