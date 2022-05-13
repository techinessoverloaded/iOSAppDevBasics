**Published by Arunprasadh C on 06 May 2022** • *Last Updated on 13 May 2022*

## Collections in Swift
As in other languages, Collections in Swift are used to store collections of values. There are three primary kinds of Collections available in Swift :

### Arrays
An array is a collection of data. Unlike C/C++, Swift allows both homogeneous and heterogeneous arrays. Arrays in Swift are handled by the `Array<DataType>` `struct`. Arrays can be declared either by type annotating as `Array<DataType>` or simply as `Array` or `[DataType]` or by specifying the array values as comma separated literals within `[ ]` or using Array constructor. Immutable arrays can be declared using `let` keyword while mutable ones can be declared using `var` keyword.

**Syntax :**
```swift
var arrayName: [DataType] = [Value1, Value2, Value3, ....]
```
**or**
```swift
var arrayName: Array<DataType> = [Value1, Value2, Value3, ....]
```
**or**
```swift
var arrayName: Array = [Value1, Value2, Value3, ....]
```
**or**
```swift
var arrayName = [DataType]() // Empty array
```
**or**
```swift
var arrayName = Array<DataTyoe>(repeating: Int, count: Int) // generates an array with repeating elements of given count
```

Note that `[DataType]()` and `Array<DataType>()` are equivalent.

**Example 1:**
```swift
var odd : Array = [1,3,5]
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
var hellos = Array(repeating: "hello", count: 5)
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

Even an array of tuples can be declared and used as shown below. The subscript syntax `[]` is used to access and modify array elements.

**Example 4:**
```swift
typealias Rectangle = (length: Int, breadth: Int)
let rect1 = Rectangle(length: 4, breadth: 3)
let rect2 = Rectangle(length: 8, breadth: 7)
let rect3 = Rectangle(length: 10, breadth: 4)
let rectangles: [Rectangle] = [rect1, rect2, rect3]
for i in rectangles.indices
{
    print("The area of rectangle with length: \(rectangles[i].length) and breadth: \(rectangles[i].breadth) is: \(rectangles[i].length * rectangles[i].breadth)")
}
```

**Output 4:**
```
The area of rectangle with length: 4 and breadth: 3 is: 12
The area of rectangle with length: 8 and breadth: 7 is: 56
The area of rectangle with length: 10 and breadth: 4 is: 40
```

Many useful in-built functions are available for Arrays in Swift. The following example showcases some of them:

**Example 5:**
```swift
var intArray = [1, 3, 4, 5, 7, 8, 9]
print("Original array: \(intArray)")
intArray.insert(2, at: 1) // Insert element at given index
intArray.insert(6, at: 5) // Insert element at given index
print("Array after inserting elements: \(intArray)")
intArray.append(10) // Append element at last index
print("Array after appending element at last: \(intArray)")
print("Number of elements in array: \(intArray.count)")
intArray.shuffle() // Randomly shuffle the elements of array
print("Array after shuffling elements: \(intArray)")
intArray.swapAt(2, 4)
print("Array after swapping indices 2 and 4: \(intArray)")
print("Random element from array: \(intArray.randomElement()!)") // Get a random element from array
intArray.sort{ $0 > $1 }
print("Sorting array in descending order: \(intArray)")
intArray.reverse()
print("Getting Original array by reversing the array: \(intArray)")
var evenArray = intArray.filter{ $0.isMultiple(of: 2) } // Filter the elements of array based on a given predicate
print("Filtered array with only even elements: \(evenArray)")
evenArray.removeLast() // Remove the last element of array
print("Even array after removing last element: \(evenArray)")
print("Does even array contain element 4 ? \(evenArray.contains(4))")
evenArray.removeAll() // Remove all elements from Even Array
print("Is Even Array empty ? \(evenArray.isEmpty)") // Check if even array is empty
```

**Output 5:**
```
Original array: [1, 3, 4, 5, 7, 8, 9]
Array after inserting elements: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Array after appending element at last: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Number of elements in array: 10
Array after shuffling elements: [10, 1, 3, 9, 4, 5, 8, 6, 7, 2]
Array after swapping indices 2 and 4: [10, 1, 4, 9, 3, 5, 8, 6, 7, 2]
Random element from array: 8
Sorting array in descending order: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Getting Original array by reversing the array: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Filtered array with only even elements: [2, 4, 6, 8, 10]
Even array after removing last element: [2, 4, 6, 8]
Does even array contain element 4 ? true
Is Even Array empty ? true
```

### Sets
A set


### Dictionaries


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/loops.html">&larr; Loops</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/funclosures.html">Functions and Closures&rarr;</a>
</span>
