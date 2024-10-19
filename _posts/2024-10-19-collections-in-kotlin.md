---
title: Collection Types and Declarations in Kotlin
date: 2024-10-19 12:00:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics]
---

## Collection Type Hierarchy

```
Collection (Interface)
├── List (Interface)
│   ├── ArrayList
│   ├── LinkedList
│   └── Arrays.asList()
├── Set (Interface)
│   ├── HashSet
│   ├── LinkedHashSet
│   └── TreeSet (SortedSet)
└── Queue (Interface)
    ├── ArrayDeque
    └── PriorityQueue

Map (Interface)
├── HashMap
├── LinkedHashMap
└── TreeMap (SortedMap)
```

## List Declarations

### Immutable Lists
```kotlin
// Type inference
val list1 = listOf(1, 2, 3)
val list2 = emptyList<Int>()

// Explicit type
val list3: List<Int> = listOf(1, 2, 3)
val list4: List<Int> = ArrayList()  // Backed by ArrayList but immutable reference

// Arrays
val array1 = arrayOf(1, 2, 3)              // Array<Int>
val array2 = intArrayOf(1, 2, 3)           // IntArray (primitive)
val array3 = Array(5) { it * 2 }           // [0, 2, 4, 6, 8]
val array4 = IntArray(5) { it * 2 }        // Primitive int array
```

### Mutable Lists
```kotlin
// Type inference
val list1 = mutableListOf(1, 2, 3)
val list2 = arrayListOf(1, 2, 3)

// Explicit type
val list3: MutableList<Int> = mutableListOf()
val list4: ArrayList<Int> = ArrayList()
val list5: LinkedList<Int> = LinkedList()

// Empty mutable lists
val list6 = mutableListOf<Int>()
val list7: MutableList<Int> = ArrayList()
```

## Set Declarations

### Immutable Sets
```kotlin
// Type inference
val set1 = setOf(1, 2, 3)
val set2 = emptySet<Int>()

// Explicit type
val set3: Set<Int> = setOf(1, 2, 3)
val set4: Set<Int> = HashSet()  // Backed by HashSet but immutable reference
```

### Mutable Sets
```kotlin
// HashSet (unordered, best performance)
val set1 = mutableSetOf<Int>()           // Returns LinkedHashSet
val set2: HashSet<Int> = HashSet()       // Explicit HashSet
val set3 = hashSetOf(1, 2, 3)            // Kotlin shorthand

// LinkedHashSet (maintains insertion order)
val set4: LinkedHashSet<Int> = LinkedHashSet()
val set5 = linkedSetOf(1, 2, 3)          // Kotlin shorthand

// TreeSet (sorted)
val set6: TreeSet<Int> = TreeSet()       // Natural ordering
val set7 = sortedSetOf(3, 1, 2)          // Returns TreeSet
val set8 = TreeSet<Int>(compareBy { -it }) // Custom comparator
```

## Map Declarations

### Immutable Maps
```kotlin
// Type inference
val map1 = mapOf("a" to 1, "b" to 2)
val map2 = emptyMap<String, Int>()

// Explicit type
val map3: Map<String, Int> = mapOf("a" to 1)
val map4: Map<String, Int> = HashMap()  // Backed by HashMap but immutable reference
```

### Mutable Maps
```kotlin
// HashMap (unordered, best performance)
val map1 = mutableMapOf<String, Int>()     // Returns LinkedHashMap
val map2: HashMap<String, Int> = HashMap()
val map3 = hashMapOf("a" to 1, "b" to 2)   // Kotlin shorthand

// LinkedHashMap (maintains insertion order)
val map4: LinkedHashMap<String, Int> = LinkedHashMap()
val map5 = linkedMapOf("a" to 1, "b" to 2)

// TreeMap (sorted by keys)
val map6: TreeMap<String, Int> = TreeMap()  // Natural ordering
val map7 = sortedMapOf("b" to 2, "a" to 1) // Returns TreeMap
val map8 = TreeMap<String, Int>(compareBy { it.length }) // Custom comparator
```

