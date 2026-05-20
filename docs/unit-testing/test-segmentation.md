# Test Segmentation

## Segmenting Inputs

Inputs to the system under test can be grouped to help you design tests systematically:

### Golden Path

Input that represents the way that callers will use the system under test under normal circumstances.

### Edge Cases

Input that is technically valid, but not likely to be encountered in everyday use. The following are some examples of edge cases:

| Input Type | Examples                                                   |
| ---------- | ---------------------------------------------------------- |
| String     | empty strings, all-whitespace tokens, non-ASCII characters |
| List       | empty list, list with duplicate values                     |
| Numeric    | zero, negative numbers, fractional numbers                 |

### Boundaries

Inputs at the edges of a rule—minimum and maximum allowed sizes or values, and the first value _just outside_ the allowed range.

Errors at the boundaries are often off-by-one errors; for example, trying to read outside the bounds of an array.

It is a good idea to test:

- The minimum value (e.g. the first element of an array)
- The maximum value (e.g. the last element of an array)

If the error contract should explicity reject values outside of the boundaries, than those should be tested as error conditions as well.

### Error Conditions

Inputs that violate the contract and must produce a defined failure (exception, error result, etc.). The failure mode should be explicitly tested.

## Segmentation by Example

Assume we have the following function that checks if a student has passed a course:

```csharp
public static bool IsPassing(int score)
{
    if (score < 0 || score > 100)
        throw new ArgumentOutOfRangeException(nameof(score));

    return score >= 60;
}
```

We might segment inputs as follows:

| Category                    | Example Inputs |
| --------------------------- | -------------- |
| Golden Path, Passing Course | 99, 75         |
| Golden Path, Failing Course | 50, 24         |
| Edge Cases / Boundaries     | 0, 100         |
| Error Conditions            | -1, 101        |
