---
title: Array Contains Duplicate
date: 2024-10-15 11:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, array, hashset]
---

## Problem: Array Contains Duplicate

**Problem Statement:** Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

**Solve Here:** [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

### Examples:

| Input | Output |
|-------|--------|
| `nums = [1,2,3,1]` | `true` |
| `nums = [1,2,3,4]` | `false` |
| `nums = [1,1,1,3,3,4,3,2,4,2]` | `true` |

### Edge Cases:
1. **Empty array**: `nums = []` → `false`
2. **Single element array**: `nums = [1]` → `false`

## Solution Approaches:

### 1. Brute Force Approach
* **Description**: Compare each element with every other element.
* **Time Complexity**: O(n²) – Double loop through the array.
* **Space Complexity**: O(1) – No extra data structure used.

```kotlin
fun containsDuplicate(nums: IntArray): Boolean {
    for (i in nums.indices) {
        for (j in i + 1 until nums.size) {
            if (nums[i] == nums[j]) {
                return true
            }
        }
    }
    return false
}
```

### 2. Using Sorting
* **Description**: Sort the array and check for consecutive duplicate elements.
* **Time Complexity**: O(n log n) – Time taken to sort the array.
* **Space Complexity**: O(1) – If in-place sorting is used (depends on the sorting algorithm used by Kotlin).

```kotlin
fun containsDuplicate(nums: IntArray): Boolean {
    nums.sort()
    for (i in 0 until nums.size - 1) {
        if (nums[i] == nums[i + 1]) {
            return true
        }
    }
    return false
}
```

### 3. Using HashSet
* **Description**: Use a `HashSet` to track seen elements and detect duplicates.
* **Time Complexity**: O(n) – Single pass through the array.
* **Space Complexity**: O(n) – Additional space required for the `HashSet`.

```kotlin
fun containsDuplicate(nums: IntArray): Boolean {
    val seen = HashSet<Int>()
    for (num in nums) {
        if (!seen.add(num)) {
            return true
        }
    }
    return false
}
```

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-------------------|
| Brute Force | O(n²) | O(1) |
| Sorting | O(n log n) | O(1) |
| Using HashSet | O(n) | O(n) |

## Conclusion:

Among the three approaches, the **HashSet** approach is the most efficient in terms of time complexity, while the **sorting** approach might be useful if we need to sort the array for other reasons.
