---
title: Collection Operations By Type in Kotlin
date: 2024-10-19 20:30:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics]
---

## Operation Availability By Collection Type

✅ - Available  
❌ - Not Available  
🔄 - Returns different type

| Operation | List | Set | Map | Array | String | Sequence |
|-----------|------|-----|-----|--------|---------|-----------|
| `size` | ✅ | ✅ | ✅ | ✅ | ✅ (`length`) | ❌ |
| `isEmpty()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `contains()` | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ |
| `containsKey()` | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| `indexOf()` | ✅ | ❌ | ❌ | ✅ | ✅ | ❌ |
| `get(index)` | ✅ | ❌ | ❌ | ✅ | ✅ | ❌ |
| `get(key)` | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |

### Transformation Operations

| Operation | List | Set | Map | Array | Sequence |
|-----------|------|-----|-----|--------|-----------|
| `filter` | ✅ | 🔄List | 🔄List | 🔄List | ✅ |
| `map` | ✅ | 🔄List | 🔄List | 🔄List | ✅ |
| `flatten` | ✅ | 🔄List | ❌ | 🔄List | ✅ |
| `flatMap` | ✅ | 🔄List | 🔄List | 🔄List | ✅ |
| `sorted` | ✅ | 🔄List | ❌ | 🔄List | 🔄List |
| `distinct` | ✅ | 🔄List | ❌ | 🔄List | ✅ |
| `groupBy` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `associate` | ✅ | ✅ | ✅ | ✅ | ✅ |

### Aggregate Operations

| Operation | List | Set | Map | Array | Sequence |
|-----------|------|-----|-----|--------|-----------|
| `count` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `sum` | ✅ | ✅ | ❌ | ✅ | ✅ |
| `average` | ✅ | ✅ | ❌ | ✅ | ✅ |
| `max/min` | ✅ | ✅ | ❌ | ✅ | ✅ |
| `reduce` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `fold` | ✅ | ✅ | ✅ | ✅ | ✅ |

## Examples By Collection Type

### List Operations
```kotlin
val list = listOf(1, 2, 3, 4)
list.get(0)              // 1
list[0]                  // 1
list.indexOf(2)          // 1
list.subList(1, 3)       // [2, 3]
list.sorted()            // [1, 2, 3, 4]
```

### Set Operations
```kotlin
val set = setOf(1, 2, 3)
set.contains(1)          // true
// set[0]               // ❌ No index access
set.sorted()            // Returns List [1, 2, 3]
set.filter { it > 1 }   // Returns List [2, 3]
```

### Map Operations
```kotlin
val map = mapOf("a" to 1, "b" to 2)
map["a"]                // 1
map.get("a")            // 1
map.getOrDefault("c", 0) // 0
map.containsKey("a")    // true
map.keys               // Set of keys
map.values            // Collection of values
```

### Array Operations
```kotlin
val array = arrayOf(1, 2, 3)
array[0]               // 1
array.get(0)           // 1
array.indexOf(2)       // 1
array.sorted()         // Returns List [1, 2, 3]
```

### Sequence Operations
```kotlin
val seq = sequenceOf(1, 2, 3)
// seq[0]             // ❌ No index access
seq.filter { it > 1 } // Returns Sequence
seq.toList()          // Converts to List
```

## Converting Between Types

```kotlin
// To List
setOf(1, 2, 3).toList()
mapOf("a" to 1).toList()
arrayOf(1, 2, 3).toList()
sequenceOf(1, 2, 3).toList()

// To Set
listOf(1, 2, 3).toSet()
mapOf("a" to 1).toSet()
arrayOf(1, 2, 3).toSet()
sequenceOf(1, 2, 3).toSet()

// To Map
listOf("a" to 1).toMap()
setOf("a" to 1).toMap()
arrayOf("a" to 1).toMap()

// To Array
listOf(1, 2, 3).toTypedArray()
setOf(1, 2, 3).toTypedArray()
```

## Important Notes

1. **Return Types**:
  - Most operations on Set/Map return List
  - Sequence operations stay lazy until terminal operation

2. **Performance Implications**:
  - Set: O(1) for contains
  - List: O(n) for contains, O(1) for index access
  - Map: O(1) for key access
  - Sequence: Lazy evaluation, good for large collections

3. **Mutability**:
```kotlin
// Mutable Collections have additional operations
val mutableList = mutableListOf(1, 2, 3)
mutableList.add(4)
mutableList.removeAt(0)

val mutableSet = mutableSetOf(1, 2, 3)
mutableSet.add(4)
mutableSet.remove(1)

val mutableMap = mutableMapOf("a" to 1)
mutableMap["b"] = 2
mutableMap.remove("a")
```

Remember:
- Always choose the most appropriate collection type for your use case
- Consider using Sequences for large collections with multiple operations
- When performance is critical, understand the time complexity of operations
