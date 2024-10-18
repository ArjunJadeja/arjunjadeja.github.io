---
title: Encode and Decode Strings
date: 2024-10-17 19:00:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, string, encoding, decoding]
---

## Problem Statement

Design an algorithm to encode a list of strings to a single string. The encoded string should be able to be decoded back into the original list of strings.

You need to:
1. Implement the `encode` function, which converts a list of strings into a single string.
2. Implement the `decode` function, which converts the single encoded string back into the original list of strings.

**Solve Here:** <a href="https://leetcode.com/problems/encode-and-decode-strings/" target="_blank">Encode and Decode Strings</a>

### Examples:

| Input | Encoded Output | Decoded Output |
|-------|---------------|----------------|
| `["hello", "world"]` | `"5#hello5#world"` | `["hello", "world"]` |
| `[""]` | `"0#"` | `[""]` |
| `["Hey", "there"]` | `"3#Hey5#there"` | `["Hey", "there"]` |

### Edge Cases:
1. **Empty string**: Handle empty strings with length 0
2. **Empty list**: Return appropriate encoding for an empty list
3. **Strings containing numbers and #**: The algorithm should handle these correctly
4. **Unicode characters**: Should work with any valid string characters

## Solution Approach

We need a way to separate the strings during encoding that won't conflict with the characters in the strings themselves. One effective solution is to use a delimiter (e.g., `#`) combined with the length of each string. This way, we can ensure that the decoding process can correctly identify the boundaries of each string.

### Steps:
* **Encode**:
  * For each string in the list, prepend its length followed by a special delimiter (e.g., `#`), then append the string itself.
  * For example, `"hello"` becomes `"5#hello"`.
* **Decode**:
  * Parse the encoded string by identifying the length of each string (before the `#`), then extract that many characters after the `#` to retrieve the original string.

## Implementation

```kotlin
class Codec {
    // Encodes a list of strings to a single string.
    fun encode(strs: List<String>): String {
        val encoded = StringBuilder()
        for (str in strs) {
            encoded.append(str.length).append("#").append(str)
        }
        return encoded.toString()
    }

    // Decodes a single string to a list of strings.
    fun decode(s: String): List<String> {
        val result = mutableListOf<String>()
        var i = 0
        
        while (i < s.length) {
            val delimiterIndex = s.indexOf("#", i)
            val length = s.substring(i, delimiterIndex).toInt()
            i = delimiterIndex + 1
            result.add(s.substring(i, i + length))
            i += length
        }
        
        return result
    }
}
```

## Detailed Explanation

### 1. Encoding Process
* The `encode` function iterates through each string in the input list
* For each string:
  * Appends the string's length
  * Adds the `#` delimiter
  * Appends the actual string
* Example: `["hello", "world"]` becomes `"5#hello5#world"`

### 2. Decoding Process
* The `decode` function maintains a pointer `i` to track position in the encoded string
* For each encoded string:
  * Finds the next `#` delimiter
  * Extracts the number before it to get string length
  * Uses the length to extract the original string
  * Updates pointer position
* Example: `"5#hello5#world"` becomes `["hello", "world"]`

## Complexity Analysis

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Encoding | O(n) | O(n) |
| Decoding | O(n) | O(n) |

Where n is the total number of characters across all strings.

## Conclusion

This encoding approach ensures that strings can be safely combined into a single string without losing information about their boundaries. By using the length of each string followed by a delimiter, we can reliably decode the original list of strings.
