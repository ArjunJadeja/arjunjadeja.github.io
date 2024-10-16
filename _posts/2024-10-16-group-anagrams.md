---
title: Group Anagrams
date: 2024-10-16 11:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, string, array, hashmap]
---

## Problem Statement

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

**Solve Here:** [Two Sum](https://leetcode.com/problems/group-anagrams/description/)

## Examples

| Input | Output |
|-------|--------|
| `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]` | `[["bat"],["nat","tan"],["ate","eat","tea"]]` |
| `strs = [""]` | `[[""]]` |
| `strs = ["a"]` | `[["a"]]` |

## Edge Cases

1. **Empty list**: If `strs` is an empty array, return an empty list.
2. **Single string**: If `strs` contains only one string, return that string in its own group.

## Solution Approaches

### 1. Using HashMap (with Sorted Keys)

* **Description**: Sort each string's characters and use the sorted string as a key in a `HashMap`. Group anagrams by storing strings with the same sorted key together.
* **Time Complexity**: O(n * k log k) – Sorting each string takes `O(k log k)` and we process each string in the list once.
* **Space Complexity**: O(n * k) – Extra space for storing sorted versions of the strings in the `HashMap`.

```kotlin
fun groupAnagrams(strs: Array<String>): List<List<String>> {
    if (strs.isEmpty()) return emptyList()
    else if (strs.size == 1) return listOf(strs.toList())
    val sortedMap = HashMap<String, MutableList<String>>()
    for (string in strs) {
        val sortedString = string.toCharArray().sorted().joinToString("")
        if (sortedMap.containsKey(sortedString)) {
          sortedMap[sortedString]?.add(string)
        } else {
          sortedMap[sortedString] = mutableListOf(string)
        }
    }
    return sortedMap.values.toList()
}
```

## Complexity Comparison

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-------------------|
| HashMap with Sorted Keys | O(n * k log k) | O(n * k) |

## Conclusion

The **HashMap with sorted keys** approach is efficient and solves our problem.
