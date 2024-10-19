---
title: Container with Most Water
date: 2024-10-19 9:00:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, two-pointers, array]
---

## Problem Statement

You are given an integer array `height` of length `n`, where each value represents the height of a vertical line drawn at that index. The task is to find two lines that, together with the x-axis, form a container that can store the maximum amount of water. The container's width is the distance between the two lines.

**Solve Here:** <a href="https://leetcode.com/problems/container-with-most-water/" target="_blank">Container with Most Water</a>

### Examples:

| Input | Output |
|-------|--------|
| `height = [1,8,6,2,5,4,8,3,7]` | `49` |
| `height = [1,1]` | `1` |

### Edge Cases:
1. **Minimum size array**: If the array has fewer than 2 elements, no container can be formed.
2. **Flat heights**: If all the heights are the same, the area is determined purely by the distance between the lines.

## Solution Approaches:

### 1. Brute Force (O(n²))

* **Description**: Use two nested loops to check every possible pair of lines and calculate the area between them. Track the maximum area found.
* **Time Complexity**: O(n²) – due to the nested loops
* **Space Complexity**: O(1) – constant space usage aside from the input array and result

```kotlin
fun maxAreaBruteForce(height: IntArray): Int {
    var maxArea = 0
    for (i in height.indices) {
        for (j in height.size - 1 downTo i) {
            val upperBound = minOf(height[i], height[j])
            val area = upperBound * (j - i)
            maxArea = maxOf(maxArea, area)
        }
    }
    return maxArea
}
```

### 2. Two Pointers (O(n))

* **Description**: Start with two pointers at the beginning and end of the array. Calculate the area between the two lines they represent. Move the pointer pointing to the shorter line inward, and repeat until the pointers meet.
* **Time Complexity**: O(n) – because we only traverse the array once
* **Space Complexity**: O(1) – constant space usage

```kotlin
fun maxArea(height: IntArray): Int {
    var maxArea = 0
    var left = 0
    var right = height.size - 1
    
    while (left < right) {
        val upperBound = minOf(height[left], height[right])
        val area = (right - left) * upperBound
        maxArea = maxOf(maxArea, area)
        
        if (height[left] < height[right]) left++ else right--
    }
    return maxArea
}
```

## Two Pointers Approach Explanation:

* **Key Idea**: The area between two lines is determined by the height of the shorter line and the distance between the lines. Thus, we maximize the area by shifting the pointer that points to the shorter line inward, hoping to find a taller line that may increase the area in subsequent calculations.
* **Why it works**: This method ensures that every possible container is considered without the need for nested loops, making it much more efficient.

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|----------------|------------------|
| Brute Force | O(n²) | O(1) |
| Two Pointers | O(n) | O(1) |

## Conclusion:

The **Two Pointers** approach is far more efficient, reducing the time complexity to O(n). By always moving the pointer associated with the shorter line, we make sure that we are exploring only the most promising pairs, ensuring that the maximum possible area is found in a single pass through the array.
