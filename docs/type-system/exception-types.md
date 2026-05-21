# Using Exception Types Effectively

## Why have Multiple Exception Types?

In most languages **Exception** is treated as a base type that can have more specific derived types. This allows for flexibility when handling exceptions.

A typical try/catch block looks like this:

```csharp
try {
    // code that can throw an exception
} catch (Exception e) {
    // handle the exception
}
```

## Creating Custom Exception Types

It can be useful to create custom exception types, aside from the built-in ones, to provide more context about the error.

TODO

```csharp
public class MyException : Exception
{
    public MyException(string message) : base(message) { }
}
```

...

## Selectively Handling Exceptions

only handle types that the error contract defines;
don't handle base Exception type unless global error handling is desired;
...
