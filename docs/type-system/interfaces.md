# Interfaces

Interfaces are related to classes in that they establish guarantees about data and behavior of a type. Unlike classes, however, interfaces do not provide values for the data or implementations for the behavior. They rely on a class to implement the interface.

Let's again refer to our reference project. The library offers several different ways to transform one color to another. Each of these ways has its own class that implements the `IColorTransform` interface.

```csharp
public interface IColorTransform
{
    RgbColor Apply(RgbColor color);
}
```

Any class that implements the `IColorTransform` interface is guaranteed to have an `Apply` method that takes a `RgbColor` as input and returns a `RgbColor`. If not the code will not compile.

This becomes useful when we need to write a function that must transform a color, but doesn't need to know which transform that it will use.

```csharp
public class PaletteTransformer
{
    private readonly IColorTransform _transform;

    public PaletteTransformer(IColorTransform transform)
    {
        _transform = transform;
    }

    public ColorPalette Transform(ColorPalette palette)
    {
        var transformedColors = new List<RgbColor>();
        foreach (var color in palette.Colors)
        {
            transformedColors.Add(_transform.Apply(color));
        }
        return new ColorPalette(transformedColors, palette.Name);
    }
}
```

The `PaletteTransformer` class is responsible for applying a color transform to a color palette, which contains a collection of colors. It takes an `IColorTransform` as a dependency in its constructor. This allows us to inject different transform implementations into the class, such as `InvertTransform` or `TintTransform`.

`PalleteTransformer` calls the `Apply` method on whichever class that it is holding a reference to (`_transform.Apply`). The `_transform` field may hold a reference to an `InvertTransform` or a `TintTransform`, but it doesn't matter to the `PaletteTransformer` class.
