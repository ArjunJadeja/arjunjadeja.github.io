---
title: Arrays in Kotlin
date: 2024-10-28 23:00:00 +0530
categories: [Problem Solving, Data Structures]
tags: [array]
image:
  path: /assets/posts/arrays-in-kotlin/thumbnail.svg
  alt: "Array Diagram"
---

## Definition

An Array is a mutable and linear collection of same data type elements, each having its own identifier index which starts from `0` and goes upto `n - 1`. where `n` is size of an array.

Array has fixed size, set during declaration and we cannot add or remove element later.

Arrays are mutable, we can assign or change value for any index after declaration.

## Working with Arrays

### Creating an array

There are various ways to create an array. Let's look into it one by one:

#### Using Array constructor `Array(size) { init }`

Creates an array of a specific size with a lambda to initialize values:

```kotlin
val fiveZeros = Array(5) { 0 } // [0, 0, 0, 0, 0]
val squares = Array(5) { i -> i * i } // [0, 1, 4, 9, 16]
```

#### Using `arrayOf()` function

This creates an array with specified elements:

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5) // Array<Int>
val mixed = arrayOf(1, "two", 3.0) // Array<Any>
```

#### Using `arrayOfNulls<T>(size)` function

This creates an array with default null values:

```kotlin
val nulls = arrayOfNulls<String>(3) // [null, null, null]
```

#### Using `emptyArray()` function

Creates an empty array. Useful in scenarios where we need to return array or setting default empty array in function parameters:

```kotlin
val arr = emptyArray() // []

fun getUsers(): Array<String> {
  val usersFromDb = loadFromDatabase()
  return if (usersFromDb.isEmpty()) emptyArray() else usersFromDb.toTypedArray()
}

fun printNames(names: Array<String> = emptyArray()) {
  for (name in names) println(name)
}
```

### Access array element

#### Using Index Operator `[]`

```kotlin
val numbers = arrayOf(10, 20, 30, 40)
val first = numbers[0] // 10
val third = numbers[2] // 30
```

#### Using `get()` Method

```kotlin
val second = numbers.get(1) // 20
```

#### Safe Access Methods

```kotlin
val element = numbers.getOrNull(10) // null (index out of bounds)
val element = numbers.getOrElse(10) { 0 } // 0 (default value)
```

#### Getting First/Last Elements

```kotlin
val first = numbers.first() // 10
val last = numbers.last() // 40
val firstOrNull = numbers.firstOrNull() // Safe version
```

### Modify Array element

#### Using Index Operator `[]`

```kotlin
val numbers = arrayOf(10, 20, 30, 40)
numbers[0] = 100 // [100, 20, 30, 40]
numbers[2] = 300 // [100, 20, 300, 40]
```

#### Using `set()` Method

```kotlin
numbers.set(1, 200) // [100, 200, 300, 40]
```

#### Modifying Multiple Elements

```kotlin
for (i in numbers.indices) {
  numbers[i] = numbers[i] * 2
}

// Using forEachIndexed
numbers.forEachIndexed { index, value ->
  numbers[index] = value + 10
}
```

### Using spread operator `*` with array

The spread operator * in Kotlin is used to "unpack" an array into individual elements.

#### Passing Array Elements as Varargs

```kotlin
fun printNumbers(vararg numbers: Int) {
  numbers.forEach { println(it) }
}

val array = intArrayOf(1, 2, 3, 4, 5)
printNumbers(*array)  // Unpacks array into individual arguments

// Without the spread operator *, we get a compilation error because the function expects individual arguments, not an array.
```

#### Combining Arrays

```kotlin
val first = arrayOf(1, 2, 3)
val second = arrayOf(4, 5, 6)
val combined = arrayOf(*first, *second)  // [1, 2, 3, 4, 5, 6]
```

#### Mixing Array Elements with Individual Values

```kotlin
val numbers = arrayOf(2, 3, 4)
val result = arrayOf(1, *numbers, 5, 6)  // [1, 2, 3, 4, 5, 6]
```

#### Note

1. The spread operator only works with arrays, not with collections like List or Set.
2. It creates a copy of the elements, not a reference.

## Primitive Arrays in Kotlin

Primitive type arrays in Kotlin are specialized array types that store primitive values directly in memory, without boxing them into objects. This makes them more memory-efficient and faster than generic arrays.

#### Creating Primitive Arrays

```kotlin
// Using factory functions with values
val booleans = booleanArrayOf(true, false, true)
val bytes = byteArrayOf(1, 2, 3, 4)
val shorts = shortArrayOf(100, 200, 300)
val ints = intArrayOf(1, 2, 3, 4, 5)
val longs = longArrayOf(1000L, 2000L, 3000L)
val floats = floatArrayOf(1.5f, 2.5f, 3.5f)
val doubles = doubleArrayOf(1.5, 2.5, 3.5)
val chars = charArrayOf('K', 'o', 't', 'l', 'i', 'n')

