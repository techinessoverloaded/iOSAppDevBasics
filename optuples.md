**Published by Arunprasadh C on 25 Apr 2022** • *Last Updated on 25 Apr 2022*

## Tuples and Optionals in Swift

### Tuples
Tuples are used to group multiple values in a single compound value. The values can be of different Data Types. Type Annotation cannot be used with Tuples as they are statically defined. The basic syntax of `Tuple` is as follows:
```swift
var TupleName = (value1, value2,… any number of values) // for Variables
```
**OR**
```swift
let TupleName = (value1, value2,… any number of values) // for Constants
```
The elements of a `Tuple` can be accessed using Index value starting from `0` till `n-1` where `n` is the number of elements in the `Tuple`.

**Example :**
```swift
let error = (404, "Not Found")
print("The error code is : \(error.0)")
print("The error description is : \(error.1)")
```

**Output :**
```
The error code is : 404
The error description is : Not Found
```

I have used **String Interpolation** in the above example. It will be covered in the Next Topic Page.

### Optionals

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/varconst.html">&larr; Variables, Literals and Constants in Swift</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
