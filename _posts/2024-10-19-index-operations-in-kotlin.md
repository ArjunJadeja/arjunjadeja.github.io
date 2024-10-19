---
title: Index & Range Operations in Kotlin
date: 2024-10-19 17:30:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics]
---

Quick reference for index operations commonly needed in problem-solving.

## Quick Reference Table

| Property/Function | Applicable On | Returns | Example | Notes |
|------------------|---------------|----------|---------|-------|
| `lastIndex` | String, Array, List | Int | `"abc".lastIndex` | Returns -1 if empty |
| `indices` | String, Array, List | IntRange | `list.indices` | Range from 0 to lastIndex |
| `first()` | Collection | E | `list.first()` | Throws if empty |
| `last()` | Collection | E | `list.last()` | Throws if empty |
| `firstOrNull()` | Collection | E? | `list.firstOrNull()` | Returns null if empty |
| `lastOrNull()` | Collection | E? | `list.lastOrNull()` | Returns null if empty |
| `getOrNull()` | List, Array | E? | `list.getOrNull(1)` | Safe index access |
| `indexOf()` | List, Array, String | Int | `list.indexOf(x)` | Returns -1 if not found |
| `indexOfFirst{}` | Collection | Int | `list.indexOfFirst { it > 0 }` | Returns -1 if none match |
| `indexOfLast{}` | Collection | Int | `list.indexOfLast { it > 0 }` | Returns -1 if none match |
| `lastIndexOf()` | List, Array, String | Int | `list.lastIndexOf(x)` | Returns -1 if not found |

## Common Use Cases

### String Index Operations
```kotlin
val str = "kotlin"
str.lastIndex               // 5
str.indices                // 0..5
str.indexOf("t")          // 2
str.lastIndexOf("t")      // 2
str[str.lastIndex]        // 'n'
str.indexOfFirst { it.isUpperCase() }  // -1 (no uppercase)
```

### List/Array Index Operations
```kotlin
val list = listOf(1, 2, 2, 3)
list.first()              // 1
list.last()               // 3
list.indexOf(2)           // 1 (first occurrence)
list.lastIndexOf(2)       // 2 (last occurrence)
list.getOrNull(10)        // null (safe access)
list.getOrElse(10) { -1 } // -1 (default value if index invalid)

// Finding elements with conditions
list.indexOfFirst { it > 1 }  // 1
list.indexOfLast { it > 1 }   // 3
```

### Ranges and Loops
```kotlin
val list = listOf(1, 2, 3)

// Forward iteration
for (i in list.indices) { ... }         // 0..2
for (i in 0..list.lastIndex) { ... }    // 0..2
for (i in 0 until list.size) { ... }    // 0..2

// Backward iteration
for (i in list.lastIndex downTo 0) { ... }     // 2 downTo 0
for (i in list.indices.reversed()) { ... }      // 2 downTo 0

// Step iteration
for (i in list.indices step 2) { ... }         // 0, 2
```

### 2D Array Index Operations
```kotlin
val matrix = Array(3) { IntArray(4) }
val rows = matrix.indices            // 0..2
val cols = matrix[0].indices        // 0..3

// Safe 2D array access
fun Array<IntArray>.getOrNull(row: Int, col: Int): Int? =
    this.getOrNull(row)?.getOrNull(col)
```

## Common Patterns for Problem Solving

### Safe Element Access
```kotlin
// ✅ Safe first/last access
val first = list.firstOrNull() ?: 0
val last = list.lastOrNull() ?: 0

// ✅ Safe index access
val element = list.getOrNull(index) ?: defaultValue
val element2 = list.getOrElse(index) { defaultValue }
```

### Finding Elements
```kotlin
// Find first/last matching indices
val firstEven = list.indexOfFirst { it % 2 == 0 }
val lastEven = list.indexOfLast { it % 2 == 0 }

// Find all indices of an element
val allIndices = list.indices.filter { i -> list[i] == target }
```

### Window Operations
```kotlin
// Check bounds for sliding window
fun isValidWindow(start: Int, end: Int, size: Int) =
    start >= 0 && end <= size - 1

// Get valid neighbors in grid
fun getNeighbors(i: Int, j: Int, grid: Array<IntArray>): List<Pair<Int, Int>> {
    val dirs = listOf(-1 to 0, 1 to 0, 0 to -1, 0 to 1)
    return dirs.map { (di, dj) -> i + di to j + dj }
        .filter { (ni, nj) -> 
            ni in grid.indices && nj in grid[0].indices 
        }
}
```

## Performance Tips
- `getOrNull()` is more efficient than try-catch for invalid indices
- Use `indices` property instead of creating ranges manually
- `indexOfFirst/Last` stops at first match, more efficient than filtering
- For large lists, avoid multiple calls to `last()` or `lastIndex` in loops

Remember: Always prefer null-safe operations and range checks when dealing with indices to avoid IndexOutOfBoundsException.
