---
title: Exploring Loops in Kotlin
date: 2024-10-15 12:00:00 +0530
categories: [Problem Solving, Helpers]
tags: [kotlin-basics, loops]
---

When diving into problem-solving in Kotlin, **loops** are an essential concept that we encounter frequently. Kotlin offers various ways to loop through data structures, ranging from traditional loops to more concise syntax sugar like `forEach`. In this post, we'll explore loops, so that we can solve problems efficiently.

## Types of Loops in Kotlin

Kotlin provides several types of loops, each suited to different scenarios:

- `for` Loop
- `while` Loop
- `do-while` Loop
- `forEach` and other iterators

Let's go over these with examples.

### for Loop

In Kotlin, the `for` loop is used to iterate over a range, array, or collection. It's a versatile and commonly used loop. Here's the basic syntax:

```kotlin
for (i in 1..5) {
    println(i)
}
```

This will print numbers from 1 to 5. We can also control the step size or iterate in reverse:

```kotlin
for (i in 5 downTo 1 step 2) {
    println(i)
}
```

This prints 5, 3, 1. Pretty neat, right?

#### Iterating Over Collections

The `for` loop also works well with collections like arrays, lists, and maps:

```kotlin
val fruits = arrayOf("apple", "banana", "cherry")
for (fruit in fruits) {
    println(fruit)
}
```

### while Loop

The `while` loop runs as long as the condition is true. It's useful when we don't know how many iterations we need beforehand:

```kotlin
var i = 1
while (i <= 5) {
    println(i)
    i++
}
```

This prints numbers from 1 to 5, similar to the `for` loop, but `while` gives more control when the condition is dynamic.

### do-while Loop

The `do-while` loop is almost the same as `while`, except it executes the block of code first and then checks the condition. It guarantees at least one execution:

```kotlin
var i = 1
do {
    println(i)
    i++
} while (i <= 5)
```

This also prints 1, 2, 3, 4, 5.

## Kotlin Syntax Sugars for Loops

Kotlin provides cleaner, more functional ways to loop through collections. These often make our code more concise and expressive.

### forEach

Instead of a traditional `for` loop, we can use `forEach` on any collection:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers.forEach { println(it) }
```

Here, `forEach` takes a lambda and applies it to every element in the collection. It's a concise alternative and improves readability.

### forEachIndexed

If we need both the index and the value, use `forEachIndexed`:

```kotlin
val fruits = listOf("apple", "banana", "cherry")
fruits.forEachIndexed { index, fruit ->
    println("Item at $index is $fruit")
}
```

This is equivalent to using a `for` loop with indices, but it's much shorter and often easier to read.

## Controlling Loops with break and continue

When working with loops, there are times when you need to interrupt the normal flow of the loop. Kotlin provides `break` and `continue` to help with this.

### break

The `break` statement is used to terminate the loop entirely when a certain condition is met:

```kotlin
for (i in 1..5) {
    if (i == 3) break
    println(i)
}
```

This will print 1, 2, and then exit the loop when `i` equals 3.

### continue

The `continue` statement skips the current iteration and moves to the next one:

```kotlin
for (i in 1..5) {
    if (i == 3) continue
    println(i)
}
```

This will print 1, 2, 4, 5, skipping 3 but continuing the rest of the loop.

## Looping Through Different Data Structures

Let's see how loops work with different data structures like arrays, lists, and strings.

### Arrays

Iterating over arrays is straightforward in Kotlin. We can either use a `for` loop or a method like `forEach`:

```kotlin
val arr = arrayOf(1, 2, 3, 4, 5)
arr.forEach { println(it) }
```

If we need access to the index, we can use `indices`:

```kotlin
for (i in arr.indices) {
    println("Index $i has value ${arr[i]}")
}
```

### Lists

Lists behave similarly to arrays, but they're more versatile. We can loop over lists using `forEach` or a `for` loop:

```kotlin
val list = listOf("a", "b", "c")
list.forEach { println(it) }
```

### Strings

Strings can be treated as an array of characters, so we can loop through each character like this:

```kotlin
val str = "Kotlin"
for (char in str) {
    println(char)
}
```

Or use `forEach` for brevity:

```kotlin
str.forEach { println(it) }
```

## Conclusion

Now, we have basic understanding of the various types of loops in Kotlin. Loops form the foundation for most algorithms, so understanding them will help us in problem-solving.

## Official Documentation

[Kotlin Conditions and loops](https://kotlinlang.org/docs/control-flow.html)
