# Implementing Encapsulation with Modules

**Encapsulation** is the practice of hiding implementation details behind a controlled interface. Used effectively, consumers of that interface gain a simplified abstraction. The set of exposed data and functionality clearly communicates the code's intent.

Referring back to the hierarchy of code units:

## Encapsulation Within Functions

To know what a function does, you look at its **signature**. This contains the functions name, input values (paramaters), and output values (return value). If the function is descriptive enough, you should not have to dig into the code to determine its purpose.

Each function has local variables that the rest of the program doesn't need to know about.

```csharp
// Function signature is the interface.
// It forms the visible boundary to the outside world.
int CountWords(string text)
{
    // The caller does not need to know about these local variables, or any logic
    // and business rules within the function.
    string trimmed = text.Trim();
    string[] words = trimmed.Split(' ', StringSplitOptions.RemoveEmptyEntries);

    // The caller knows only that they will receive a count
    return words.Length;
}
```

A function's signature forms its **Application Programming Interface (API)**. Callers of this API do not need to know the internals of the function.

## Encapsulation Within Classes

Classes extend this by bundling state with behavior at a slightly larger scale. Classes typically hide or expose members (data and functionality) via **access modifier** keywords.

| Access Modifier | Description                                   |
| --------------- | --------------------------------------------- |
| **private**     | Members are accessible only within the class. |
| **public**      | Members are accessible from anywhere.         |

These modifiers define the "rules" of access:

- Use `public` to make a function accessible to any consumer of the class.
- Use `private` to make a function visible only within the class itself.

The `RgbColor` record type needs to ensure that the red, green, and blue values are within the range of 0 to 255 when the object is constructed. To make the code more readable, this functionality has been extracted to a private method, `ValidateRange`. This private method should never be called directly by any code outside of the `RgbColor` class. These callers may only "see" the constructor method.

```csharp
public record RgbColor
{
    // ...

    public RgbColor(int red, int green, int blue)
    {
        ValidateRange(red, nameof(red));
        ValidateRange(green, nameof(green));
        ValidateRange(blue, nameof(blue));

        Red = red;
        Green = green;
        Blue = blue;
    }

    private void ValidateRange(int value, string name)
    {
        if (value < 0 || value > 255) throw new ArgumentOutOfRangeException(name);
    }
}
```

The set of public methods exposed on a class form its API. Callers of this API do not need to know the internals of the class.

<!-- prettier-ignore -->
!!! info "Other Access Modifiers"
    There are other combinations of access modifier that we have not listed, such as a protected method in a class, or a private class within another class. We are focusing on the most common use cases in this section.

## Encapsulation Within Modules

Organizing code into modules provides the same encapsulation benefits as classes and functions. Each module controls access and visibility over its contained classes, and can expose only what is necessary to the consumer of the package.

Modules may use visibility modifiers to control access to their classes.

| Access Modifier | Description                                               |
| --------------- | --------------------------------------------------------- |
| **internal**    | Classes are accessible within the same assembly (module). |
| **public**      | Classes are accessible from outside the module.           |

These modifiers define the "rules" of access:

- Use `public` for classes that are intended to be accessed by any consumer of the module.
- Use `internal` for classes that are intended to be accessed within the module itself.

The `ColorMath` class contains a simple utility method for clamping a value to the range of 0 to 255. This is something we want to be able to use in several places _inside_ the project, but not _outside_ of it.

```csharp
internal static class ColorMath
{
    public static int Clamp(int value) =>
        Math.Clamp(value, 0, 255);
}
```

<!-- TODO: explain how this is used / consumed in the project -->

```csharp
public class InvertTransform : IColorTransform
{
    public RgbColor Apply(RgbColor color) {
        int red = ColorMath.Clamp(255 - color.Red);
        int green = ColorMath.Clamp(255 - color.Green);
        int blue = ColorMath.Clamp(255 - color.Blue);
        return new RgbColor(red, green, blue);
    }
}
```

The set of public classes exposed on a module form its API. Callers of this API do not need to know the internals of the module.

<!-- prettier-ignore -->
!!! info "Encapsulation in Other Languages"
    Other languages may have different implementations of access control. For example, in JavaScript there is no "public" keyword. Instead a module may "export" a public API. In Python, member access control is determined by convention; you simply apply underscore prefixes to private members and this signals to other developers not to use them.
