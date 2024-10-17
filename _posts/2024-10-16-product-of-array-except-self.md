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

### 2. Using Division (Not Allowed by Problem Constraints)

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

### 3. Prefix and Postfix Products

* **Description:**
  - First, create a prefix product array where `prefix[i]` is the product of all elements before i.
  - Then, calculate a postfix product from the end of the array and multiply it with the prefix array.
  - This approach avoids using division and achieves O(n) time complexity.

* **Time Complexity:** O(n) – We pass through the array twice, once for the prefix and once for the postfix.
* **Space Complexity:** O(n) – The result array.

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
The first loop calculates the prefix product for each element, while the second loop calculates the postfix product. The final result at each index is the product of the prefix and postfix, which avoids division and achieves O(n) time complexity.

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-----------------|
| Brute Force | O(n²) | O(n)            |
| Division | O(n) | O(n)            |
| Prefix and Postfix Products | O(n) | O(n)            |

## Conclusion:

The brute force method is simple but inefficient with O(n²) time complexity. The division method provides a quick solution but violates the problem constraints. The prefix and postfix approach provides an optimal solution with O(n) time complexity.
