---
title: Top K Frequent Elements
date: 2024-10-16 15:00:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, array, hashmap, sorting]
---

## Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order.

**Solve Here:** <a href="https://leetcode.com/problems/top-k-frequent-elements/description/" target="_blank">Top K Frequent Elements</a>

### Examples:

| Input | Output |
|-------|--------|
| `nums = [1,1,1,2,2,3], k = 2` | `[1, 2]` |
| `nums = [1], k = 1` | `[1]` |
| `nums = [3,0,1,0], k = 1` | `[0]` or `[3]` |

### Edge Cases:
1. **Single element**: If `nums` has only one element, return that element.
2. **All elements have equal frequency**: If every element in the array occurs the same number of times, any `k` elements can be returned.

## Solution Approaches:

### 1. Using HashMap and Sorting

* **Description:** First, create a frequency map using a HashMap where the key is the element and the value is its frequency. Sort the entries of the map by the frequency in descending order. Finally, select the first `k` elements from the sorted list and return them.
* **Time Complexity:** O(n log n) – Sorting the frequency map.
* **Space Complexity:** O(n) – Storing the frequency map.

```kotlin
fun topKFrequent(nums: IntArray, k: Int): IntArray {
    val frequencyMap = HashMap<Int, Int>()
    for (num in nums) {
        frequencyMap[num] = frequencyMap.getOrDefault(num, 0) + 1
    }
    val sortedNumbers = frequencyMap.entries.sortedByDescending { it.value }
    return sortedNumbers.take(k).map { it.key }.toIntArray()
}
```

### 2. Using Bucket Sort

* **Description:** Create a frequency map like before, but instead of sorting the map, use a list of lists (`freq`) where the index represents the frequency and each element at that index represents the numbers with that frequency. Finally, iterate through the `freq` list in reverse order to collect the `k` most frequent elements.

* **Time Complexity:** O(n) – No sorting involved.
* **Space Complexity:** O(n) – Storing the frequency map and the `freq` list.

```kotlin
fun topKFrequent(nums: IntArray, k: Int): IntArray {
    val res = mutableListOf<Int>()
    val count = hashMapOf<Int, Int>()
    val freq = MutableList<MutableList<Int>>(nums.size + 1) { mutableListOf() }
    
    for (n in nums) {
        count[n] = count.getOrDefault(n, 0) + 1
    }
    
    for ((n, c) in count) {
        freq[c].add(n)
    }
    
    for (i in freq.size - 1 downTo 0) {
        for (n in freq[i]) {
            res.add(n)
            if (res.size == k) {
                return res.toIntArray()
            }
        }
    }
    
    return intArrayOf()
}
```

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-------------------|
| HashMap + Sorting | O(n log n) | O(n) |
| Bucket Sort | O(n) | O(n) |

## Conclusion:

For most cases, the Bucket Sort approach is highly efficient with O(n) time complexity. However, if `k` is much smaller than `n`. The HashMap + Sorting method is simple and intuitive, but its O(n log n) complexity makes it less efficient for large inputs.
