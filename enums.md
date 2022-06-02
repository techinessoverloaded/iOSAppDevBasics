**Published by Arunprasadh C on 02 June 2022** • *Last Updated on 02 June 2022*

## Enumerations in Swift
An Enumeration defines a common type for a group of related values and enables you to work with those values in a type-safe way within your code.

If you are familiar with **C**, you will know that **C** enumerations assign related names to a set of integer values. Enumerations in Swift are much more flexible, and don’t have to provide a value for each case of the enumeration. If a value (known as a raw value) is provided for each enumeration case, the value can be a string, a character, or a value of any integer or floating-point type.

Alternatively, enumeration cases can specify associated values of any type to be stored along with each different case value, much as unions or variants do in other languages. You can define a common set of related cases as part of one enumeration, each of which has a different set of values of appropriate types associated with it.

Enumerations are **Value Types** like Structures. Enumerations are declared by using the `enum` keyword in Swift. The `case` keyword is used to declare values inside an Enumeration. Cases can appear on multiple lines or can be defined in a single line, separated by comma `,`.

**Example 1:**
```swift
enum Direction
{
    case north, south, east, west
}
```


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/classes.html">&larr; Classes</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
