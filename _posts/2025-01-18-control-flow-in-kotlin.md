---
title: Control Flow in Kotlin
date: 2025-01-18 11:00:00 +0530
categories: [Kotlin Notes]
tags: [control-flow, loops, conditional-statements]
---

## Control Flow

Executing a program sequentially line by line without any control is basic stuff. What if we want to skip the execution of a particular line or a block of code? OR What if we want to run a particular line of code ten times? OR What if our program faces runtime Exception? 

That's where control flow comes into picture!

Can you think of any other scenarios where you might need different type of control in your program?

## Different types of controls in Kotlin

1. Conditional Statements
2. Loops
3. Return and Jumps
4. Exceptions
5. Coroutines

### Conditional Statements

What do we mean by conditional statements? When we have to write code which should run only if a certain logical condition(for example. `if name == "arjun"`) is satisfied, we can use conditional statements.

In Kotlin, we have `if-else` and `when` type of conditional statements.

#### First, lets understand `if-else` conditional statements in detail:

If you want to execute a block or a line of code only for specific condition, then you can write it inside `if` block like example below.

```kotlin
if (name == "Arjun") {
  print(name)
}
```

The syntax for writing `if` block is:
1. Write `if` keyword.
2. Followed by a logical condition inside parenthesis `()`.
3. Followed by the code to be executed for given `if` condition inside curly braces `{}`.

As simple as that.

The curly braces `{}` can be ignored if there is only one line of code. This helps in writing concise code. we can simplify the above example like the example below.

```kotlin
if (name == "Arjun") print(name)
```

Looks better and more readable right? 

Ok. What if we want to execute a block or a line of code only if it satisfies multiple conditions? We can do that too by using `&&` or `||` logical operators. Let's understand it with example below.

```kotlin
if (name == "Arjun" && age > 18) print(name)
```

The above example will print name only if both conditions are satisfied because we have written AND `&&` condition in between. Let's look into one more example below.

```kotlin
if (name == "Arjun" || age > 18) print(name)
```

The above example will print name if any one condition is satisfied because we have written OR `||` condition in between.

We can also club multiple conditions like example below.

```kotlin
if ((name == "Arjun" && age > 18) || height > 6) print(name)
```

Can you guess, when the above example will print name?

We can do much more by grouping and clubbing multiple conditions according to our requirement. It is really a powerful tool!

Now let's say, we want a block or a line of code to execute if the condition written in `if` block is not true. In that case, we can write `else` block just after `if` block like the example below.

```kotlin
if (name == "Arjun") {
  print(name)
}
else {
  print("Not Found")
}
```

The syntax for writing `else` block is:
1. Write `else` keyword just after the `if` block.
2. Followed by the code to be executed inside curly braces `{}` when the logical condition for `if` block is not true or false.

Please note: `else` block does not exist on its own and has to be paired with `if` block.

we can write `else` block just after `if` block also like example below.

```kotlin
if (name == "Arjun") {
  print(name)
} else {
  print("Not Found")
}
```

We can simplify it even further like example below.

```kotlin
if (name == "Arjun") print(name)
else print("Wrong Name")
```

Let's simplify it even more like example below.

```kotlin
if (name == "Arjun") print(name) else print("Wrong Name")
```

Concise and more readable right? That's the beauty of Kotlin!

Please note: We can skip curly braces only for a single line of code. But for multiple lines of code, curly braces are mandatory.

Ok. What if we have multiple conditions and have to execute code according to each condition? Think about it. How will we handle this situation, with multiple `if` blocks?

Let's look into it with the example below.

```kotlin
if (month == "January" || month == "February" || month == "March") print("First Quarter")

if (month == "April" || month == "May" || month == "June") print("Second Quarter")

if (month == "July" || month == "August" || month == "September") print("Third Quarter")

if (month == "October" || month == "November" || month == "December") print("Fourth Quarter")
```

The example above works, but it can be simplified further using `else-if` chain instead of multiple `if` statements like the example below.

When would we need to write multiple `if` statements instead of using `else-if` chain? The answer is, when we have to make sure that each and every condition is evaluated.

```kotlin
if (month == "January" || month == "February" || month == "March") print("First Quarter")
else if (month == "April" || month == "May" || month == "June") print("Second Quarter")
else if (month == "July" || month == "August" || month == "September") print("Third Quarter")
else if (month == "October" || month == "November" || month == "December") print("Fourth Quarter")
```

Now, this is more readable! correct? It also has one more benefit, we can handle `else` case commonly. Let's understand in the example below.

```kotlin
if (month == "January" || month == "February" || month == "March") print("First Quarter")
else if (month == "April" || month == "May" || month == "June") print("Second Quarter")
else if (month == "July" || month == "August" || month == "September") print("Third Quarter")
else if (month == "October" || month == "November" || month == "December") print("Fourth Quarter")
else print("No Quarter matched")
```

In the example above, we did not have to handle `else` case for each `if` block. If any condition does not match, it will run code from common `else` block.

Please note: While running code, when one of the conditional block satisfies it logical condition, the code inside it is executed and no other conditional block is evaluated further in the same chain.

Ok. We can make the code above even more readable using `when` statements. Let's see how in the example below.

```kotlin
when (month) {
  "January" || "February" || "March" -> print ("First Quarter")
  "April" || "May" || "June" -> print ("Second Quarter")
  "July" || "August" || "September" -> print ("Third Quarter")
  "October" || "November" || "December" -> print ("Fourth Quarter")
  else -> print("No Quarter matched")
}
```

Same result but different way of declaration.

The syntax for writing `when` statements is:
1. 

- Using as expressions and statements
- Guard Conditions


### Loops

### Exceptions

### Coroutines

### Flow

## Can we manipulate flow during runtime?

## Can we stop the flow in between?

### Return and Jumps

## Do we consider a function as a part of control flow?

## How does it work?

## What is Control Flow Integrity?

## Redo/Retry in Control Flow?

## When should we use the above features?


Please Note:

[Control Flow](https://en.wikipedia.org/wiki/Control_flow) and [Flow Control](https://en.wikipedia.org/wiki/Flow_control_(data)) are different concepts. Do not confuse it with each other.
