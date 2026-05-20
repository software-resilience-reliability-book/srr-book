# Enumerations

## Unreliable Parameter Values

In many cases our program needs to accept a parameter that is one of a fixed set of values. While this can be done with strings, this method is unreliable. Take the following function:

```csharp
string FormatPrice(string currency, decimal amount) {
    if (currency == "USD") {
        return $"${amount:N2}";
    } else if (currency == "EUR") {
        return $"€{amount:N2}";
    } else {
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
enum Currency
{
    USD,
    EUR,
}
```

...

## Reference Example: The Grayscale Formula

Let's look at how enums are used in the reference project.

...

```csharp
public class GrayscaleTransform(GrayscaleFormula formula = GrayscaleFormula.Average) : IColorTransform
{
    public RgbColor Apply(RgbColor color)
    {
        int grayscale = formula switch
        {
            GrayscaleFormula.Average => ToAverage(color),
            GrayscaleFormula.Luminance => ToLuminance(color),
            _ => throw new ArgumentOutOfRangeException(nameof(formula)),
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
