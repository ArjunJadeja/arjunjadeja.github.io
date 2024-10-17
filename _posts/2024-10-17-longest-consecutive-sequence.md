---
title: Longest Consecutive Sequence
date: 2024-10-17 10:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, array, hashset]
---

## Problem Statement

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

The algorithm should run in **O(n)** time complexity.

**Solve Here:** [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

## Examples

| Input | Output |
|-------|--------|
| `nums = [100, 4, 200, 1, 3, 2]` | `4` |
| `nums = [0,3,7,2,5,8,4,6,0,1]` | `9` |

## Edge Cases

1. **Empty array**: `nums = []` → `0`
2. **Single element array**: `nums = [1]` → `1`

## Solution Approaches

### 1. Brute Force (Sorting)

* **Description**: First, sort the array, then iterate through the sorted array to count consecutive elements.
* **Time Complexity**: O(n log n) – Due to sorting.
* **Space Complexity**: O(1) – Sorting is in-place.

```kotlin
fun longestConsecutive(nums: IntArray): Int {
    if(nums.isEmpty()) return 0
    else if(nums.size == 1) return 1
  
    nums.sort()
  
    var currentMax = 1
    var max = 1
  
    for(i in 0 until nums.size - 1) {
        if(nums[i] + 1 == nums[i + 1]) currentMax++
        else if(nums[i] == nums[i + 1]) continue
        else currentMax = 1
      
        if(currentMax >= max) max = currentMax
    }
  
    return max
}
```

### 2. Using HashSet

* **Description**: Insert all elements into a `HashSet`, then look for the beginning of a sequence by checking if `num - 1` exists. If it doesn't, it means the current `num` is the start of a new sequence. From there, count consecutive elements.
* **Time Complexity**: O(n) – Since each number is processed at most twice.
* **Space Complexity**: O(n) – Additional space for the `HashSet`.

```kotlin
fun longestConsecutive(nums: IntArray): Int {
    if(nums.isEmpty()) return 0
    else if(nums.size == 1) return 1
  
    val hashSet = HashSet<Int>()
    nums.forEach{ hashSet.add(it) }
  
    var longestStreak = 1
  
    for(num in nums) {
        if(!hashSet.contains(num - 1)) {
            var nextConsecutiveNumber = num + 1
            var currentStreak = 1
            
            while(hashSet.contains(nextConsecutiveNumber)){
              nextConsecutiveNumber++
              currentStreak++
            }
            
            longestStreak = max(longestStreak, currentStreak)
        }
    }
  
    return longestStreak
}
```

## Complexity Comparison

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-------------------|
| Sorting Approach | O(n log n) | O(1) |
| HashSet Approach | O(n) | O(n) |

## Conclusion

The **HashSet** approach is more efficient in terms of time complexity, as it allows for O(n) time by avoiding the need to sort the array. While it uses O(n) extra space, it meets the problem's requirement of O(n) time complexity. The **sorting** approach is straightforward but has a time complexity of O(n log n) due to the sorting step, making it less optimal for this specific problem.
