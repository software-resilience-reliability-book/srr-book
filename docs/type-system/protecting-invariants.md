# Protecting Invariants

## What are Invariants?

An **invariant** is a condition that must be true throughout the execution of a program. As containers for **state**, classes and other types can be designed to protect invariants through access control and error contracts.

## Guaranteeing Invariants

A natural place to place invariant checks is in the constructor of a class. Classes should take a fail fast approach when guaranteeing valid state. Let's look at two ways that we might implement a simple `Name` class:

### Version 1: No Constructor Checks

```csharp
public class Name
{
    public string First { get; }
    public string Last { get; }

    public string GetFullName()
    {
        if (string.IsNullOrEmpty(First) || string.IsNullOrEmpty(Last))
            throw new ArgumentException("First and last name are required");

        return $"{First} {Last}";
    }

    public string GetInitials()
    {
        if (string.IsNullOrEmpty(First) || string.IsNullOrEmpty(Last))
            throw new ArgumentException("First and last name are required");

        return $"{First[0]}{Last[0]}";
    }
}
```

This first version does not provide a constructor and instead relies on the caller to set the `First` and `Last` properties. There is nothing technically wrong with this approach, but it forces each method on the class to check that the `First` and `Last` properties are not null or empty.

It is possible to have a `Name` instance that violates the invariant that the `First` and `Last` properties are not null or empty:

```csharp
Name name = new Name();
name.Last = "Codesly";
name.GetFullName(); // Will throw an exception
```

In this case the call to `GetFullName` happened immediately after we created the `Name` object, but in a real application this `Name` object might have a longer lifecycle and the error might not be caught until much later in the program's execution. During this time the program is in an invalid state. The name with the empty values is a mess waiting to happen.

### Version 2: Guard Clause in Constructor

```csharp
public class Name
{
    public string First { get; }
    public string Last { get; }

    public Name(string first, string last)
    {
        // Guard clause ensures that we cannot create a Name object with empty values
        if (string.IsNullOrEmpty(first) || string.IsNullOrEmpty(last))
            throw new ArgumentException("First and last name are required");

        First = first;
        Last = last;
    }

    public string GetFullName()
    {
        return $"{First} {Last}";
    }

    public string GetInitials()
    {
        return $"{First[0]}{Last[0]}";
    }
}
```

In this second version we have added a constructor with a **guard clause** that ensures that we cannot create a `Name` object with empty values. The caller will still receive an exception if they provide empty values, but it will fail early so that the program will not continue in an invalid state.

```csharp
Name name = new Name("", "Codesly"); // Will throw an exception
name.GetFullName();
```

We've taken this same approach in the `RgbColor` class from in the reference project. It's not possible to have an instance of `RgbColor` with a value for `Red`, `Green`, or `Blue` that is outside the range of 0 to 255. The constructor prevents this from happening by enforcing these invariants.

If program data needs guarantees about its validity, consider protecting invariants by creating a custom type. Types do not need to be complex to add utility to a program. Even a simple data wrapper class can provide additional safety.
