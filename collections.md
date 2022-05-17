**Published by Arunprasadh C on 06 May 2022** • *Last Updated on 17 May 2022*

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

**2D Arrays** can be created by optionally type annotating as `[[DataType]]` or `Array<[DataType]>` or `Array<Array<DataType>>` or `[Array<DataType>]` or simply as `Array` and assigning them to literals nested array literals.

**Example 6:**
```swift
var twoDAry : Array<[Int]> = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(twoDAry)
print(type(of: twoDAry))
print("Iterating using for-in loop")
for x in twoDAry
{
    for y in x
    {
        print(y, terminator: ", ")
    }
}
print("\nIterating using while loop")
var i: Int = twoDAry.startIndex
while(i < twoDAry.endIndex)
{
    var j: Int = twoDAry[i].startIndex
    while(j < twoDAry[i].endIndex)
    {
        print(twoDAry[i][j], terminator: ", ")
        j += 1
    }
    i += 1
}
```
**Output 6:**
```
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
Array<Array<Int>>
Iterating using for-in loop
1, 2, 3, 4, 5, 6, 7, 8, 9, 
Iterating using while loop
1, 2, 3, 4, 5, 6, 7, 8, 9,
```

### Sets
A set is an unordered collection of unique values. The elements of a Set cannot be duplicate. Swift `Set` is similar to `unordered_set` of C++ and `HashSet` of Java. A `var` or `let` specifying a `Set` value must always provide type annotation as either `Set` or `Set<DataType>` because for a `Set` too, array literals (comma separated values within `[]`) are used for specifying values.

**Syntax :**
```swift
var setName: Set = [value1, value2, value3....]
```
**or**
```swift
var setName: Set<DataType> = [value1, value2, value3....]
```

**Example 1:**
```swift
var intSet: Set = [1, 2, 3, 4]
print(type(of: intSet))
print(intSet)
```
**Output 1:**
```
Set<Int>
[3, 4, 1, 2] //Since it is an unordered collection, insertion order is not maintained.
```

**Example 2:**
```swift
var uniqueSet: Set<Int> = Set<Int>() // Empty Set
for i in 1...10
{
    uniqueSet.insert(i)
}
print(uniqueSet)
for i in 5...15
{
    uniqueSet.insert(i)
}
print(uniqueSet)
```
**Output 2:**
```
[7, 6, 8, 9, 5, 1, 4, 2, 10, 3]
[14, 9, 3, 8, 10, 15, 5, 4, 13, 1, 2, 6, 11, 7, 12] // Since a Set allows only unique values, values from 5 to 10 are not inserted again.
```

The elements of a `Set` can be iterated using `for`-`in` loop. `Set` also provides `Set.Index` instead of `Int` index for accessing elements. But, in practical use, the `Set.Index` is not used as the elements are unordered and each time the Index may return a different element.

**Example 3:**
```swift
var charSet: Set<Character> = ["A", "B", "C", "D", "E", "F"]
for c in charSet
{
    print(c, terminator: " -> ")
}
print()
for c in charSet.sorted(by: >)
{
    print(c, terminator: " -> ")
}
```
**Output 3:**
```
D -> A -> F -> B -> C -> E -> 
F -> E -> D -> C -> B -> A ->
```

The `insert()` function is used to insert an element into the `Set`. The `insert()` function returns a `Tuple` containing two members: a `Bool` value named `inserted` representing whether the element was inserted (will be `true` if the element is not already there in the set and hence was inserted) and a `DataType` value named `memberAfterInsert` representing the inserted element.

**Example 4:**
```swift
var intSet: Set = [1, 2, 3, 4, 5, 6]
print("Original Set: \(intSet)")
let result = intSet.insert(10)
if(result.inserted == true)
{
    print("\(result.memberAfterInsert) was inserted successfully into the set !")
    print("Modified Set: \(intSet)")
}
```
**Output 4:**
```
Original Set: [6, 4, 2, 1, 5, 3]
10 was inserted successfully into the set !
Modified Set: [5, 1, 6, 10, 2, 4, 3]
```

