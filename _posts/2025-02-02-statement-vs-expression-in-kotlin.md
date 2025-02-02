---
title: Statement vs Expression in Kotlin
date: 2025-02-02 23:00:00 +0530
categories: [Kotlin Bytes]
tags: [kb, statement, expression]
image:
  path: /assets/posts/kotlin-bytes/statement-vs-expression-in-kotlin/thumbnail.svg
  alt: "Statement v/s Expression"
---

## Definition

**Expression**: A piece of code that evaluates to a value. It always produces/returns a result that can be assigned to a variable or used in other expressions.

**Statement**: A piece of code that performs an action but does not return a value. It executes instructions without producing a result.

## Key Differences

| Aspect | Expression | Statement |
|--------|------------|-----------|
| **Returns a value** | Yes, always | No |
| **Can be assigned to variable** | Yes | No |
| **Can be used in other expressions** | Yes | No |
| **Purpose** | Produce a value | Perform an action |
| **Examples** | `2 + 3`, `if-else`, `when` | `for` loop, `while` loop |

## Simple Rule

**If you can assign it to a variable, it's an expression. If you can't, it's a statement.**

```kotlin
// Expression - can be assigned
val result = 2 + 3  // ✓ Works

// Statement - cannot be assigned
val result = for (i in 1..5) { println(i) }  // ✗ Error
```

## Expressions in Kotlin

### Basic Expressions

```kotlin
// Arithmetic expressions
val sum = 5 + 3           // 8
val product = 4 * 2       // 8
val division = 10 / 2     // 5

// Boolean expressions
val isAdult = age >= 18   // true or false
val isValid = x > 0 && x < 100

// Function calls (if they return a value)
val length = "Hello".length  // 5
val upper = "hello".uppercase()  // "HELLO"
```

### if as Expression

In Kotlin, `if` is an expression that returns a value:

```kotlin
// if-else as expression
val max = if (a > b) a else b

val result = if (score >= 60) {
    "Pass"
} else {
    "Fail"
}

// Can be used directly in function return
fun getGrade(marks: Int) = if (marks >= 90) "A" 
                           else if (marks >= 80) "B"
                           else if (marks >= 70) "C"
                           else "F"
```

### when as Expression

`when` in Kotlin is an expression that returns a value:

```kotlin
val dayType = when (day) {
    "Saturday", "Sunday" -> "Weekend"
    else -> "Weekday"
}

val result = when {
    x < 0 -> "Negative"
    x == 0 -> "Zero"
    else -> "Positive"
}

// Using when directly in assignment
val message = when (age) {
    in 0..12 -> "Child"
    in 13..19 -> "Teenager"
    in 20..59 -> "Adult"
    else -> "Senior"
}
```

### try-catch as Expression

```kotlin
val number = try {
    input.toInt()
} catch (e: NumberFormatException) {
    0  // Default value if parsing fails
}

val result = try {
    risky()
} catch (e: Exception) {
    "Error occurred"
}
```

### Block Expression

The last expression in a block becomes its value:

```kotlin
val result = {
    val x = 10
    val y = 20
    x + y  // This is returned (30)
}()

val greeting = run {
    val name = "Alice"
    val age = 25
    "Hello, $name! You are $age years old."  // This is returned
}
```

### Lambda Expressions

```kotlin
val double = { x: Int -> x * 2 }
val result = double(5)  // 10

val sum = { a: Int, b: Int -> a + b }
val total = sum(3, 7)  // 10
```

## Statements in Kotlin

Statements perform actions but don't return values.

### for Loop (Statement)

```kotlin
// for loop is a statement - cannot assign it
for (i in 1..5) {
    println(i)
}

// This is an ERROR
val result = for (i in 1..5) { i }  // ✗ Compilation error
```

### while Loop (Statement)

```kotlin
// while loop is a statement
var count = 0
while (count < 5) {
    println(count)
    count++
}

// This is an ERROR
val result = while (count < 10) { count++ }  // ✗ Compilation error
```

### do-while Loop (Statement)

```kotlin
// do-while is a statement
var i = 0
do {
    println(i)
    i++
} while (i < 5)
```

### Variable Declarations (Statement)

```kotlin
// Variable declarations are statements
val name = "Alice"    // Statement
var age = 25          // Statement

// But the right side is an expression
val result = 10 + 20  // '10 + 20' is expression, whole line is statement
```

### Assignment (Statement)

```kotlin
var x = 10
x = 20  // Assignment is a statement (in Kotlin)

// This is an ERROR in Kotlin
val y = (x = 30)  // ✗ Error: assignment is not an expression
```

