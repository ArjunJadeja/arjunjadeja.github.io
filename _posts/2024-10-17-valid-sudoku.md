---
title: Valid Sudoku
date: 2024-10-17 18:30:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, array, hashset]
---

## Problem Statement

Determine if a 9 x 9 Sudoku board is valid. The board is considered valid if:
* Each row contains the digits 1-9 without repetition.
* Each column contains the digits 1-9 without repetition.
* Each of the nine 3 x 3 sub-boxes contains the digits 1-9 without repetition.

**Note:**
* Only filled cells need to be validated.
* The board could be valid even if it is not solvable.

**Solve Here:** [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

## Examples

| Input | Output |
|-------|--------|
| `[ `<br>`["5","3",".",".","7",".",".",".","."],`<br>`["6",".",".","1","9","5",".",".","."],`<br>`[".","9","8",".",".",".",".","6","."],`<br>`["8",".",".",".","6",".",".",".","3"],`<br>`["4",".",".","8",".","3",".",".","1"],`<br>`["7",".",".",".","2",".",".",".","6"],`<br>`[".","6",".",".",".",".","2","8","."],`<br>`[".",".",".","4","1","9",".",".","5"],`<br>`[".",".",".",".","8",".",".","7","9"]`<br>`]` | `true` |

## Edge Cases

1. **Empty board**: If all cells are empty, it should return `true`.
2. **Partial board**: Some cells can be filled while others are not; as long as no rules are violated, the board is valid.

## Solution Approach

The algorithm uses three sets of hash sets to track numbers already seen in each row, column, and 3x3 sub-box. For each cell, if the number already exists in any of these sets, the board is invalid.

### Steps:
* Initialize hash sets to track numbers in each row, column, and sub-box.
* Iterate through each cell:
  * Skip if the cell is not a digit.
  * Check for duplicates in the corresponding row, column, and 3x3 sub-box.
  * Add the number to the appropriate sets if no duplicates are found.

### Code Implementation:

```kotlin
fun isValidSudoku(board: Array<CharArray>): Boolean {
    val columns = Array(9) { HashSet<Int>() }
    val rows = Array(9) { HashSet<Int>() }
    val subGrids = arrayOf(
        arrayOf(HashSet<Int>(), HashSet<Int>(), HashSet<Int>()),
        arrayOf(HashSet<Int>(), HashSet<Int>(), HashSet<Int>()),
        arrayOf(HashSet<Int>(), HashSet<Int>(), HashSet<Int>())
    )

    for (row in 0 until 9) {
        for (col in 0 until 9) {
            if (!board[row][col].isDigit()) continue

            val value = Character.getNumericValue(board[row][col])

            // Check the row
            if (value in rows[row]) return false
            rows[row].add(value)

            // Check the column
            if (value in columns[col]) return false
            columns[col].add(value)

            // Check the 3x3 sub-grid
            val subGridRow = row / 3
            val subGridCol = col / 3
            if (value in subGrids[subGridRow][subGridCol]) return false
            subGrids[subGridRow][subGridCol].add(value)
        }
    }
    return true
}
```

## Complexity Analysis

* **Time Complexity**: O(1) – Since the board is fixed at 9x9, this operation is constant time.
* **Space Complexity**: O(1) – The space used is also constant since the board size is fixed, though we are using several hash sets to track the state.

## Conclusion

This approach ensures that the board is validated by checking each row, column, and 3x3 sub-box in a single pass. The algorithm runs efficiently with constant time complexity due to the fixed size of the Sudoku board.
