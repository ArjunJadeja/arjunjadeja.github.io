---
title: Annotations in Programming with Kotlin ft. KSP
date: 2024-08-04 13:00:00 +0530
categories: [Kotlin Notes]
tags: [kotlin, annotations, meta-annotations, kapt, ksp]
---

## Annotations in Programming with Kotlin ft. KSP

Like most things in life, we can't define Annotation in just one way. Here are a few ways I think of an annotation:

- छोटा पैकेट, बड़ा धमाका: This translates to something that looks small but is very powerful or impactful.
- An annotation is extra or other information associated with a particular point in a document [wikipedia](https://en.wikipedia.org/wiki/Annotation).
- Annotations are like a `tag` given to something. It can have some logic (literally!) or be used just for reference. For example, you might call your friend Sam a `genius`, which implies they are very knowledgeable about something. Here, there's some logic behind the label. But you could also call your friend Sam `Sammy` just for ease of use, which is purely a reference without additional logic.
- So, they are like a `data about a data` i.e. `Metadata`.

### Now, we have some knowledge about it. Lets learn about it's use in Kotlin:

To create an annotation in Kotlin, you define a class with the `annotation` keyword:

```kotlin
annotation class Genius
```

Now, you can use it anywhere. For example:

```kotlin
fun main() {
    val jim = Student(name = "Jim")
    @Genius val tim = Student(name = "Tim")
}
```

Here, our intention is to annotate the variable user2 with Genius. However, the problem is that we can apply this annotation to anything, like a class, function, or even an expression:

```kotlin
@Genius
class Result {
    @Genius fun getMarks(): Int {
        // Implementation here
    }
}
```

This might not be what we want, so Kotlin provides a way to specify where annotations are allowed to be used. You can declare the targets for the annotation like this:

```kotlin
@Target(AnnotationTarget.PROPERTY)
annotation class Genius
```

This ensures that the `Genius` annotation can only be applied to properties. If you try to use it elsewhere, the compiler will throw an error.

We can set annotation's target type (e.g., class, function, property) and retention policy (e.g., runtime, binary, source). Check all available types here: [AnnotationTarget](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.annotation/-annotation-target/) and [AnnotationRetention](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.annotation/-annotation-retention/)

You might think what are this annotations(@Target, @Retention, @Repeatable, @MustBeDocumented) right?

These are called **Meta-Annotations**.

### What are Meta-Annotations?

Meta-Annotations are `annotations about annotations`. Just like annotations themselves are `data about data`. Cool, right?

We can also create our own Meta-Annotations.

Here's how we create Meta-Annotation:

```kotlin
@Target(AnnotationTarget.ANNOTATION_CLASS)
@Retention(AnnotationRetention.RUNTIME)
annotation class MetaGenius(val description: String = "Meta-Annotation for Genius")
```

Use it with new annotation `@Genius`

```kotlin
@MetaGenius(description = "This annotation marks a class or function as genius.")
annotation class GeniusClass
```

Ok, But what's the use of doing all of these?

### Processing annotations using KSP

Now that we know what annotations and meta-annotations are, let's utilize their power by finding all the geniuses in our class:

Set up [KSP / Kotlin Symbol Processing](https://kotlinlang.org/docs/ksp-overview.html) for this:

Here's a summary of setting up KSP:  

1. **Add Dependencies**
2. **Create Annotations**
3. **Implement SymbolProcessor and SymbolProcessorProvider interfaces**
4. **Register your processor provider**
5. **Make the IDE aware of generated code**

Here's how your processor and processor provider might look:

```kotlin
import com.google.devtools.ksp.processing.*
import com.google.devtools.ksp.symbol.*
import kotlin.reflect.KClass

class GeniusProcessor(
    private val codeGenerator: CodeGenerator,
    private val logger: KSPLogger
) : SymbolProcessor {

    override fun process(resolver: Resolver): List<KSAnnotated> {
        // Find all symbols annotated with @Genius
        val symbols = resolver.getSymbolsWithAnnotation(Genius::class.qualifiedName!!)
            .filterIsInstance<KSPropertyDeclaration>()

        // Iterate through all annotated properties
        symbols.forEach { symbol ->
            val studentName = symbol.simpleName.asString()
            val className = symbol.parentDeclaration?.qualifiedName?.asString()

            logger.warn("Found Genius student: $studentName in class $className")
        }

        return emptyList()
    }
}

class GeniusProcessorProvider : SymbolProcessorProvider {
    override fun create(
        environment: SymbolProcessorEnvironment
    ): SymbolProcessor {
        return GeniusProcessor(environment.codeGenerator, environment.logger)
    }
}
```

Use it in main fun:

```kotlin
class TestingKSP {
    fun main() {
        val jim = Student(name = "Jim")
        @Genius val tim = Student(name = "Tim")
    }
}
```

After compiling, if everything is set up correctly, the processor will log:

```
Found Genius student: tim in class TestingKSP
```

This is just a basic example. We can do much more using annotations in our code.

Now can we say that annotations are frontend of the complicated process running behind the scene and making life easy for user(here, it is developer)? 

don't hesitate to use them wisely 😉

checkout [KotlinPoet](https://square.github.io/kotlinpoet/) for code generation and use it with ksp to generate code.

Follow official documentation for latest guidelines:

- [Kotlin Annotation](https://kotlinlang.org/docs/annotations.html)
- [KSP](https://kotlinlang.org/docs/ksp-overview.html)
