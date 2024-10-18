---
title: Valid Palindrome
date: 2024-10-18 11:00:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, two-pointers, string]
---

## Problem Statement

A string is considered a palindrome if, after converting all uppercase letters to lowercase and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include both letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

**Solve Here:** <a href="https://leetcode.com/problems/valid-palindrome/" target="_blank">Valid Palindrome</a>

### Examples:

| Input | Output |
|-------|--------|
| `"A man, a plan, a canal: Panama"` | `true` |
| `"race a car"` | `false` |
| `" "` | `true` |

### Edge Cases:
1. **Empty string**: If the string is empty, it should return `true`.
2. **Single character**: Any single character is considered a palindrome.
3. **String with non-alphanumeric characters**: Ignore spaces, punctuation, and special characters.

## Solution Approaches:

### 1. Using reversed() function

* **Description:** This approach is simple and uses Kotlin's `reversed()` function after filtering out non-alphanumeric characters and converting the string to lowercase.
* **Time Complexity:** O(n) – String filtering and reversing
* **Space Complexity:** O(n) – Additional space for the filtered string

```kotlin
fun isPalindrome(s: String): Boolean {
    val cleanedString = s.filter { it.isLetterOrDigit() }.lowercase()
    return cleanedString == cleanedString.reversed()
}
```

### 2. Using Two Pointers

* **Description:** This approach utilizes two pointers—one starting from the beginning and one from the end. The idea is to move both pointers inward while skipping any non-alphanumeric characters. If the characters at the two pointers don't match, it's not a palindrome.
* **Time Complexity:** O(n) – Each character is visited at most once
* **Space Complexity:** O(1) – No additional space is used except for the input string

```kotlin
fun isPalindrome(s: String): Boolean {
    val formattedString = s.lowercase()
    var left = 0
    var right = formattedString.length - 1
    
    while (left < right) {
        // Move left pointer to the next alphanumeric character
        while (left < right && !formattedString[left].isLetterOrDigit()) {
            left++
        }
        
        // Move right pointer to the previous alphanumeric character
        while (right > left && !formattedString[right].isLetterOrDigit()) {
            right--
        }
        
        // Check if characters at both pointers match
        if (formattedString[left] != formattedString[right]) {
            return false
        }
        
        left++
        right--
    }
    
    return true
}
```

## Complexity Comparison:

| Approach | Time Complexity | Space Complexity |
|----------|----------------|------------------|
| Using `reversed()` | O(n) | O(n) |
| Two Pointers | O(n) | O(1) |

## Conclusion:

The **Two Pointers** approach is more efficient in terms of space complexity, as it doesn't require creating a new string for filtering or reversing. Both approaches, however, work efficiently with O(n) time complexity.
