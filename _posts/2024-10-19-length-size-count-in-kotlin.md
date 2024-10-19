---
title: Length, Size and Count in Kotlin
date: 2024-10-19 19:00:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics]
---

A quick reference guide for length and size operations you'll frequently need in competitive programming and problem-solving.

## Quick Reference Table

| Data Structure | Property/Function | Returns | Example | Notes |
|----------------|------------------|----------|---------|-------|
| String | `length` | Int | `"kotlin".length` | Property, not function |
| Array | `size` | Int | `arrayOf(1,2,3).size` | Property |
| List/Set | `size` | Int | `listOf(1,2,3).size` | Property |
| Map | `size` | Int | `mapOf("a" to 1).size` | Count of key-value pairs |
| Collection | `isEmpty()` | Boolean | `list.isEmpty()` | Preferred over `size == 0` |
| Collection | `isNotEmpty()` | Boolean | `list.isNotEmpty()` | Preferred over `size > 0` |
| IntRange | `count()` | Int | `(1..10).count()` | Size of range |

## Common Problem-Solving Patterns

### String Operations
```kotlin
val str = "kotlin"
str.length                  // 6
str.lastIndex              // 5 (length - 1, useful in loops)
str.indices               // 0..5 (range of valid indices)

// Check if empty
str.isEmpty()             // false
str.isBlank()            // false (empty or only whitespace)
```

### Array Operations
```kotlin
val arr = arrayOf(1, 2, 3)
arr.size                  // 3
arr.indices              // 0..2
arr.lastIndex            // 2

// 2D Array
val matrix = Array(3) { IntArray(4) }
matrix.size              // 3 (rows)
matrix[0].size          // 4 (columns)
```

### Collection Operations
```kotlin
val list = listOf(1, 2, 3)
list.size                // 3
list.lastIndex          // 2

// For problem solving
list.first()            // 1 (first element)
list.last()             // 3 (last element)
list.getOrNull(5)       // null (safe access)

// Count elements matching condition
list.count { it > 1 }   // 2 (elements greater than 1)
```

### Map Operations
```kotlin
val map = mapOf("a" to 1, "b" to 2)
map.size                // 2
map.keys.size          // 2 (number of keys)
map.values.size        // 2 (number of values)
```

## Performance Tips

- Use `isEmpty()` instead of `size == 0` (more idiomatic and sometimes more efficient)
- `lastIndex` is better than `size - 1` for readability
- For large collections, `count()` with predicate traverses the entire collection, use with care

## Common Pitfalls to Avoid

```kotlin
// ❌ Don't do this
if (list.size == 0)   
if (str.length == 0)  

// ✅ Do this instead
if (list.isEmpty())   
if (str.isEmpty())    

// ❌ Don't do this in loops
for (i in 0..list.size)      // Includes size, causes IndexOutOfBounds
for (i in 0..list.size-1)    // Works but not idiomatic

// ✅ Do this instead
for (i in list.indices)      // Range of valid indices
for (i in 0 until list.size) // Excludes size
```

Remember: In Kotlin, prefer properties (`size`, `length`) over function calls when available, and use built-in ranges (`indices`, `lastIndex`) for cleaner code.