// Using constructors with size and initializer
val zeros = IntArray(5)                    // [0, 0, 0, 0, 0]
val squares = IntArray(5) { i -> i * i }   // [0, 1, 4, 9, 16]
val filled = DoubleArray(3) { 1.0 }        // [1.0, 1.0, 1.0]
```

#### Table of all primitive array types

| Kotlin Type | Java Equivalent | Element Type | Creation Function | Constructor | Example |
|-------------|----------------|--------------|-------------------|-------------|---------|
| `BooleanArray` | `boolean[]` | `Boolean` | `booleanArrayOf()` | `BooleanArray(size)` | `booleanArrayOf(true, false)` |
| `ByteArray` | `byte[]` | `Byte` | `byteArrayOf()` | `ByteArray(size)` | `byteArrayOf(1, 2, 3)` |
| `ShortArray` | `short[]` | `Short` | `shortArrayOf()` | `ShortArray(size)` | `shortArrayOf(10, 20, 30)` |
| `IntArray` | `int[]` | `Int` | `intArrayOf()` | `IntArray(size)` | `intArrayOf(1, 2, 3)` |
| `LongArray` | `long[]` | `Long` | `longArrayOf()` | `LongArray(size)` | `longArrayOf(100L, 200L)` |
| `FloatArray` | `float[]` | `Float` | `floatArrayOf()` | `FloatArray(size)` | `floatArrayOf(1.5f, 2.5f)` |
| `DoubleArray` | `double[]` | `Double` | `doubleArrayOf()` | `DoubleArray(size)` | `doubleArrayOf(1.5, 2.5)` |
| `CharArray` | `char[]` | `Char` | `charArrayOf()` | `CharArray(size)` | `charArrayOf('a', 'b')` |

## Properties

- `size`: Returns the number of elements in the array.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
println(numbers.size) // 5
```

- `indices`: Returns the range of valid indices for the array.

```kotlin
val numbers = arrayOf(10, 20, 30)
println(numbers.indices) // 0..2
for (i in numbers.indices) {
    println(numbers[i])
}
```

- `lastIndex`: Returns the index of the last element in the array.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
println(numbers.lastIndex) // 4
```

## Functions

- `isEmpty()`: Checks if array is empty.

```kotlin
val empty = emptyArray<Int>()
println(empty.isEmpty()) // true

val numbers = arrayOf(1, 2, 3)
println(numbers.isEmpty()) // false
```

- `toTypedArray()`: Converts a primitive array to an object array or a collection to a typed array.

```kotlin
val intArray = intArrayOf(1, 2, 3)
val objectArray = intArray.toTypedArray() // Array<Int>

val list = listOf(1, 2, 3)
val array = list.toTypedArray() // Array<Int>
```

- `joinToString()`: Converts array elements into a single string with optional separator, prefix, and suffix.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
println(numbers.joinToString()) // 1, 2, 3, 4, 5
println(numbers.joinToString(separator = " - ")) // 1 - 2 - 3 - 4 - 5
println(numbers.joinToString(prefix = "[", postfix = "]")) // [1, 2, 3, 4, 5]
println(numbers.joinToString(separator = ", ", prefix = "{", postfix = "}")) // {1, 2, 3, 4, 5}
```

- `contentToString()`: Returns a string representation of the array contents.

```kotlin
val numbers = intArrayOf(1, 2, 3)
println(numbers.contentToString()) // [1, 2, 3]
```

- `sort()`: Sorts the array in ascending order (in-place).

