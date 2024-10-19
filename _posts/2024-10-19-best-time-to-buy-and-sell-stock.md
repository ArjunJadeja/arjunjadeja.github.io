---
title: Best Time to Buy and Sell Stock
date: 2024-10-19 15:00:00 +0530
categories: [Problem Solving, Questions]
tags: [dsa, array]
---

## Problem Statement

You are given an array `prices` where `prices[i]` represents the price of a given stock on the `i`th day. You want to maximize your profit by buying the stock on one day and selling it on another later day.

Return the maximum profit you can achieve from this transaction. If no profit is possible (i.e., prices are only decreasing), return `0`.

### Examples:

| Input | Output | Explanation |
|-------|--------|-------------|
| `prices = [7,1,5,3,6,4]` | `5` | Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 5 |
| `prices = [7,6,4,3,1]` | `0` | No transaction yields profit |

### Edge Cases:
1. **Single day**: If there's only one price, no transaction is possible, so the profit is `0`.
2. **Decreasing prices**: If the prices only decrease, no profit is possible, and the function should return `0`.

## Solution Approach:

### 1. Optimized Single Pass (O(n))

* **Description**: We traverse the price array once, keeping track of the minimum price so far and calculating the maximum possible profit at each step.
* **Time Complexity**: O(n) – we only iterate through the array once
* **Space Complexity**: O(1) – constant space usage

```kotlin
fun maxProfit(prices: IntArray): Int {
    if (prices.isEmpty()) return 0
    
    var minPrice = prices[0]
    var maxProfit = 0
    
    for (price in prices) {
        minPrice = minOf(minPrice, price)       
        val profit = price - minPrice
        maxProfit = maxOf(maxProfit, profit)
    }
    
    return maxProfit
}
```

## Approach Explanation:

* **Key Idea**: To maximize profit, you need to buy at the lowest price and sell at the highest price after the buying day. By keeping track of the minimum price seen so far and calculating the profit at each step, we ensure that we always capture the maximum possible profit.
* **Profit Calculation**: At each price, the profit is calculated by subtracting the minimum price so far from the current price. If this profit is greater than the previous maximum profit, we update the maximum profit.

## Complexity Analysis:

| Approach | Time Complexity | Space Complexity |
|----------|----------------|------------------|
| Optimized Single Pass | O(n) | O(1) |

## Conclusion:

The **Single Pass** approach is highly efficient, with a time complexity of O(n) and constant space usage. It ensures that we find the maximum profit by iterating through the price array just once, making it the optimal solution for this problem.
