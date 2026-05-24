# Type Implementations

## Dynamically Typed Languages

Whether implicitly or explicitly, all values in a program have a data type.

**Dynamically typed** languages do not require that the data type be declared, and type checking occurs at runtime. These languages typically infer the type of a variable based on the value assigned to it. For example, the following JavaScript code assigns a string to the `firstName` variable and a numeric value to the `age` variable, then prints the type of each variable:

```javascript
const firstName = "Arie";
const age = 21;
console.log(typeof firstName);
console.log(typeof age);
```

## Statically Typed Languages

**Statically typed** languages require that variables be declared with a specific type before they can be used.

```csharp
string firstName = "Arie";
int age = 21;
```

Because the data type is known at compile time, the compiler can provide **type safety**, and prevent code from being compiled if there is a type mismatch. If a function expects a string, and you pass it an integer, the compiler will not allow it to compile.

## Custom Types

The type system not only descibes **primitive types** like integers and strings, but provides the means to create **custom types**. Classes are the primary way to create these custom types in C#. Other options include records, structs, and enumerations.

## Additional Resources

We will cover the what is needed to follow the concepts in this book. If you would like to learn more about data types that C# supports see the following documentation:

- [Classes](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes)
- [Structs](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/structs)
- [Record types](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/records)
- [Interfaces](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces)
- [Enumerations](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/enums)
- [Generics](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics)

If you are new to object oriented programming you may also follow these tutorials:

- [Explore object oriented programming with classes and objects](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/classes)
- [Object-Oriented programming (C#)](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/oop)
- [Inheritance in C# and .NET](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/inheritance)
