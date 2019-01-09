## Dart

### Some important concepts of Dart

- Evertthing is an object, even a number, function and **null**.
- Dart can infer types, if no types is expected, use **dynamic**
- Generic types
- Dart support top-level objects and OO objects.
- identifier with a start of **_** is private.

### final and const

- **final** objects can only be assigned once.
- **const** is a compile-time constant.

```dart
const bar = 100
const bar1 = bar * 2 // a valid const in dart
```

### Built-in types

- numbers
- strings
- booleans
- lists
- maps
- runes: The UTF-32 code points of a string.
- symbols

### Functions

Function is also an object and it can also be used as a parameter.

- optional named parameters.
- optional positional parameters.
- default parameter values.

Every APP should have a **main** function for the entry point.

Cascade notation(..)  
	Allow to make a sequence of operations on a same object.

```dart
var button = a(b)
button.text = "yes"
button.setOnClickListener(this)

var button = a(b)
	..text = "yes"
	..setOnClickListener(this)
```

### Error handling

**Dart** provides **error** and **Exception**, but you can throw everything in Dart.

```
throw FormatException('This is a format exception.') // Throw an exception
throw "hahah" // Throw some objects
```

To capture something, use try{} catch {} structure in the code.  
