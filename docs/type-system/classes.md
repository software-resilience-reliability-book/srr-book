# Classes

The type system provides guarantees about the contents and behavior of a type via class definitions. These definitions tell us what data are available, the class's **properties**, and what functions are available, the class's **methods**.

At its most basic, a class can be a simple container for data. Let's start with a function from our reference project. This function comes from the `InvertTransform` class. The function has been rewritten here without the use of classes:

```csharp
public (int, int, int) Apply(int red, int green, int blue) {
    int newRed = ColorMath.Clamp(255 - red);
    int newGreen = ColorMath.Clamp(255 - green);
    int newBlue = ColorMath.Clamp(255 - blue);
    return (newRed, newGreen, newBlue);
}
```

This function technically works. It takes three integers as input and returns a tuple of three integers. But it can easily lead to mistakes when it is called. The caller receives three anonymous integers with no indication of which is red, green, or blue.

Most of all - this solution is messy. The function tells us that it returns a tuple of three integers, but it does not tell us what the integers represent.

Code is a communication tool, and our code should be self-documenting. Let's look at the version that uses a class:

```csharp
public RgbColor Apply(RgbColor color) {
    int red = ColorMath.Clamp(255 - color.Red);
    int green = ColorMath.Clamp(255 - color.Green);
    int blue = ColorMath.Clamp(255 - color.Blue);
    return new RgbColor(red, green, blue);
}
```

We can immediately see that the function takes a `RgbColor` as input and returns a `RgbColor`. The colors can be accessed as properties on the object, which gives us additional protections: there is less likelihood that a wrong value will be supplied.

Classes serve as more than a way to bundle related data. They serve as a _definition_ of data and operations that can be performed.

This is why we refer to types as contracts. If we pass in an `RgbColor` to a function, we can guarantee that that it will have a `Red`, `Green`, and `Blue` property.