```kotlin
val numbers = intArrayOf(5, 2, 8, 1, 9)
numbers.sort()
println(numbers.contentToString()) // [1, 2, 5, 8, 9]
```

- `sortDescending()`: Sorts the array in descending order (in-place).

```kotlin
val numbers = intArrayOf(5, 2, 8, 1, 9)
numbers.sortDescending()
println(numbers.contentToString()) // [9, 8, 5, 2, 1]
```

- `reverse()`: Reverses the order of elements in the array (in-place).

```kotlin
val numbers = intArrayOf(1, 2, 3, 4, 5)
numbers.reverse()
println(numbers.contentToString()) // [5, 4, 3, 2, 1]
```

- `contains()`: Checks if an element exists in the array.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
println(numbers.contains(3)) // true
println(numbers.contains(10)) // false
println(3 in numbers) // true (alternative syntax)
```

- `sum()`: Returns the sum of all elements (for numeric arrays).

```kotlin
val numbers = intArrayOf(1, 2, 3, 4, 5)
println(numbers.sum()) // 15
```

- `average()`: Returns the average of all elements (for numeric arrays).

```kotlin
val numbers = intArrayOf(2, 4, 6, 8, 10)
println(numbers.average()) // 6.0
```

- `max()` and `min()`: Returns the maximum and minimum element.

```kotlin
val numbers = intArrayOf(5, 2, 8, 1, 9)
println(numbers.max()) // 9
println(numbers.min()) // 1
```

- `filter()`: Returns a list containing only elements matching the given predicate.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5, 6)
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers) // [2, 4, 6]
```

- `map()`: Returns a list containing the results of applying the given transform function.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
val doubled = numbers.map { it * 2 }
println(doubled) // [2, 4, 6, 8, 10]
```

- `forEach()`: Performs the given action on each element.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
numbers.forEach { println(it) }
```

- `forEachIndexed()`: Performs the given action on each element with its index.

```kotlin
val numbers = arrayOf(10, 20, 30)
numbers.forEachIndexed { index, value ->
    println("Index $index: $value")
}
// Output:
// Index 0: 10
// Index 1: 20
// Index 2: 30
```

## When to use Array

Arrays in Kotlin are useful in specific scenarios:

- **Fixed-size collections**: When you know the exact number of elements and it won't change.

```kotlin
val daysOfWeek = arrayOf("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
```

- **Performance-critical code**: Arrays, especially primitive arrays, offer better performance than collections.

```kotlin
val largeDataSet = IntArray(1_000_000) // More efficient than List<Int>
```

- **Interoperability with Java**: When working with Java code that expects arrays.

```kotlin
// Java method: public void processData(int[] data)
val data = intArrayOf(1, 2, 3)
javaObject.processData(data)
```

- **Working with varargs**: When you need to pass multiple arguments using spread operator.

```kotlin
fun printAll(vararg items: String) {
    items.forEach { println(it) }
}

val names = arrayOf("Alice", "Bob", "Charlie")
printAll(*names)
```

- **Multi-dimensional data structures**: For matrices or grids.

```kotlin
val matrix = Array(3) { IntArray(3) } // 3x3 matrix
```

**Note**: For most cases, prefer using Kotlin collections like `List`, `MutableList`, `Set`, etc., as they are more flexible and provide better APIs. Use arrays only when you have specific requirements like those mentioned above.

## Summary

1. Arrays in Kotlin are mutable (you can change elements), but their size is fixed.
2. Array indices start at `0` and go up to `array.size - 1`.
3. Accessing an invalid index throws `ArrayIndexOutOfBoundsException`.
4. Use safe access methods like `getOrNull()` when the index might be invalid.
5. Primitive arrays (`IntArray`, `DoubleArray`, etc.) are more memory-efficient than object arrays (`Array<Int>`, `Array<Double>`, etc.).
6. The spread operator `*` is used to unpack arrays into individual elements, useful for varargs and combining arrays.
7. Use `toTypedArray()` to convert collections or primitive arrays to object arrays.
8. For most use cases, prefer Kotlin collections over arrays for better flexibility and API support.

### References

- [Kotlin Official Documentation - Arrays](https://kotlinlang.org/docs/arrays.html)
