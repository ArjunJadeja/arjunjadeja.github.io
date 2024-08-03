## Data Serialization and Deserialization with Kotlin

How would you transfer the state of a `User` object (e.g., `User(name: String, age: Int)`) from one place to another (server -> frontend)?

We need a process to transfer data from one place to another, right?

Well, we have a two-step process to successfully transfer the state of data from one place to another:
1. **Serialization**
2. **Deserialization**

### What is serialization?

![Serialization Diagram](/assets/data-serialization-and-deserialization/fig.serialization.png)

Serialization is the process of converting the state of an object, such as a `User`, into a form that can be persisted or transferred.

### What is deserialization?

![Deserialization Diagram](/assets/data-serialization-and-deserialization/fig.deserialization.png)

Deserialization is the process of converting a stream of data back into an object, like reconstructing a `User` object from the transferred data.

How the data travels? Is it in bits or is it raw data ?