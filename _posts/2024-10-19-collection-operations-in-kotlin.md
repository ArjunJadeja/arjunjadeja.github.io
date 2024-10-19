---
title: Collection Operations in Kotlin
date: 2024-10-19 20:00:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics]
---

## Quick Reference Tables

### Basic Operations

| Operation | Description | Example | Returns |
|-----------|-------------|---------|----------|
| `filter` | Keep elements matching predicate | `list.filter { it > 0 }` | List |
| `filterNot` | Remove elements matching predicate | `list.filterNot { it > 0 }` | List |
| `map` | Transform each element | `list.map { it * 2 }` | List |
| `forEach` | Iterate elements | `list.forEach { print(it) }` | Unit |
| `any` | Check if any match | `list.any { it > 0 }` | Boolean |
| `all` | Check if all match | `list.all { it > 0 }` | Boolean |
| `none` | Check if none match | `list.none { it > 0 }` | Boolean |
| `count` | Count elements | `list.count { it > 0 }` | Int |
| `find` | First matching or null | `list.find { it > 0 }` | E? |
| `contains` | Check if element exists | `list.contains(5)` | Boolean |

### Transformation Operations

| Operation | Description | Example | Returns |
|-----------|-------------|---------|----------|
| `distinct` | Unique elements | `list.distinct()` | List |
| `sorted` | Sort ascending | `list.sorted()` | List |
| `sortedBy` | Sort by selector | `list.sortedBy { it.age }` | List |
| `sortedDescending` | Sort descending | `list.sortedDescending()` | List |
| `reversed` | Reverse order | `list.reversed()` | List |
| `flatten` | Flatten nested lists | `listOf(list1, list2).flatten()` | List |
| `flatMap` | Map and flatten | `list.flatMap { listOf(it, -it) }` | List |
| `groupBy` | Group by key | `list.groupBy { it.type }` | Map |
| `associate` | Create map | `list.associate { it to it * 2 }` | Map |
| `zip` | Pair elements | `list1.zip(list2)` | List<Pair> |

### Aggregate Operations

| Operation | Description | Example | Returns |
|-----------|-------------|---------|----------|
| `sum` | Sum of elements | `list.sum()` | Number |
| `average` | Average of elements | `list.average()` | Double |
| `max/min` | Max/min element | `list.max()` | E? |
| `maxBy/minBy` | Max/min by selector | `list.maxBy { it.value }` | E? |
| `reduce` | Reduce to single value | `list.reduce { acc, e -> acc + e }` | E |
| `fold` | Reduce with initial | `list.fold(0) { acc, e -> acc + e }` | R |
| `joinToString` | Join to string | `list.joinToString(",")` | String |
| `chunked` | Split into chunks | `list.chunked(3)` | List<List> |
| `windowed` | Sliding window | `list.windowed(3)` | List<List> |

## Common Problem-Solving Patterns

### Frequency Count
```kotlin
// Count occurrences
val freq = list.groupingBy { it }.eachCount()

// Top K frequent
val topK = freq.entries
    .sortedByDescending { it.value }
    .take(k)
    .map { it.key }
```

### Window Operations
```kotlin
// Fixed size window
list.windowed(3) { window -> window.sum() }

// Sliding window with step
list.windowed(3, step = 2, partial = true)

// Running sum
list.runningFold(0) { acc, e -> acc + e }
```

### Two Pointers
```kotlin
// Find pair sum
fun findPairSum(list: List<Int>, target: Int): Pair<Int, Int>? {
    val sorted = list.sorted()
    var left = 0
    var right = sorted.lastIndex
    
    while (left < right) {
        val sum = sorted[left] + sorted[right]
        when {
            sum == target -> return sorted[left] to sorted[right]
            sum < target -> left++
            else -> right--
        }
    }
    return null
}
```

### Set Operations
```kotlin
val set1 = setOf(1, 2, 3)
val set2 = setOf(3, 4, 5)

set1 intersect set2  // [3]
set1 union set2      // [1, 2, 3, 4, 5]
set1 subtract set2   // [1, 2]
```

### Matrix Operations
```kotlin
// Transpose matrix
val transposed = matrix.indices.map { i ->
    matrix[0].indices.map { j -> matrix[j][i] }
}

// Flatten 2D array
val flattened = matrix.flatten()

// Matrix multiplication using fold
val result = matrix1.map { row ->
    matrix2[0].indices.map { col ->
        row.indices.fold(0) { acc, i ->
            acc + row[i] * matrix2[i][col]
        }
    }
}
```

## Performance Tips

1. Use sequences for large collections with multiple operations:
```kotlin
list.asSequence()
    .filter { it > 0 }
    .map { it * 2 }
    .take(3)
    .toList()
```

2. Prefer:
  - `getOrNull()` over try-catch
  - `firstOrNull()` over `find()`
  - `any()` over `count() > 0`
  - `none()` over `count() == 0`

3. Chain Operations Efficiently:
```kotlin
// ❌ Inefficient
list.filter { it > 0 }.map { it * 2 }.filter { it < 10 }

// ✅ Better
list.filter { it > 0 && it * 2 < 10 }.map { it * 2 }
```

Remember: Consider space-time tradeoffs when choosing between different collection operations. Some operations create new collections while others work in-place.
