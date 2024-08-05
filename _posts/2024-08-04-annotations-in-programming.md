## Annotations in Programming with Kotlin

Like most things in life, we can't define Annotation in just one way. Here are a few ways I think of an annotation:

- छोटा पैकेट, बड़ा धमाका: This translates to something that looks small but is very powerful or impactful.
- An annotation is extra or other information associated with a particular point in a document [wikipedia](https://en.wikipedia.org/wiki/Annotation).
- Annotations are like a `tag` given to something. It can have some logic (literally!) or be used just for reference. For example, you might call your friend Sam a `genius`, which implies they are very knowledgeable about something. Here, there's some logic behind the label. But you could also call your friend Sam `Sammy` just for ease of use, which is purely a reference without additional logic.
- So, they are like a `data about a data` i.e. `Metadata`.

### Now, we have some knowledge about it. Lets learn about it's use in Kotlin:

To create an annotation in Kotlin, you define a class with the annotation keyword:

```
annotation class Genius
```

Now, you can use it anywhere. For example:

```
fun main() {
    val jim = Student(name = "Jim")
    @Genius val tim = Student(name = "Tim")
}
```

Here, our intention is to annotate the variable user2 with Genius. However, the problem is that we can apply this annotation to anything, like a class, function, or even an expression:

```
@Genius
class Result {
    @Genius fun getMarks(): Int {
        // Implementation here
    }
}
```

This might not be what we want, so Kotlin provides a way to specify where annotations are allowed to be used. You can declare the targets for the annotation like this:

```
@Target(AnnotationTarget.PROPERTY)
annotation class Genius
```

This ensures that the `Genius` annotation can only be applied to properties. If you try to use it elsewhere, the compiler will throw an error.

We can set annotation's target type (e.g., class, function, property) and retention policy (e.g., runtime, binary, source). Check all available types here: [AnnotationTarget](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.annotation/-annotation-target/) and [AnnotationRetention](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.annotation/-annotation-retention/)

### You might think what are this annotations(@Target, @Retention, @Repeatable, @MustBeDocumented) right?

These are called **Meta-Annotations**.

Meta-Annotations are `annotations about annotations`. Just like annotations themselves are `data about data`. Cool, right?

We can also create our own Meta-Annotations.

Here's how we create Meta-Annotation:

```
@Target(AnnotationTarget.ANNOTATION_CLASS)
@Retention(AnnotationRetention.RUNTIME)
annotation class MetaGenius(val description: String = "Meta-Annotation for Genius")
```

Use it with new annotation `@Genius`

```
@MetaGenius(description = "This annotation marks a class or function as genius.")
annotation class GeniusClass
```

###  Great now we know what are annotations and meta annotations lets utilize more power of it by finding all the geniuses of our class:

We are going to use [KSP / Kotlin Symbol Processing](https://kotlinlang.org/docs/ksp-overview.html) for that:

// todo

To learn more, check this out:

- [Kotlin Annotation](https://kotlinlang.org/docs/annotations.html#arrays-as-annotation-parameters)