## Special Collections

### Queue and Deque
```kotlin
// ArrayDeque (double-ended queue)
val deque1: ArrayDeque<Int> = ArrayDeque()
val deque2 = ArrayDeque(listOf(1, 2, 3))

// PriorityQueue
val pq1: PriorityQueue<Int> = PriorityQueue()
val pq2 = PriorityQueue<Int>(compareBy { -it })  // Max heap
```

### Fixed-Size Collections
```kotlin
// Fixed-size list
val fixed1 = List(5) { it * 2 }             // Immutable [0,2,4,6,8]
val fixed2 = MutableList(5) { 0 }           // Mutable [0,0,0,0,0]

// 2D Arrays/Lists
val matrix1 = Array(3) { IntArray(4) }      // 3x4 primitive int array
val matrix2 = Array(3) { Array(4) { 0 } }   // 3x4 Array<Array<Int>>
val matrix3 = List(3) { MutableList(4) { 0 } } // 3x4 mutable list
```

## Collection Builders
```kotlin
// Build collections with custom logic
val list = buildList {
    add(1)
    addAll(listOf(2, 3))
    add(4)
}

val set = buildSet {
    add(1)
    addAll(setOf(2, 3))
}

val map = buildMap {
    put("a", 1)
    putAll(mapOf("b" to 2))
}
```

## Type Conversion
```kotlin
// List conversions
list.toMutableList()
list.toList()           // New immutable copy
list.toTypedArray()
list.toIntArray()       // For List<Int>

// Set conversions
set.toMutableSet()
set.toSet()            // New immutable copy
set.toList()

// Map conversions
map.toMutableMap()
map.toMap()            // New immutable copy
map.toList()           // List of Pairs
```

## Performance Characteristics

| Collection Type | Add/Remove | Get/Contains | Memory Usage | Ordered? |
|----------------|------------|--------------|--------------|----------|
| ArrayList | O(1)/O(n) | O(1)/O(n) | Low | Yes |
| LinkedList | O(1)/O(1) | O(n)/O(n) | Medium | Yes |
| HashSet | O(1)/O(1) | O(1) | Medium | No |
| LinkedHashSet | O(1)/O(1) | O(1) | Medium | Yes |
| TreeSet | O(log n)/O(log n) | O(log n) | Medium | Sorted |
| HashMap | O(1)/O(1) | O(1) | Medium | No |
| LinkedHashMap | O(1)/O(1) | O(1) | Medium | Yes |
| TreeMap | O(log n)/O(log n) | O(log n) | Medium | Sorted |
| ArrayDeque | O(1)/O(1) | O(1) | Low | Yes |
| PriorityQueue | O(log n)/O(log n) | O(1) for peek | Medium | Partial |

## Tips and Best Practices

1. Choose the right collection type:
  - Need ordered elements? → List or LinkedHashSet/Map
  - Need unique elements? → Set
  - Need key-value pairs? → Map
  - Need sorting? → TreeSet/TreeMap
  - Need fast lookups? → HashSet/HashMap

2. Use immutable collections by default:
   ```kotlin
   // Prefer
   val list = listOf(1, 2, 3)
   
   // Over
   val list = mutableListOf(1, 2, 3)
   ```

3. Use type inference but be explicit when needed:
   ```kotlin
   // Good for simple cases
   val list = listOf(1, 2, 3)
   
   // Better for complex types
   val map: Map<String, List<Int>> = mapOf(
       "a" to listOf(1, 2),
       "b" to listOf(3, 4)
   )
   ```

Remember:
- LinkedHash* variants maintain insertion order but use more memory
- Tree* variants keep elements sorted but have slower operations
- Choose mutable collections only when you need to modify the collection
- Consider using sequences for large collections with multiple operations
