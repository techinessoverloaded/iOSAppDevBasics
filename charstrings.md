**Published by Arunprasadh C on 27 Apr 2022** • *Last Updated on 29 Apr 2022*

## Characters and Strings in Swift
### Characters
In Swift, Characters are represented via Single character String Literals (character within double quotes `" "`) unlike other languages where Characters are represented via character within single quotes `' '`. As characters too are represented by String literals, to make a variable as `Character` Type, we have to explicitly provide Type Annotation as `Character` or if we want to avoid Type Annotation, we have to use the `Character` constructor and also ensure that there are no more than one character in the String Literal.

**Example :**
```swift
var char = "a"
var char2: Character = "a"
var char3 = Character("அ")
print(type(of: char))
print(type(of: char2))
print(type(of: char3))
```
**Output :**
```
String
Character
Character
```
You can observe that when the variable is not type annotated as a `Character`, it is considered as a `String`. Swift `Character` is compliant with **Unicode** encoding (like Java, unlike C/C++), and hence supports a a very large collection of **Unicode** characters. So, multiple language characters and even emojis like ♥ can be used with Swift. Empty `Character` Literals can be specified with `""`.

### Strings
In Swift, a `String` is an ordered collection of `Character`s. A `String` can be initialized with either a String Literal or with the `String` constructor which takes a literal as a parameter.

**Example :**
```swift
var str = "a"
var str2: String = "Hello"
let str3 = String(45.5)
print(type(of: str),type(of: str2),type(of: str3),separator: ", ")
print(str, str2, str3, separator: ", ")
```
**Output :**
```
String, String, String
a, Hello, 45.5
```

We can also declare Multiline Strings using Multiline String Literals, which are represented by text within triple quotes(""").

**Example :**
```swift
var paragraph: String = """
This is a paragraph.

    This is a new paragraph.
"""
print(paragraph)
```
**Output :**
```
This is a paragraph.

    This is a new paragraph.
```

If we want to avoid line breaks in the `String` value, we can use the `\` character within Multiline Literals.

**Example :**
```swift
var paragraph: String = """
This is a paragraph.\
\
    This is not a new paragraph.
"""
print(paragraph)
```
**Output :**
```
This is a paragraph.    This is not a new paragraph.
```

#### String Indices
If you are a C/C++/Python developer, you would be familiar with getting characters of a String using the indexing/subscript operator `[]` with Integer indices. If you are a Java developer, you would be familiar with using the `String.charAt()` method to obtain the character at the specific Integer Index. 

##### Integer Indices are not allowed in Swift for Strings !
In Swift, neither of these approaches are followed. Rather, a modified version of the C/C++/Python Character access approach is used. As we saw earlier, Swift allows Unicode characters to be used. Swift also allows combining of Unicode characters graphically. For example, the Letter `é` is represented in Unicode as `\u{E9}`. It can be used as such in Swift too. Additionally, Swift can also combine the Unicode characters of `e` (`\u{65}`) and "` ́`" (`\u{301}`) graphically when used in succession, to obtain the character `é` (as `\u{65}\u{301}`). Hence, different characters can require different amounts of memory to store, so in order to determine which `Character` is at a particular position, you must iterate over each Unicode scalar from the start or end of that `String`. For this reason, Swift strings cannot be indexed by integer values.

##### How to access the Characters of a String ?
Swift uses a `struct` called `String.Index` for storing the position of each `Character` of the `String`. We can use the subscript operator `[]` with `String.Index` values to access the characters of a `String`. The starting Index of the `String` can be accessed by using `String.startIndex` and using values before `startIndex` will cause an error. The ending Index, that is, the Index value after the last `Character` can be accessed via `String.endIndex` and using values after `endIndex` will cause an error. 

**Example :**
```swift
var str : String = "Poke"+"\u{301}mon"
print(str)
print(str[str.startIndex])
print(str[str.index(after: str.startIndex)])
print(str[str.index(str.startIndex, offsetBy: 2)])
print(str[str.index(str.startIndex, offsetBy: 3)])
print(str[str.index(str.startIndex, offsetBy: 4)])
print(str[str.index(str.startIndex, offsetBy: 5)])
print(str[str.index(before: str.endIndex)])
```
**Output :**
```
Pokémon
P
o
k
é
m
o
n
```

We can use the `String.indices` property to get a collection of indices which can be iterated and used.

**Example :**
```swift
var str : String = "Poke"+"\u{301}mon"
print(str)
for x in str.indices {
    print(str[x])
}
```

**Output :**
```
Pokémon
P
o
k
é
m
o
n
```

We can also simply iterate the Characters of a `String` with a `for`-`in` loop.

**Example :**
```swift
var str : String = "Poke\u{301}mon"
print(str)
for c in str
{
    print(c)
}
```
**Output :**
```
Pokémon
P
o
k
é
m
o
n
```
#### String Concatenation
Strings can be concatenated using `+` operator or can be concatenated and reassigned using `+=` operator or the `append()` function of `String` can also be used for concatenation in Swift.

**Example :**
```swift
var greeting = "Good " + "Morning !"
greeting += " Hope you are doing well !"
greeting.append(contentsOf: "\nI will call you in the evening.")
print(greeting)
```
**Output :**
```
Good Morning ! Hope you are doing well !
I will call you in the evening.
```

#### String Comparison
Strings can be compared by using the `==` operator or by using the `elementsEqual()` function of `String`.

**Example :**
```swift
var greeting = "Hello"
var greeting2 = "Hello"
var greeting3 = "HELLO"
print(greeting.elementsEqual(greeting2))
print(greeting == greeting3)
```

**Output :**
```
true
false
```

#### String Interpolation
String Interpolation in Swift allows us to include variables and constants inside a `String` value (You can find it in `printf()` in other languages).
String Interpolation can be done using the `\` character followed by the variable or constant name enclosed within parantheses `()`.

**Example: **
```swift
var temperature = 35
print("Today, the Temperature in Chennai is over \(temperature)°C")
```

**Output :**
```
Today, the Temperature in Chennai is over 35°C
```

#### Other useful functions and property in `String` Type

| Name | Function/Properties | Description |
| --- | --- | --- |
| `count` | Property | Gets the number of `Characters` present in the `String` |
| `isEmpty` | Property | Has the value `true` if the `String` is Empty |
| `uppercased()` | Function | Returns the upper case version of the `String` |
| `lowercased()` | Function | Returns the lower case version of the `String` |
| `hasPrefix()` | Function | Returns `true` if the `String` starts with the given Prefix |
| `hasSuffix()` | Function | Returns `true` if the `String` ends with the given Suffix |
| `write()` | Function | Write the `String` value to a File or Stream |
| `insert()` | Function | Insert a `Character` into the `String` at given `String.Index` |
| `write()` | Function | Write the `String` value to a File or Stream |
| `replaceSubrange()` | Function | Replace the given range of `String.Index` with given `Character`s |
| `remove()`, `removeAll`, `removeFirst()`, `removeLast()`, `removeSubrange()` | Function(s) | Used for removing `Character` or `Substring` from `String` |
| `contains()` | Function | Returns `true` if the `String` contains the given `Character` |

Now, we can move on to learn about Tuples and Optionals in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/datatypes.html">&larr; Data Types available in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/optuples.html">Tuples and Optionals in Swift &rarr;</a>
</span>
