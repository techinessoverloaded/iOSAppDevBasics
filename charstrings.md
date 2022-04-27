**Published by Arunprasadh C on 27 Apr 2022** • *Last Updated on 27 Apr 2022*

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

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html">&larr; </a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
