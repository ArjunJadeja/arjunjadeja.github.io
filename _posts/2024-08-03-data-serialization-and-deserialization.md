## Data Serialization and Deserialization with Kotlin

Suppose you have `User(name: String, age: Int)` object in your system. How would you transfer the
state of that object from one place to another (eg. server -> frontend)?

We need a process to transfer data from one place to another, right?

Well, we have a two-step process to successfully transfer the state of data from one place to
another:

1. **Serialization**
2. **Deserialization**

### What is serialization?

Serialization is the process of converting the state of an object, such as a `User`, into a form
that can be persisted or transferred.

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.serialization.png)

### What is deserialization?

Deserialization is the process of converting a stream of data back into an object, like
reconstructing a `User` object from the transferred data.

![Deserialization Diagram](/assets/data-serialization-and-deserialization/fig.deserialization.png)

### How does the data travel? Is it in bits(0101) or is it raw data(ab12) ?

It depends. Based on the type of serialization we are following.

1. Binary Serialization(0101) : ProtoBuf, CBOR
2. Others(anyType) : JSON, XML, YAML

Note: Both the sending and receiving end should use same type of serialization and deserialization
other wise state of data can't be translated back to same version.

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.types-of-serialization.svg)

