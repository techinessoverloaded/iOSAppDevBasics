**Published by Arunprasadh C on 19 May 2022** • *Last Updated on 20 May 2022*

## Closures in Swift
Closures are self-contained blocks of functionality that can be passed around and used in our code (Similar to **Lambda Expressions** of **Java/C/C++/Python/Kotlin**). Closures can capture and store references to any Constants and Variables from the context in which they’re defined. This is known as closing over those Constants and Variables. Swift handles all of the memory management of capturing values. 

Global and nested functions, as introduced in [Functions](https://techinessoverloaded.github.io/iOSAppDevBasics/functions.html), are actually special cases of Closures. Closures take one of three forms:

- **Global functions** are closures that have a name and don’t capture any values.
- **Nested functions** are closures that have a name and can capture values from their enclosing function.
- **Closure expressions** are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.

Swift’s closure expressions have a clean and clear style, with optimizations that encourage brief, clutter-free syntax in common scenarios. These optimizations include:

- Inferring parameter and return value types from context.
- Implicit returns from single-expression closures.
- Shorthand argument names.
- Trailing closure syntax.


<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/functions.html">&larr; Functions</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/.html"> &rarr;</a>
</span>