**Note**: In some languages like C or Java, assignment is an expression, but in Kotlin it's a statement.

## Practical Examples

### Example 1: Using if as Expression

```kotlin
// Good - Using if as expression
fun getDiscount(age: Int): Double {
    return if (age < 18 || age > 60) 0.20 else 0.10
}

// Can be simplified to
fun getDiscount(age: Int) = if (age < 18 || age > 60) 0.20 else 0.10
```

### Example 2: Using when as Expression

```kotlin
// Good - Using when as expression
fun getPaymentMethod(type: String) = when (type) {
    "cash" -> "Pay by Cash"
    "card" -> "Pay by Card"
    "upi" -> "Pay by UPI"
    else -> "Invalid payment method"
}

val method = getPaymentMethod("upi")  // "Pay by UPI"
```

### Example 3: Converting Statement to Expression

```kotlin
// Using statement (verbose)
fun checkNumber(num: Int): String {
    var result: String
    if (num > 0) {
        result = "Positive"
    } else if (num < 0) {
        result = "Negative"
    } else {
        result = "Zero"
    }
    return result
}

// Using expression (concise)
fun checkNumber(num: Int): String {
    return when {
        num > 0 -> "Positive"
        num < 0 -> "Negative"
        else -> "Zero"
    }
}

// Even more concise
fun checkNumber(num: Int) = when {
    num > 0 -> "Positive"
    num < 0 -> "Negative"
    else -> "Zero"
}
```

### Example 4: try-catch as Expression

```kotlin
// Using statement
fun parseNumber(input: String): Int {
    var result: Int
    try {
        result = input.toInt()
    } catch (e: NumberFormatException) {
        result = -1
    }
    return result
}

// Using expression
fun parseNumber(input: String): Int {
    return try {
        input.toInt()
    } catch (e: NumberFormatException) {
        -1
    }
}

// Even more concise
fun parseNumber(input: String) = try {
    input.toInt()
} catch (e: NumberFormatException) {
    -1
}
```

## Expression-Oriented Programming

Kotlin encourages expression-oriented programming, which leads to more concise and functional code.

### Benefits of Expressions

1. **More concise code**

```kotlin
// Statement style
var max: Int
if (a > b) {
    max = a
} else {
    max = b
}

// Expression style
val max = if (a > b) a else b
```

2. **Immutability (using val)**

```kotlin
// With expressions, you can use val instead of var
val status = if (isLoggedIn) "Online" else "Offline"

// With statements, you need var
var status: String
if (isLoggedIn) {
    status = "Online"
} else {
    status = "Offline"
}
```

3. **Better readability**

```kotlin
// Expression style - clear and readable
val grade = when (marks) {
    in 90..100 -> "A"
    in 80..89 -> "B"
    in 70..79 -> "C"
    in 60..69 -> "D"
    else -> "F"
}
```

## Common Mistakes

### Mistake 1: Forgetting else in if Expression

```kotlin
// ERROR - if used as expression must have else
val result = if (x > 0) "Positive"  // ✗ Missing else branch

// CORRECT
val result = if (x > 0) "Positive" else "Non-positive"  // ✓
```

### Mistake 2: Trying to assign loops

```kotlin
// ERROR - for loop is a statement
val numbers = for (i in 1..5) { i }  // ✗ Won't work

// CORRECT - Use map or list comprehension
val numbers = (1..5).map { it }  // ✓
val numbers = (1..5).toList()    // ✓
```

### Mistake 3: Not using the returned value

```kotlin
// Inefficient - when returns value but not used
var result = ""
when (day) {
    "Monday" -> result = "Start of week"
    "Friday" -> result = "End of week"
    else -> result = "Mid week"
}

// Better - Use when as expression
val result = when (day) {
    "Monday" -> "Start of week"
    "Friday" -> "End of week"
    else -> "Mid week"
}
```

## Summary

1. **Expressions** return a value and can be assigned to variables; **Statements** perform actions without returning values.
2. In Kotlin, `if`, `when`, and `try-catch` are expressions, unlike many other languages.
3. `for`, `while`, and `do-while` loops are statements in Kotlin.
4. Expressions enable more concise, functional, and immutable code.
5. Prefer expressions over statements when possible for cleaner code.
6. If used as an expression must have an `else` branch.
7. The last expression in a block becomes its return value.

### References

- [Kotlin Official Documentation - Control Flow](https://kotlinlang.org/docs/control-flow.html)
- [Kotlin Official Documentation - Returns and Jumps](https://kotlinlang.org/docs/returns.html)
