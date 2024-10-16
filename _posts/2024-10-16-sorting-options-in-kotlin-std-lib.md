---
title: Sorting options in Kotlin Standard Library
date: 2024-10-16 13:00:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics, sorting]
---

Sorting is a fundamental operation in problem-solving. Kotlin provides a rich set of sorting functions in its standard library, making it easy to sort various data structures efficiently.

## Sorting Functions: sort() vs sorted()

Kotlin offers two main approaches to sorting: `sort()` and `sorted()`.

- `sort()`: Modifies the original collection in-place.
- `sorted()`: Returns a new sorted collection, leaving the original unchanged.

Example:
```kotlin
val numbers = mutableListOf(3, 1, 4, 1, 5, 9, 2, 6, 5)
numbers.sort() // Modifies 'numbers' in-place
println(numbers) // [1, 1, 2, 3, 4, 5, 5, 6, 9]

val originalList = listOf(3, 1, 4, 1, 5, 9, 2, 6, 5)
val sortedList = originalList.sorted() // Returns a new sorted list
println(originalList) // [3, 1, 4, 1, 5, 9, 2, 6, 5] (unchanged)
println(sortedList)   // [1, 1, 2, 3, 4, 5, 5, 6, 9]
```

## Sorting Different Data Structures

### Arrays

```kotlin
val array = arrayOf(5, 2, 8, 1, 9)
array.sort() // In-place sorting
println(array.contentToString()) // [1, 2, 5, 8, 9]

val sortedArray = array.sortedArray() // Returns new sorted array
println(sortedArray.contentToString()) // [1, 2, 5, 8, 9]
```

### Lists

```kotlin
val list = mutableListOf(5, 2, 8, 1, 9)
list.sort() // In-place sorting
println(list) // [1, 2, 5, 8, 9]

val immutableList = listOf(5, 2, 8, 1, 9)
val sortedList = immutableList.sorted() // Returns new sorted list
println(sortedList) // [1, 2, 5, 8, 9]
```

### Sets

```kotlin
val set = setOf(5, 2, 8, 1, 9)
val sortedSet = set.sorted() // Returns a sorted List
println(sortedSet) // [1, 2, 5, 8, 9]
```

### Maps

```kotlin
val map = mapOf(3 to "three", 1 to "one", 2 to "two")
val sortedByKey = map.toSortedMap() // Sorts by key
println(sortedByKey) // {1=one, 2=two, 3=three}

val sortedByValue = map.entries.sortedBy { it.value }
println(sortedByValue) // [(1, one), (3, three), (2, two)]
```

### Strings

```kotlin
val str = "kotlin"
val sortedString = str.toCharArray().sorted().joinToString("")
println(sortedString) // "iklnot"
```

## Customizing Sort Order

### Using sortBy and sortWith

```kotlin
data class Person(val name: String, val age: Int)

val people = listOf(
    Person("Alice", 29),
    Person("Bob", 31),
    Person("Charlie", 30)
)

val sortedByName = people.sortedBy { it.name }
println(sortedByName) // [Alice, Bob, Charlie]

val sortedByAgeDesc = people.sortedWith(compareByDescending { it.age })
println(sortedByAgeDesc) // [Bob, Charlie, Alice]
```

## Kotlin Syntax Sugars for Sorting

1. `sortedByDescending`: Sorts in descending order based on a selector function.
   ```kotlin
   val descNumbers = numbers.sortedByDescending { it }
   ```

2. `sortedWith`: Uses a custom comparator.
   ```kotlin
   val customSort = numbers.sortedWith { a, b -> a % 2 - b % 2 }
   ```

3. `reversed()`: Reverses the order of a collection.
   ```kotlin
   val reversedList = numbers.sorted().reversed()
   ```

## Performance Considerations

- In-place sorting (`sort()`) is generally more memory-efficient for large collections.
- `sorted()` creates a new collection, which may impact memory usage for very large datasets.
- Kotlin's standard library sorting functions use TimSort, which has O(n log n) time complexity.

## Conclusion

Kotlin's powerful syntax sugars helps us write more concise and readable code. Choose the right function based on specific need.

For the most up-to-date information, always refer to the [official Kotlin documentation](https://kotlinlang.org/docs/collection-ordering.html).
