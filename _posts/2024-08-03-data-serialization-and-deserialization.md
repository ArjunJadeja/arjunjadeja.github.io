## Data Serialization and Deserialization with Kotlin

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.data-travel.svg)

Suppose you have a `User(name: String, age: Int)` object in your system. How would you transfer the state of that object from one place to another (e.g., server -> frontend)?

We need a process to transfer the state of data from one place to another, right?

Well, we have a two-step process to successfully transfer the state of data from one place to another:

1. **Serialization**
2. **Deserialization**

### What is serialization?

Serialization is the process of converting the state of an object, such as a `User`, into a form that can be persisted or transferred.

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.serialization.svg)

### What is deserialization?

Deserialization is the process of converting a stream of data back into an object, like reconstructing a `User` object from the transferred data.

![Deserialization Diagram](/assets/data-serialization-and-deserialization/fig.deserialization.svg)

### How does the serialized data travel? Is it in bits (0101) or is it raw data (ab12)?

It depends on the type of serialization we are following:

1. **Binary Serialization (0101)**: ProtoBuf, CBOR
2. **Text-Based Serialization (anyType)**: JSON, XML, YAML

![Types of Serialization Diagram](/assets/data-serialization-and-deserialization/fig.types-of-serialization.svg)

**Note:** Both the sending and receiving ends should use the same type of serialization and deserialization; otherwise, the state of the data can't be translated back to the same version.

### Which serialization type is better?

**Binary Serialization (ProtoBuf, CBOR)**

Binary serialization involves converting data into a binary format. This format is compact and not human-readable but is efficient in terms of size and speed. It is well-suited for scenarios where performance and low overhead are crucial.

**Advantages:**

- **Efficiency:** Generally more space-efficient and faster to serialize/deserialize because it doesn't require parsing or generating human-readable text.
- **Performance:** Lower computational overhead due to reduced size and the absence of parsing.

**Disadvantages:**

- **Readability:** Not human-readable, which makes debugging and manual inspection more challenging.
- **Portability:** May be less portable across different systems or languages, especially if the format is not standardized.

**Text-Based Serialization (JSON, XML, etc.)**

**Advantages:**

- **Readability:** Human-readable and writable, making it easier to debug and manually inspect.
- **Interoperability:** Widely supported across different programming languages and platforms.
- **Simplicity:** The format is simple and easy to understand.

**Disadvantages:**

- **Size:** Generally larger than binary formats due to additional overhead for text representation.
- **Speed:** Serialization and deserialization can be slower compared to binary formats due to the parsing of text.

While binary serialization offers better performance, its lack of readability, potential complexity, and limited support across diverse platforms make it less attractive in scenarios where human interaction, interoperability, and flexibility are crucial. JSON and XML, despite being less efficient, offer these benefits, which is why they are more widely adopted.

### How is the state of data serialized and deserialized in Kotlin?

It depends on which library you are using. Each library will have its own way of serializing and deserializing.

Generally, Kotlin and Java serialization libraries use reflection or code generation to recursively traverse and process data class properties and nested objects. Reflection provides flexibility but may incur runtime overhead, while code generation offers better performance by generating efficient serialization and deserialization code at compile-time.

[//]: # (![Serialization Process Diagram]&#40;/assets/data-serialization-and-deserialization/fig.serialization-process.svg&#41;)

### How to serialize and deserialize the state of data in Kotlin?

There are mainly two ways:

1. **Using Java Interfaces or Classes:** This includes using standard Java libraries or Java-based libraries that are interoperable with Kotlin. Examples include using `Serializable`, `Externalizable`, or third-party libraries like Gson, Jackson, or Moshi.

2. **Using Kotlin Libraries:** This includes libraries like Kotlin Serialization that are specifically designed for Kotlin and take advantage of its features.
