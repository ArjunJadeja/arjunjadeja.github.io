## Data Serialization and Deserialization with Kotlin

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.data-travel.svg)

Suppose you have a `User(name: String, age: Int)` object in your system. How would you transfer the
state of that object from one place to another (e.g., server -> frontend)?

We need a process to transfer the state of data from one place to another, right?

Well, we have a two-step process to successfully transfer the state of data from one place to
another:

1. **Serialization**
2. **Deserialization**

### What is serialization?

Serialization is the process of converting the state of an object, such as a `User`, into a form
that can be persisted or transferred.

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.serialization.svg)

### What is deserialization?

Deserialization is the process of converting a stream of data back into an object, like
reconstructing a `User` object from the transferred data.

![Deserialization Diagram](/assets/data-serialization-and-deserialization/fig.deserialization.svg)

### How does the serialized data travel? Is it in bits (0101) or is it raw data (ab12)?

It depends on the type of serialization we are following:

1. **Binary Serialization (0101)**: ProtoBuf, CBOR
2. **Text-Based Serialization (anyType)**: JSON, XML, YAML

![Types of Serialization Diagram](/assets/data-serialization-and-deserialization/fig.types-of-serialization.svg)

**Note:** Both the sending and receiving ends should use the same type of serialization and
deserialization; otherwise, the state of the data can't be translated back to the same version.

### Which type of serialization is better?

While binary serialization offers better performance, its lack of readability, potential complexity,
and limited support across diverse platforms make it less attractive in scenarios where human
interaction, interoperability, and flexibility are crucial. JSON and XML, despite being less
efficient, offer these benefits, which is why they are more widely adopted.

### How the state of data is serialized and deserialized in Kotlin internally?

It depends on which library you are using. Each library will have its own way of serializing and
deserializing.

Generally, Kotlin and Java serialization libraries use reflection or code generation to recursively
traverse and process data class properties and nested objects. Reflection provides flexibility but
may incur runtime overhead, while code generation offers better performance by generating efficient
serialization and deserialization code at compile-time.

![Serialization Process Diagram](/assets/data-serialization-and-deserialization/fig.serialization-process.svg)

### How to serialize and deserialize the state of data in Kotlin?

There are mainly two ways:

1. **Using Java Interfaces or Classes:** This includes using standard Java libraries or Java-based
   libraries that are interoperable with Kotlin.

2. **Using Kotlin Libraries:** This includes libraries like Kotlin Serialization that are
   specifically designed for Kotlin and take advantage of its features.

Lets serialize data with Kotlin Serialization library

Step 1: Add Dependencies for Kotlin Serialization library in `build.gradle` file

Step 2: Annotate class with `@Serializable`

```kotlin
import kotlinx.serialization.Serializable

@Serializable
data class User(val name: String, val age: Int)
```

Step 3: Serialize to JSON:

Use the `Json` object from Kotlin Serialization to convert the object to a JSON string.

```kotlin
import kotlinx.serialization.json.Json

val user1 = User("Jim", 21)
val json = Json.encodeToString(user1)
println(json)  // Output: {"name":"Alice","age":21}
```

Step 4: Deserialize from JSON:

Convert the JSON string back to an object.

```kotlin
val userFromJson = Json.decodeFromString<User>(json)
println(userFromJson)  // Output: User(name=Jim, age=21)
```

Can we ignore any field during serialization?

Yes, we can ignore fields during serialization with most libraries, whether we are using Java-based libraries or Kotlin-specific libraries. 

We have to mark the field to be ignored as transient, it will not be serialized by the standard Kotlin serialization library.

Annotate the field with @Transient in the class:

```kotlin
import kotlinx.serialization.Serializable
import kotlinx.serialization.Transient

@Serializable
data class User(
val name: String,
val age: Int,
@Transient val password: String? = null
)
```

Serialize and Deserialize:

```kotlin
import kotlinx.serialization.json.Json

val user2 = User("Tim", 20, "5678")
val json = Json.encodeToString(user2)
println(json)  // Output: {"name":"Tim","age":20}

val userFromJson = Json.decodeFromString<User>(json)
println(userFromJson)  // Output: User(name=Tim, age=20, password=null)
```

**Note:** A default value is required for non-serialized (@Transient) fields because the deserialization process needs to create a complete instance of the object. We can make it as nullable and provide default value as `null`.

### Why all the classes are not serializable by default in kotlin?

1. 

### References

Wikipedia - https://en.wikipedia.org/wiki/Serialization

[KotlinLang.org](http://KotlinLang.org) - https://kotlinlang.org/docs/serialization.html

Rock the
prototype - https://rock-the-prototype.com/en/learn-programming/serialization-how-does-serialization-of-data-work/
