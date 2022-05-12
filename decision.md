**Published by Arunprasadh C on 04 May 2022** • *Last Updated on 12 May 2022*

## Decision-making Constructs in Swift
Decision-making constructs are used to control the flow of execution in a program based on some condition. Swift provides the following Decision-making Constructs:

### `if` Statement
The `if` Statement executes a block of code when the given condition evaluates to `true`.

**Syntax :**
```swift
if(condition)
{
// block of code
}
```

**Example :**
```swift
var age = 22
if(age >= 18 && age <= 100)
{
    print("You're eligible to vote !")
}
```

**Output :**
```
You're eligible to vote !
```
### `if`-`else` Statement
The `if`-`else` Statement executes a block of code when the given condition evaluates to `true` or an alternate block of code when the given condition evaluates to `false`.

**Syntax :**
```swift
if(condition)
{
// block of code
}
else
{
// alternate block of code
}
```

**Example :**
```swift
var age = 16
if(age >= 18 && age <= 100)
{
    print("You're eligible to vote !")
}
else
{
    print("You're not eligible to vote !")
}
```

**Output :**
```
You're not eligible to vote !
```

### `if`-`else if`-`else` Statement
The `if`-`else if`-`else` Statement executes a block of code when the given condition evaluates to `true` or an alternate block of code when an alternate condition evaluates to `true`. If none of the conditions are met, the `else` block code is executed.

**Syntax :**
```swift
if(condition1)
{
// block of code
}
else if(condition2)
{
// alternate code block 1
}
...
else if(conditionN)
{
// alternate code block N-1
}
else
{
// alternate code block N
}
```

**Example :**
```swift
var age = -9
if(age >= 18 && age <= 100)
{
    print("You're eligible to vote !")
}
else if(age < 1 || age > 100)
{
    print("Invalid Age !")
}
else
{
    print("You're not eligible to vote !")
}
```

**Output :**
```
Invalid Age !
```

### Nested `if` Statement
The Nested `if` Statement transfers the control to the inner `if` statement when the condition provided in the outer `if` statement is met. The control flow is then handled by the inner `if` statement.

**Syntax :**
```swift
if(condition1)
{
if(condition2)
{
// block of code
}
else
{
// alternate block of code
}
}
else
{
// alternate code block
}
```

**Example :**
```swift
var num = 6
if(num >= 0)
{
    if(num == 0)
    {
        print("Zero !")
    }
    else
    {
        print("Positive Number !")
    }
}
else
{
    print("Negative Number !")
}
```

**Output :**
```
Positive Number !
```


### `guard` Statement
In Swift, we use the `guard` statement to transfer program control out of scope when certain conditions are not met. The `guard` statement is similar to the `if` statement with one major difference. The `if` statement runs when a certain condition is met. However, the `guard` statement runs when a certain condition is not met. A control statement is mandatory in `guard` block.

**Syntax :**
```swift
guard expression else 
{
  //block of code
  //control statement: return, break, continue or throw.
}
```

You can notice control statements in the above syntax. The `return` statement is used to return a value and/or transfer the control outside a function block. The `break` statement is used to terminate a loop. The `continue` statement is used to skip the current iteration and move on to the next iteration. The `throw` statement is used to throw an Error.

**Example :**
```swift
var i = 1
while (i <= 20)
{
  // guard condition to check the odd number
  guard i % 2 != 0 else
  {
    i += 1
    continue
  }
  print(i, terminator: ", ")
  i += 1
}
```

**Output :**
```
1, 3, 5, 7, 9, 11, 13, 15, 17, 19,
```

### The `if`-`let` Statement and `guard`-`let` Statement
We have seen about `if`-`let` Statement in [Optionals and Tuples](https://techinessoverloaded.github.io/iOSAppDevBasics/optuples.html). The `guard`-`let` Statement can also be used for the same purpose.

### The `switch` Statement
The `switch` statement allows us to execute a block of code among many alternatives. The code block of the `case` which is matched is executed. When there is no match for any `case`, the `default` case code block is executed. An explicit `break` statement is not required for each case (unlike C/C++/Java), as the execution of the `switch` statement ends as soon as a `case` matched block is executed. However, if we want to force the control to fall through to other cases (equivalent to not using `break` in C/C++/Java), we can use the `fallthrough` statement. Unlike Java, a range/comma separated values can be used in `case` label.

**Syntax :**
```swift
switch (expression)  
{
  case value1:
    // statements 
    // optional fallthrough
  case value2:
    // statements
    // optional fallthrough
  ...  
  default:
    // statements
}
```

**Example 1:**
```swift
let ageGroup = 22

switch ageGroup
{
  case 0...16:
    print("Child")

  case 17...30:
    print("Young Adults")

  case 31...45:
    print("Middle-aged Adults")
    
  default:
    print("Old-aged Adults")
}
```

**Output 1:**
```
Young Adults
```

**Example 2:**
```swift
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe 
{
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
    
default:
    description += " an integer."
}
print(description)
```

**Output 2:**
```
The number 5 is a prime number, and also an integer.
```

Let's see a complex example showcasing optional tuple, array of tuples, random array value and pattern matching.

**Example 3:**
```swift
let valueRepo: [(Int, String)] = [(5, "Kris"), (6, "Shiv")]
var tupOpt: (Int, String)? = nil
print(type(of: tupOpt))
var shouldContinue = true
while shouldContinue
{
switch tupOpt
{
case .none:
    print("Found nil ! Assigning value...")
    tupOpt = valueRepo.randomElement()
    // fallthrough can't be used here as swift compiler doesn't allow to fallthrough nil case. hence shouldContinue boolean is used
case .some(let (age, name)):
    print("\(name) is a \(age) year old boy")
    shouldContinue = false
}
}
```

**Output 3:**
```
Optional<(Int, String)>
Found nil ! Assigning value...
Shiv is a 6 year old boy
```

Now, as we have seen about Decision-making Constructs, let's move on to see about Loops in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/operators.html">&larr; Operators</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/loops.html">Loops &rarr;</a>
</span>
