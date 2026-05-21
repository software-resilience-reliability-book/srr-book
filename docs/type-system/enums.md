# Enumerations

## Restricting Parameter Values

In many cases our program needs to accept a parameter that is one of a fixed set of values. While this can be done with strings, this method is unreliable. Take the following function:

```csharp
string FormatPrice(string currency, decimal amount) {
    switch (currency) {
        case "USD":
            return $"${amount:N2}";
        case "EUR":
            return $"€{amount:N2}";
        default:
            throw new ArgumentException("Invalid currency");
    }
}

string price = FormatPrice("USD", 100.00m);
Console.WriteLine(price); // Output: $100.00
```

The function supports a currency of either "USD" or "EUR", but there is no guaranteed that the caller will provide one of these. The case sensitivity makes this even more fragile.

## Using an Enum to Improve Reliability

We can improve the above function by creating an **enum** for the currency. An enum, or enumeration, is a type that defines a set of named constants. In C# we define an enum using the `enum` keyword.

```csharp
// Currency.cs
enum Currency
{
    USD,
    EUR,
}
```

The enum is its own type, so we can plug it into our function as a parameter.

```csharp
// Program.cs
string FormatPrice(Currency currency, decimal amount) {
    switch (currency) {
        case Currency.USD:
            return $"${amount:N2}";
        case Currency.EUR:
            return $"€{amount:N2}";
        default:
            throw new ArgumentException("Invalid currency");
    }
}

string price = FormatPrice(Currency.USD, 100.00m);
Console.WriteLine(price); // Output: $100.00
```

It is now no longer possible to provide any value other than `Currency.USD` or `Currency.EUR` to the `FormatPrice` function. The enum type has documented the valid values for this parameter.

<!-- prettier-ignore -->
!!! check "IDE Autocomplete Support"
    Another benefit is that the IDE will now provide autocomplete for the valid values of the `Currency` enum.

    Try creating it out in VS Code: after typing `Currency.` you should see suggestions for the valid values of the `Currency` enum.

## Reference Example: The Grayscale Formula

As another example, let's look at how enums are used in the reference project.

```csharp
// GrayscaleFormula.cs
enum GrayscaleFormula
{
    Average,
    Luminance,
}
```

```csharp
// GrayscaleTransform.cs
public class GrayscaleTransform(GrayscaleFormula formula = GrayscaleFormula.Average) : IColorTransform
{
    public RgbColor Apply(RgbColor color)
    {
        int grayscale = formula switch
        {
            GrayscaleFormula.Average => ToAverage(color),
            GrayscaleFormula.Luminance => ToLuminance(color),
            _ => throw new ArgumentException(nameof(formula)),
        };
        return new RgbColor(grayscale, grayscale, grayscale);
    }

    private static int ToAverage(RgbColor color) =>
        (color.Red + color.Green + color.Blue) / 3;

    private static int ToLuminance(RgbColor color) =>
        // This is the int "fast luminance" algorithm.
        (2 * color.Red + 5 * color.Green + 1 * color.Blue) / 8;
}
```

The `GrayscaleTransform` class needs to know which formula to use in the `Apply` method when converting a color to grayscale. It will call either `ToAverage` or `ToLuminance` depending on the formula provided to the switch statement.

Rather than allowing arbitrary strings, we use an enum to restrict the valid values for the `formula` parameter. By default it is set to use `GrayscaleFormula.Average`, but the caller can specify `GrayscaleFormula.Luminance` if they want to use the luminance formula instead.

## Additional Resources

For additional resources on enums, see the following Microsoft docs:

- [System.Enum class](https://learn.microsoft.com/en-us/dotnet/fundamentals/runtime-libraries/system-enum)
