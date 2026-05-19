# Error Contracts

## What is an Error Contract?

An **error contract** is the mechanism by which an application communicates its expected error behavior to the caller. This applies mostly in the context of functions and methods.

The function's **caller** is responsible for handling the error, so it must know the format in which the error will be communicated.

## Return Values as Error Contracts

All functions return a value, and this value may form part of the error contract. A typical example is a function that finds the index of an item in a list.

In almost all implementations, the function will not "break" if it does not find the item: it will simply return a "magic value" (-1) to indicate that the item was not found.

```csharp
List<string> animals = new()
{
    "cat",
    "dog",
    "mouse"
};

// Will return -1 if the item is not found in the list
int index = animals.IndexOf("moose");
Console.WriteLine(index); // Output: -1
```

In this case it is up to the caller to check the return value prior to using it:

```csharp
if (index == -1)
    // Handle error, short-circuit processing if necessary
    Console.WriteLine("Item not found");
```

Even in languages that support exceptions, it is often necessary or preferable to return a dedicated error value and require the caller to check it.

One common example is a web API. There is no exception mechanism supported by the HTTP protocol, so the API must return a dedicated error code and require the caller to check it. A typical JSON response from a web service that contains an error might look like this:

```json
{
  "data": null,
  "error": "Item not found",
  "error_code": 404
}
```

The data field on the response forms part of the error contract. In this case the caller tried to fetch an item that did not exist. The caller is expected to check for an error prior to using the data; otherwise they will receive a null value error when they try to use it.

<!-- ... subnote on Result<T> as error contract, but don't need detail as this is not a .NET book... -->

## Exceptions as Error Contracts

Many languages provide a mechanism to define and throw **exceptions**. Exceptions break out of the normal flow of execution and **bubble up** the call stack until they are caught by a handler. This can provide flexibility in how and when errors are handled within the application.

We have already seen several examples of exceptions in the course so far. If we wanted to, we could write our own version of the `IndexOf` method that throws an exception if the item is not found rather than returning a magic value.

```csharp
int CustomIndexOf(List<string> list, string item)
{
    for (int i = 0; i < list.Count; i++)
    {
        if (list[i] == item)
            return i;
    }

    // We've reached the end of the list without finding the item, so it must not be present
    throw new Exception("Item not found");
}
```

Now think about the consequences of this change for the caller:

```csharp
List<string> animals = new()
{
    "cat",
    "dog",
    "mouse"
};

// Will throw an exception if the item is not found in the list
int index = CustomIndexOf(animals, "moose");

// We will never reach this line
Console.WriteLine(index); // Unreachable code
```

To accomodate the new error contract, we would have to wrap the call to `CustomIndexOf` in a try/catch block and handle the exception:

```csharp
try
{
    int index = CustomIndexOf(animals, "moose");
    Console.WriteLine(index);
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

## Which to Use?

There is no right answer when it comes to choosing between return values and exceptions. Each comes with a design tradeoff. For example:

- Return values offer simplicity and clarity. However, if a caller fails to check for the error condition the program may continue to run in a flawed state.
- Exceptions offer flexibility and ensure that the program cannot continue to run in a flawed state. However, they require the caller to handle them in a try/catch block, which adds complexity to the solution.
