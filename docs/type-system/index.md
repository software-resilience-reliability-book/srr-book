# The Type System

Computers must know how to store and manipulate data in order to be able to execute a program. To do this, programming languages provide a **type system** that defines the allowed values and operations for each type.

The foundation of a type system is **primitive types**. These are the basic types that are built into the language, such as integers, strings, and booleans. Primitive types often correspond to the basic data types of the underlying hardware - what the CPU can directly manipulate.

For example, a 32-bit signed integer is represented in memory as a sequence of 32 bits, with one bit reserved for the sign and the remaining 31 bits encoding the value using a scheme called two's complement. A single character may be represented as single byte.

From these primitive types, more complex types can be built. This allows us, as programmers, to create data types that are meaningful and easily understood by humans: a "Vehicle" class with properties for "Make", "Model", and "Year". This way the codebase is not a cryptic collection of symbols; it is instead a communication tool that relays the intent of the code.

Choosing types that accurately model a domain improves the reliability of a program by establishing expectations about data and behaviors.
