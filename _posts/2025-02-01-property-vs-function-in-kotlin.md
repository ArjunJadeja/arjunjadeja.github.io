---
title: Property vs Function in Kotlin
date: 2025-02-01 23:00:00 +0530
categories: [Kotlin Bytes]
tags: [kb, property, function]
image:
  path: /assets/posts/kotlin-bytes/property-vs-function-in-kotlin/thumbnail.svg
  alt: "Property v/s Function"
---

## Definition

**Property**: A property is a characteristic or attribute of an object that holds data. It represents a state or value that belongs to a class or object.

**Function**: A function is a block of code that performs a specific task or action. It represents behavior and can optionally return a value.

## Key Differences

| Aspect | Property | Function |
|--------|----------|----------|
| **Purpose** | Stores data/state | Performs action/computation |
| **Syntax** | No parentheses `()` | Requires parentheses `()` |
| **Access** | Direct access like a field | Called/invoked with `()` |
| **Naming Convention** | Noun (what it is) | Verb (what it does) |
| **Can have parameters** | No | Yes |
| **Typical use** | Get or set values | Execute logic or calculations |

## Property in Kotlin

Properties represent the state of an object. They can have getters and setters.

### Syntax

```kotlin
// Read-only property (val)
val propertyName: Type = initialValue

// Mutable property (var)
var propertyName: Type = initialValue
```

### Examples

```kotlin
class Person {
    val name: String = "Arjun"  // Read-only property
    var age: Int = 25           // Mutable property
}

val person = Person()
println(person.name)  // Access property (no parentheses)
println(person.age)   // Access property (no parentheses)
person.age = 26       // Modify property
```

### Custom Getters and Setters

Properties can have custom logic:

```kotlin
class Rectangle(val width: Int, val height: Int) {
    // Property with custom getter
    val area: Int
        get() = width * height
    
    // Property with custom getter and setter
    var displayName: String = ""
        get() = field.uppercase()
        set(value) {
            field = if (value.isNotEmpty()) value else "Unknown"
        }
}

val rect = Rectangle(5, 10)
println(rect.area)  // 50 (computed each time)
```

## Function in Kotlin

Functions represent behavior or actions that an object can perform.

### Syntax

```kotlin
fun functionName(parameter: Type): ReturnType {
    // function body
    return value
}
```

### Examples

```kotlin
class Calculator {
    // Function with parameters and return value
    fun add(a: Int, b: Int): Int {
        return a + b
    }
    
    // Function without parameters
    fun printMessage(): Unit {
        println("Hello from Calculator")
    }
}

val calc = Calculator()
val result = calc.add(5, 3)  // Call function with parentheses
calc.printMessage()          // Call function with parentheses
```

## How to Identify: Property or Function?

### Look at the Syntax

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)

// Property - no parentheses
numbers.size          // Property
numbers.indices       // Property
numbers.lastIndex     // Property

// Function - has parentheses
numbers.isEmpty()     // Function
numbers.first()       // Function
numbers.sum()         // Function
numbers.contains(3)   // Function
```

### Naming Convention

```kotlin
// Properties (nouns - what it is)
person.name
person.age
rectangle.width
array.size

// Functions (verbs - what it does)
person.getName()      // Gets name
person.updateAge()    // Updates age
rectangle.calculateArea()  // Calculates area
array.isEmpty()       // Checks if empty
```

## When to Use Property vs Function

### Use Property When:

1. **Representing state or characteristic**

```kotlin
class Car {
    val brand: String = "Toyota"
    var speed: Int = 0
}
```

2. **Simple computation without parameters**

```kotlin
class Circle(val radius: Double) {
    val area: Double
        get() = Math.PI * radius * radius
}
```

3. **Accessing or storing data**

```kotlin
val text = "Hello"
println(text.length)  // Property: characteristics of the string
```

### Use Function When:

1. **Performing an action or operation**

```kotlin
class Printer {
    fun printDocument(doc: String) {
        println(doc)
    }
}
```

2. **Computation requires parameters**

```kotlin
class Math {
    fun power(base: Int, exponent: Int): Int {
        return base.toDouble().pow(exponent.toDouble()).toInt()
    }
}
```

3. **Complex logic or side effects**

```kotlin
class Database {
    fun saveData(data: String) {
        // Complex logic to save data
        println("Saving: $data")
    }
}
```

4. **Name implies action**

```kotlin
val numbers = arrayOf(5, 2, 8, 1)
numbers.sort()           // Action: sort the array
numbers.reverse()        // Action: reverse the array
println(numbers.max())   // Action: find maximum
```

## Real-World Analogy

Think of a **Car**:

**Properties** (characteristics):
- `color` - what color is the car
- `speed` - how fast it's going
- `fuelLevel` - how much fuel it has

**Functions** (actions):
- `start()` - start the engine
- `accelerate(amount)` - increase speed
- `brake()` - slow down
- `refuel(liters)` - add fuel

```kotlin
class Car {
    // Properties - state
    var color: String = "Red"
    var speed: Int = 0
    var fuelLevel: Double = 50.0
    
    // Functions - behavior
    fun start() {
        println("Engine started")
    }
    
    fun accelerate(amount: Int) {
        speed += amount
        fuelLevel -= 0.5
    }
    
    fun brake() {
        speed = 0
    }
}

val myCar = Car()
println(myCar.color)    // Access property
println(myCar.speed)    // Access property
myCar.start()           // Call function
myCar.accelerate(20)    // Call function with parameter
```

## Special Case: Functions that Look Like Properties

Some functions in Kotlin don't require parentheses when they take no parameters, but this is rare and not recommended:

```kotlin
// Not common in Kotlin
fun getMessage() = "Hello"

// Can be called without parentheses (not recommended)
// val msg = getMessage

// Should be called with parentheses
val msg = getMessage()
```

**Best Practice**: Always use parentheses when calling functions for clarity.

## Summary

1. **Properties** store data and represent state (nouns) - accessed without parentheses.
2. **Functions** perform actions and represent behavior (verbs) - called with parentheses.
3. Properties can have custom getters/setters but no parameters.
4. Functions can accept parameters and perform complex logic.
5. Use properties for characteristics, functions for actions.

### References

- [Kotlin Official Documentation - Properties](https://kotlinlang.org/docs/properties.html)
- [Kotlin Official Documentation - Functions](https://kotlinlang.org/docs/functions.html)
