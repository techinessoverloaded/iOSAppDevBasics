**Published by Arunprasadh C on 02 June 2022** • *Last Updated on 02 June 2022*

## Type Casting in Swift
Type casting is a way to check the type of an instance, or to treat that instance as a different superclass or subclass from somewhere else in its own class hierarchy.

Type casting in Swift is implemented with the `is` and `as` operators. These two operators provide a simple and expressive way to check the type of a value or cast a value to a different type.

You can also use type casting to check whether a type conforms to a protocol. Type casting operators require `class` instances only as only classes support inheritance.

### Checking Type
The type check operator `is` is used to check the type of an instance. It returns `true` if the instance is of the given type, else it returns `false`. The following example's classes are used in subsequent examples too.

**Example 1:**
```swift
class MediaItem
{
    var name: String
    init(name: String)
    {
        self.name = name
    }
}

class Movie: MediaItem
{
    var director: String
    init(name: String, director: String)
    {
        self.director = director
        super.init(name: name)
    }
}

class Song: MediaItem
{
    var artist: String
    init(name: String, artist: String)
    {
        self.artist = artist
        super.init(name: name)
    }
}

let library: [MediaItem] = [
    Movie(name: "Casablanca", director: "Michael Curtiz"),
    Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
    Movie(name: "Citizen Kane", director: "Orson Welles"),
    Song(name: "The One And Only", artist: "Chesney Hawkes"),
    Song(name: "Never Gonna Give You Up", artist: "Rick Astley")
]

var movieCount = 0
var songCount = 0

for item in library
{
    if item is Movie
    {
        movieCount += 1
    }
    else if item is Song
    {
        songCount += 1
    }
}

print("Media library contains \(movieCount) movies and \(songCount) songs")
```
**Output 1:**
```
Media library contains 2 movies and 3 songs
```

### Downcasting
A constant or variable of a certain class type may actually refer to an instance of a subclass behind the scenes. Where you believe this is the case, you can try to downcast to the subclass type with a type cast operator (`as?` or `as!`).

Because downcasting can fail, the type cast operator comes in two different forms. The conditional form, `as?`, returns an optional value of the type you are trying to downcast to. The forced form, `as!`, attempts the downcast and force-unwraps the result as a single compound action.

Use the conditional form of the type cast operator (`as?`) when you aren’t sure if the downcast will succeed. This form of the operator will always return an optional value, and the value will be `nil` if the downcast was not possible. This enables you to check for a successful downcast.

Use the forced form of the type cast operator (`as!`) only when you are sure that the downcast will always succeed. This form of the operator will trigger a runtime error if you try to downcast to an incorrect class type.

**Example 1.1:**
```swift
for item in library
{
    if let movie = item as? Movie
    {
        print("Movie: \(movie.name), dir. \(movie.director)")
    }
    else if let song = item as? Song
    {
        print("Song: \(song.name), by \(song.artist)")
    }
}
```
**Output 1.1:**
```
Movie: Casablanca, dir. Michael Curtiz
Song: Blue Suede Shoes, by Elvis Presley
Movie: Citizen Kane, dir. Orson Welles
Song: The One And Only, by Chesney Hawkes
Song: Never Gonna Give You Up, by Rick Astley
```

**NOTE:** Casting doesn’t actually modify the instance or change its values. The underlying instance remains the same; it’s simply treated and accessed as an instance of the type to which it has been cast.

### Upcasting
Upcasting in Swift can be done implicitly. Simply, type annotation is used for the purpose. Also, the `type(of:)` method will return the type of variable as its actual type only even after upcasting (See the above **NOTE** for the reason), but only the properties and methods common to both the superclass and subclass can be accessed because of Upcasting. Moreover, explicit upcasting can also be done by using `as` operator.

**Example 1.2:**
```swift
let movie: MediaItem = Movie(name: "Jurassic Park", director: "Steven Spielberg") // Implicit Upcasting
print(type(of: movie))
print(movie is MediaItem)
print(movie is Movie)
print((movie as! Movie).director) // Downcasting to access Movie Director

let song: MediaItem = Song(name: "Un Mela", artist: "Jitin") as MediaItem // Explicit Typecasting
print(type(of: song))
print(song is MediaItem)
print(song is Song)
print((song as! Song).artist) // Downcasting to access Song Artist
```
**Output 1.2:**
```
Movie
true
true
Steven Spielberg
Song
true
true
Jitin
```

Now that we have seen about Type Casting in Swift, we can move on to see about Extensions in Swift.

<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/index.html">&larr; Back to Index</a>
<br>
<span style="float: left">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/enums.html">&larr; Enumerations</a>
</span>
<span style="float: right">
<a href="https://techinessoverloaded.github.io/iOSAppDevBasics/extensions.html">Extensions &rarr;</a>
</span>
