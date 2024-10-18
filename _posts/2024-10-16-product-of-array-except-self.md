---
title: Product of Array Except Self
date: 2024-10-16 16:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, array]
---

## Problem Statement

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Solve Here:** [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)

**Constraints:**
- The product of any prefix or suffix of `nums` is guaranteed to fit in a 32-bit integer.
- You must write an algorithm that runs in O(n) time and without using the division operation.

### Examples:

| Input | Output |
|-------|--------|
| `nums = [1,2,3,4]` | `[24,12,8,6]` |
| `nums = [-1,1,0,-3,3]` | `[0,0,9,0,0]` |

### Edge Cases:
1. **Single element array**: If `nums` has only one element, the result should be an empty array.
2. **Array contains zeros**: When the array contains one or more zeros, the product for non-zero elements will be 0, except where `nums[i]` itself is zero.

## Solution Approaches:

### 1. Brute Force

* **Description:**
  - For each element, iterate through the entire array and compute the product of all elements except the current one.
  - This approach checks all combinations, making it a simple but inefficient solution.

* **Time Complexity:** O(n²) – For each element in the array, we iterate through the rest of the array.
* **Space Complexity:** O(n) – We store the result in a separate array.

```kotlin
fun productExceptSelf(nums: IntArray): IntArray {
    val res = IntArray(nums.size)
    for(i in nums.indices) {
        var prod = 1
        for(j in nums.indices) {
            if(i != j) prod *= nums[j]
        }
        res[i] = prod
    }
    return res
}
```

**Explanation:**
For each index i, the algorithm multiplies all elements in `nums` except `nums[i]`. This requires nested loops, resulting in O(n²) time complexity.

### 2. Using Division

* **Description:**
  - First, calculate the product of all elements in the array. Then, for each element at index i, divide the total product by `nums[i]`.
  - Although not allowed by the problem's constraints, this solution is included for understanding.

* **Time Complexity:** O(n) – Two passes through the array (one to compute the product, one to divide).
* **Space Complexity:** O(n) – The result array.

```kotlin
fun productExceptSelf(nums: IntArray): IntArray {
    val totalProduct = nums.fold(1) { prod, num -> prod * num }
    val res = IntArray(nums.size)

    for (i in nums.indices) {
        res[i] = totalProduct / nums[i]
    }

    return res
}
```

**Explanation:**
Calculate the total product of the array, then divide by each element to get the result. This approach has O(n) time complexity but uses division, which violates the problem constraints.

### 3. Two Arrays Products

* **Description:**
  - Create separate arrays for left and right products.
  - Combine them to get the final result.

* **Time Complexity:** O(n) – Three passes through the array.
* **Space Complexity:** O(n) – Three arrays used.

```kotlin
fun productExceptSelf(nums: IntArray): IntArray {
    val n = nums.size
    val leftProducts = IntArray(n) { 1 }
    val rightProducts = IntArray(n) { 1 }
    val result = IntArray(n)
    
    for (i in 1 until n) {
        leftProducts[i] = leftProducts[i-1] * nums[i-1]
    }
    
    for (i in n-2 downTo 0) {
        rightProducts[i] = rightProducts[i+1] * nums[i+1]
    }
    
    for (i in nums.indices) {
        result[i] = leftProducts[i] * rightProducts[i]
    }
    
    return result
}
```

**Explanation:**
Uses two arrays to store products from both directions, then combines them to get the final result without using division.

### 4. Space-Optimized Products

* **Description:**
  - Optimize the previous approach by using only the output array.
  - Calculate products in-place using two passes.

* **Time Complexity:** O(n) – Two passes through the array.
* **Space Complexity:** O(1) – Only the output array used.

```kotlin
fun productExceptSelf(nums: IntArray): IntArray {
    val res = IntArray(nums.size)

    var prefix = 1
    for (i in 0 until nums.size) {
        res[i] = prefix
        prefix *= nums[i]
    }

    var postfix = 1
    for (i in nums.size - 1 downTo 0) {
        res[i] *= postfix
        postfix *= nums[i]
    }

    return res
}
```

**Explanation:**
Uses the result array to store intermediate products and combines them in-place, achieving optimal space complexity.

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-----------------|
| Brute Force | O(n²) | O(n) |
| Division | O(n) | O(n) |
| Two Arrays Products | O(n) | O(n) |
| Space-Optimized Products | O(n) | O(1) |

## Conclusion:

The space-optimized products approach provides the optimal solution with O(n) time complexity and O(1) space complexity while meeting all problem constraints.
