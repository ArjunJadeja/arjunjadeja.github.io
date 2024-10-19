---
title: Trapping Rain Water
date: 2024-10-19 10:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, two-pointers, array]
---

## Problem Statement

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

**Solve Here:** <a href="https://leetcode.com/problems/trapping-rain-water/" target="_blank">Trapping Rain Water</a>

### Examples:

| Input | Output |
|-------|--------|
| `height = [0,1,0,2,1,0,1,3,2,1,2,1]` | `6` |
| `height = [4,2,0,3,2,5]` | `9` |

### Explanation:
To visualize the problem, imagine that each integer in the array represents the height of a vertical bar at that position. After raining, water will be trapped between the bars, and we need to calculate the total volume of water trapped.

### Edge Cases:
1. **Flat or increasing heights**: If the height array is constantly increasing or flat, no water will be trapped.
2. **Single bar**: If the array has fewer than 3 elements, no water can be trapped.

## Solution Approaches:

### 1. Using Extra Space (O(n) Time, O(n) Space)

* **Description**: We calculate the maximum heights to the left and right of each bar. Then, for each bar, the amount of water trapped is the minimum of these two maximum heights minus the height of the current bar.
* **Time Complexity**: O(n) – three passes through the array (left, right, and result computation)
* **Space Complexity**: O(n) – for the two extra arrays (leftMax and rightMax)

```kotlin
class Solution {
    fun trap(height: IntArray): Int {
        if (height.isEmpty()) return 0
        
        val leftMax = IntArray(height.size)
        val rightMax = IntArray(height.size)
        
        var result = 0
        var currentMax = 0
        
        // Fill leftMax
        for (i in height.indices) {
            currentMax = maxOf(currentMax, height[i])
            leftMax[i] = currentMax
        }

        currentMax = 0
        
        // Fill rightMax
        for (i in height.size - 1 downTo 0) {
            currentMax = maxOf(currentMax, height[i])
            rightMax[i] = currentMax
        }

        // Calculate trapped water
        for (i in height.indices) {
            val minOfBoth = minOf(leftMax[i], rightMax[i])
            result += (minOfBoth - height[i].coerceAtLeast(0))
        }
        
        return result
    }
}
```

### 2. Using Two Pointers (O(n) Time, O(1) Space)

* **Description**: Instead of using extra arrays, we can keep track of the maximum heights on the left and right as we traverse the array with two pointers. One pointer starts from the left and the other from the right, and they move towards each other.
* **Time Complexity**: O(n) – one pass through the array
* **Space Complexity**: O(1) – no extra space apart from variables

```kotlin
class Solution {
    fun trap(height: IntArray): Int {
        if (height.isEmpty()) return 0
        
        var volumeOfWaterTrapped = 0
        var left = 0
        var right = height.lastIndex
        var currentLeftMax = 0
        var currentRightMax = 0

        while (left < right) {
            if (height[left] <= height[right]) {
                currentLeftMax = maxOf(currentLeftMax, height[left])
                volumeOfWaterTrapped += (currentLeftMax - height[left])
                left++
            } else {
                currentRightMax = maxOf(currentRightMax, height[right])
                volumeOfWaterTrapped += (currentRightMax - height[right])
                right--
            }
        }

        return volumeOfWaterTrapped
    }
}
```

## Two Pointers Approach Explanation:

* **Key Idea**: The trapped water at any given bar depends on the minimum of the tallest bars to its left and right. Using two pointers, we can maintain the maximum heights seen so far as we move from both ends of the array towards the center.
* **Why it works**: By always processing the smaller side (left or right), we ensure that the amount of water trapped is determined only by the shorter side, which is the limiting factor for water trapping.

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|----------------|------------------|
| Using Extra Space | O(n) | O(n) |
| Two Pointers | O(n) | O(1) |

## Conclusion:

The Two Pointers approach is more space-efficient with a constant space complexity of O(1), while still maintaining the same time complexity of O(n). This makes it the optimal solution for solving the trapping rain water problem, especially when working with large input arrays.
