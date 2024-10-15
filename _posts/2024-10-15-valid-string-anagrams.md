---
title: Valid String Anagrams
date: 2024-10-15 12:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, string, array]
---

## Problem: Valid String Anagrams

**Problem Statement:** Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

**Solve Here:** [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

### Examples:

| Input | Output |
|-------|--------|
| `s = "anagram"`, `t = "nagaram"` | `true` |
| `s = "rat"`, `t = "car"` | `false` |

### Edge Cases:
1. **Different lengths**: If `s` and `t` have different lengths, return `false`.
2. **Empty strings**: Two empty strings are considered anagrams, so return `true` in this case.

## Solution Approaches:

### 1. By Sorting Strings
* **Description**: Sort both strings and compare them character by character. If the sorted strings are identical, they are anagrams.
* **Time Complexity**: O(n log n) – Time taken to sort the strings.
* **Space Complexity**: O(n) – Extra space used by the sorting function.

```kotlin
fun isAnagram(s: String, t: String): Boolean {
    if (s.length != t.length) return false
    return s.toCharArray().sorted() == t.toCharArray().sorted()
}
```

### 2. Using Frequency count
* **Description**: If the problem restricts `s` and `t` to lowercase English letters, we can use an `IntArray` of size 26 to store the frequency of each letter.
* **Time Complexity**: O(n) – Single pass to update and compare frequencies.
* **Space Complexity**: O(1) – Fixed space for the `IntArray`.

```kotlin
fun isAnagram(s: String, t: String): Boolean {
    if (s.length != t.length) return false
    
    val count = IntArray(26)
    
    for (i in s.indices) {
        count[s[i] - 'a']++
        count[t[i] - 'a']--
    }
    
    return count.all { it == 0 }
}
```

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|-------------------|
| Sorting Strings | O(n log n) | O(n) |
| IntArray (for a-z characters) | O(n) | O(1) |

## Conclusion:

The **sorting** method is easy to implement and understand, but it's slightly less efficient due to the sorting step. The **IntArray** approach is the most efficient in terms of both time and space complexity. It uses a simple counting technique to compare the frequency of characters in both strings.