Heterogeneous `Set` can be declared using `AnyHashable` type since `Set` allows only elements conforming to `Hashable` Protocol.

**Example 5:**
```swift
var anySet: Set<AnyHashable> = [1, "Hello", true, "World", 6.5]
anySet.insert(8.9)
anySet.forEach { element in
    print(element)
}
```
**Output 5:**
```
1
Hello
true
6.5
World
8.9
```

The following example showcases various methods available in `Set`:

**Example 6:**
```swift
var evenSet: Set = [2, 4, 6, 8, 10, 12]
print("Original Set: \(evenSet)")
evenSet.insert(4)
evenSet.insert(13) // Insert element into Set if it doesn't exist
evenSet.insert(20)
evenSet.insert(21)
print("Set after inserting elements: \(evenSet)")
evenSet.remove(21) // Remove given element from Set if it exists
evenSet.remove(13)
print("Set after removing elements: \(evenSet)")
print("Does set have element 8 ? \(evenSet.contains(8))")// Returns true if given element is present
print("Sorted View of Set: \(evenSet.sorted())") // Returns a sorted array using elements of set
print("Random element of Set: \(evenSet.randomElement()!)") //Random element from Set
evenSet.removeAll() // Remove all elements from Set
print("Length of Set after removing elements: \(evenSet.count)")
```
**Output 6:**
```
Original Set: [2, 12, 4, 6, 8, 10]
Set after inserting elements: [4, 10, 6, 20, 8, 2, 12, 13, 21]
Set after removing elements: [4, 10, 6, 20, 8, 2, 12]
Does set have element 8 ? true
Sorted View of Set: [2, 4, 6, 8, 10, 12, 20]
Random element of Set: 4
Length of Set after removing elements: 0
```

#### Mathematical Set Operations
Swift `Set` provides different built-in methods to perform Mathematical Set Operations like Union, Intersection, Subtraction, and Symmetric Difference.

##### Union Operation
The Union of two Sets A and B includes all the elements of set A and B (A ⋃ B). We use the `union()` method to perform the Set Union Operation.

