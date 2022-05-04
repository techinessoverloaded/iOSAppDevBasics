**Published by Arunprasadh C on 04 May 2022** • *Last Updated on 04 May 2022*

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

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/operators.html">&larr; Operators</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/loops.html">Loops &rarr;</a>
</span>
