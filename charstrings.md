**Published by Arunprasadh C on 27 Apr 2022** • *Last Updated on 28 Apr 2022*

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

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html">&larr; </a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
