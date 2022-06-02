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

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/enums.html">&larr; Enumerations</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