**Example 7:**
```swift
let even: Set = [0, 2, 4, 6, 8]
let odd: Set = [1, 3, 5, 7, 9]
print("Even set: \(even)")
print("Odd set: \(odd)")
let union = even.union(odd)
print("Sorted view of Union of even and odd: \(union.sorted())")
```
**Output 7:**
```
Even set: [0, 4, 8, 6, 2]
Odd set: [7, 3, 5, 9, 1]
Sorted view of Union of even and odd: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

##### Intersection Operation
The Intersection of two Sets A and B includes all the elements common to both set A and B (A ⋂ B). We use the `intersection()` method to perform the Set Intersection Operation.

**Example 8:**
```swift
let set1: Set = [1, 2, 3, 4, 5]
let set2: Set = [0, 2, 4, 6, 8]
print("Set 1: \(set1)")
print("Set 2: \(set2)")
let intersection = set1.intersection(set2)
print("Intersection of Set 1 and Set 2: \(intersection)")
```
**Output 8:**
```
Set 1: [1, 2, 4, 3, 5]
Set 2: [6, 8, 4, 0, 2]
Intersection of Set 1 and Set 2: [2, 4]
```

##### Set Difference/Subtraction Operation
The Subtraction of two Sets A and B includes all the elements present in A but not in B (A - B). We use the `subtracting()` method to perform the Set Subtraction Operation.

**Example 9:**
```swift
let set1: Set<AnyHashable> = [1, 2.5, "Hello", true]
let set2: Set<AnyHashable> = [2.5, true, false, 6, 8]
print("Set 1: \(set1)")
print("Set 2: \(set2)")
let subtraction = set1.subtracting(set2)
print("Subtraction of Set 1 and Set 2: \(subtraction)")
```
**Output 9:**
```
Set 1: [AnyHashable(2.5), AnyHashable("Hello"), AnyHashable(true), AnyHashable(1)]
Set 2: [AnyHashable(6), AnyHashable(2.5), AnyHashable(8), AnyHashable(true), AnyHashable(false)]
Subtraction of Set 1 and Set 2: [AnyHashable("Hello"), AnyHashable(1)]
```

##### Symmetric Difference Operation
The Symmetric Difference between two Sets A and B includes all elements of A and B without the common elements ((A - B) ⋃ (B - A)). We use the `symmetricDifference()` method to perform the Set Symmetric Difference Operation.

**Example 10:**
```swift
let set1: Set = [1, 2, 3, 5]
let set2: Set = [1, 8, 9, 5]
print("Set 1: \(set1)")
print("Set 2: \(set2)")
let subtraction1 = set1.subtracting(set2)
let subtraction2 = set2.subtracting(set1)
let sub1Usub2 = subtraction1.union(subtraction2)
let symmetricDifference = set1.symmetricDifference(set2)
print("Symmetric Difference of two sets: \(symmetricDifference)")
print("Are Symmetric Difference and Union of A - B and B - A the same ? \(sub1Usub2 == symmetricDifference)")
```
**Output 10:**
```
Set 1: [5, 2, 3, 1]
Set 2: [9, 1, 5, 8]
Symmetric Difference of two sets: [2, 3, 9, 8]
Are Symmetric Difference and Union of A - B and B - A the same ? true
```

##### How to check if a Set is a Subset of another Set
The `isSubset(of: )` method is used to check if `Set` is a subset of another `Set`.

**Example 11:**
```swift
let set1: Set = [1, 2, 3, 4, 5, 6, 7, 8]
let set2: Set = [2, 4, 6, 8]
print("Set 1: \(set1)")
print("Set 2: \(set2)")
print("Is Set 2 a subset of Set 1 ? \(set2.isSubset(of: set1))")
```
**Output 11:**
```
Set 1: [3, 2, 5, 7, 6, 1, 8, 4]
Set 2: [4, 8, 2, 6]
Is Set 2 a subset of Set 1 ? true
```

### Dictionaries
Swift `Dictionary` is an Unordered Collection of Items. It stores elements in key/value pairs. Here, keys are unique identifiers that are associated with each value. The Key has to be unique and must conform to the `Hashable` Protocol. Swift `Dictionary` is similar to `unordered_map` of C++ and `HashMap` of Java. A Dictionary can be declared either by specifying Dictionary Literal (`[HashableType : Type]`), or by annotating the variable/constant as `Dictionary` along with specification of the Literal, or by annotating the variable/constant as `Dictionary<DataType, DataType>`, or by annotating as `[HashableType : Type]`.

**Syntax :**
```swift
var dictName = [key1 : value1, key2 : value2, key3 : value3,....]
```
**or**
```swift
var dictName: Dictionary = [key1 : value1, key2 : value2, key3 : value3,....]
```
**or**
```swift
var dictName: Dictionary<HashableType, Type> = [key1 : value1, key2 : value2, key3 : value3,....]
```
**or**
```swift
var dictName: [HashableType : Type] = [key1 : value1, key2 : value2, key3 : value3,....]
```

**Example 1:**
```swift
//Creating empty Dictionary
var empty1: [Int : Float] = [Int : Float]()
var empty2: [String : Int] = [:]
var empty3 = Dictionary<Double, Int>()
print(empty1, empty2, empty3, separator: ", ")
print(type(of: empty1), type(of: empty2), type(of: empty3), separator: ", ")
```
**Output 1:**
```
[:], [:], [:]
Dictionary<Int, Float>, Dictionary<String, Int>, Dictionary<Double, Int>
```

The values can be accessed in O(1) lookup time using keys, as the unique keys are hashed internally. The values of a `Dictionary` can be accessed via the subscript syntax `[]` which takes key as the argument. Note that a `Dictionary` always returns the value wrapped inside an `Optional` type as the any given may/may not exist in the `Dictionary`. Even if the value is annotated as an `Optional` type, assigning `nil` to a value pointed by a key will remove that key-value pair from the `Dictionary`. If you're doubtful about the existence of a key-value pair in a `Dictionary`, you can give a default value in the subscript syntax `[_ key, default: defaultValue]` which will be used when the given key is not present in the `Dictionary`.

**Example 2:**
```swift
var dict = [1 : "One", 2 : "Two", 3 : "Three", 4 : "Four"]
print(dict)
print(type(of: dict))
dict[3] = nil //Remove 3 : "Three" from dict
print(dict)
print("4 in words is: \(dict[4]!)")
print(dict[5,default:"Word Representation not present"])
```
**Output 2:**
```
[1: "One", 2: "Two", 3: "Three", 4: "Four"]
Dictionary<Int, String>
[1: "One", 2: "Two", 4: "Four"]
4 in words is: Four
Word Representation not present
```

The following example showcases various operations on a `Dictionary`:

**Example 3:**
```swift
let even = "EVEN", odd = "ODD"
var evenOdd : [Int : String] = [2 : even, 3 : even, 9 : odd, 10 : even]
print("Original Dictionary: \(evenOdd)")
evenOdd[3] = odd // Modifying value of key
print("Modified Dictionary: \(evenOdd)")
evenOdd[19] = even // Adding new key-value pair
evenOdd[22] = odd // Adding new key-value pair
print("Modified Dictionary: \(evenOdd)")
evenOdd[19] = nil // Removing key-value pair from Dictionary
evenOdd.removeValue(forKey: 22) // Removing key-value pair from Dictionary
print("Modified Dictionary: \(evenOdd)")
print("Keys of Dictionary in sorted order: \(evenOdd.keys.sorted())") //Access all keys
print("Values of Dictionary: \(evenOdd.values)") // Access all values
print("Key-Value pairs sorted in descending order of Keys: \(evenOdd.sorted(by: >))") // Access all pairs in descending order of keys
print("Shuffled Dictionary: \(evenOdd.shuffled())") // Shuffle key-value pairs of dictionary
let is11Present = evenOdd.contains { k,v in //Checking presence of key:value pair using contains method
    return k==11 && v==odd
}
print("Is 11 : \"ODD\" present in Dictionary ? \(is11Present)")
print("Number of elements in Dictionary: \(evenOdd.count)")
```
**Output 3:**
```
Original Dictionary: [3: "EVEN", 9: "ODD", 2: "EVEN", 10: "EVEN"]
Modified Dictionary: [3: "ODD", 9: "ODD", 2: "EVEN", 10: "EVEN"]
Modified Dictionary: [3: "ODD", 9: "ODD", 19: "EVEN", 22: "ODD", 2: "EVEN", 10: "EVEN"]
Modified Dictionary: [3: "ODD", 9: "ODD", 2: "EVEN", 10: "EVEN"]
Keys of Dictionary in sorted order: [2, 3, 9, 10]
Values of Dictionary: ["ODD", "ODD", "EVEN", "EVEN"]
Key-Value pairs sorted in descending order of Keys: [(key: 10, value: "EVEN"), (key: 9, value: "ODD"), (key: 3, value: "ODD"), (key: 2, value: "EVEN")]
Shuffled Dictionary: [(key: 3, value: "ODD"), (key: 9, value: "ODD"), (key: 10, value: "EVEN"), (key: 2, value: "EVEN")]
Is 11 : "ODD" present in Dictionary ? false
Number of elements in Dictionary: 4
```

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/loops.html">&larr; Loops</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/funclosures.html">Functions and Closures&rarr;</a>
</span>
