**Published by Arunprasadh C on 06 May 2022** • *Last Updated on 12 May 2022*

## Collections in Swift
As in other languages, Collections in Swift are used to store collections of values. There are three primary kinds of Collections available in Swift :

### Arrays
An array is a collection of data. Unlike C/C++, Swift allows both homogeneous and heterogeneous arrays. Arrays in Swift are handled by the `Array<DataType>` `struct`. Arrays can be declared either by type annotating as `Array<DataType>` or `[DataType]` or by specifying the array values as comma separated literals within `[ ]` or using Array constructor. Immutable arrays can be declared using `let` keyword while mutable ones can be declared using `var` keyword.

**Syntax :**
```swift
var/let arrayName: [DataType] = [Value1, Value2, Value3, ....]
```
**or**
```swift
var/let arrayName: Array<DataType> = [Value1, Value2, Value3, ....]
```
**or**
```swift
var/let arrayName = [Value1, Value2, Value3, ....]
```
**or**
```swift
var/let arrayName = [DataType]() // Empty array
```
**or**
```swift
var/let arrayName = Array<DataTyoe>(repeating: Int, count: Int) // generates an array with repeating elements of given count
```

Note that `[DataType]()` and `Array<DataType>()` are equivalent.

**Example 1:**
```swift
var odd : Array<Int> = [1,3,5]
var even : [Int] = [2,4,6]
for i in 0...2
{
    print(odd[i], even[i], separator: ", ", terminator: ", ")
}
```

**Output 1:**
```
1, 2, 3, 4, 5, 6,
```


**Example 2:**
```swift
var hellos = Array<String>(repeating: "hello", count: 5)
print(hellos)
```

**Output 2:**
```
["hello", "hello", "hello", "hello", "hello"]
```

Heterogeneous Arrays can be declared by using `Any` type, which can literally represent any type of value.

**Example 3:**
```swift
var anyArray: [Any] = [1, "Hello", 4.5, true]
print(anyArray)
for x in anyArray
{
    print(type(of: x), separator: ", ", terminator: ", ")
}
```

**Output 3:**
```
[1, "Hello", 4.5, true]
Int, String, Double, Bool,
```

### Sets

### Dictionaries


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/loops.html">&larr; Loops</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
