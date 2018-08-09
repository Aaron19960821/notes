## Kotlin

### The philosophy of kotlin

- Pragmatic: Kotlin is a practical language designed to solve real-world problems.
- Concise: Kotlin has a lot of shared library. The syntax of Kotlin is clear enough.
- Safe: To prevent the Kotlin app have a lot of errors, the complier will have check more things at compliation stage.
- Interoperable: Kotlin users can use all APIs in Java.

### Basic

#### Hello World

See the following code:  

```kotlin
fun main(args: Array<String>) {
    println("Hello, World")
}
```

**fun** to declare a new function. The function can be written standalone a class.  

A more complete function declaration is here below:  

```kotlin
fun max(l: Int, r:Int): Int {
    return if(a > b) a else b
}
```

#### Statement and expression

- Statement: Do not have a return value, all top elements in a enclosing block is a statement.
- expression: Expression have a return value.

#### Variables

A variable declaration is here below:  

```kotlin
val answer: Int
var answer2: Int
```

**val**: Immutable references, the variable can not be changed.  
**var**: Mutable references, the variable can be changed.  
Note that if **val** is a reference, then the reference itself can not be changed while the object may be changed.  

#### Properties

In Kotlin's class, **val** is used to declare a read-only property and **var** to declare a writable variable.  

```kotlin
class Person (
    val name: String
    var isMarried: Boolean
)
```

Obviously, we can implement a custom accessor:  

```kotlin
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
    get() {
        return height == width
    }
}
```
