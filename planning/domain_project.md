# Companion Code Project

Color Transformer Application:

A series of functions that take either a single hex argument or a list of hex arguments and return a single or aggregate operation result.

- Invert
- Grayscale
- Brighten
- ???

Example arguments:

- Single hex argument: `#FF0000`
- List of hex arguments: `#FF0000 #00FF00 #0000FF`

---

ColorTransformer/
├── IColorTransform.cs ← single-operation interface
├── Transforms/
│ ├── InvertTransform.cs
│ ├── GrayscaleTransform.cs
│ └── BrightenTransform.cs
├── ColorPalette.cs ← holds IReadOnlyList<RgbColor>, the stateful object
├── PaletteTransformer.cs ← applies an IColorTransform to a palette
└── ColorParser.cs ← parses hex strings into RgbColor instances

```csharp
public interface IColorTransform
{
    RgbColor Apply(RgbColor color);
}

public class InvertTransform : IColorTransform
{
    public RgbColor Apply(RgbColor color) =>
        new RgbColor(255 - color.R, 255 - color.G, 255 - color.B);
}
```

```csharp
public class PaletteTransformer
{
    private readonly IColorTransform _transform;

    public PaletteTransformer(IColorTransform transform)
    {
        _transform = transform;
    }

    public ColorPalette Apply(ColorPalette palette) =>
        new ColorPalette(palette.Colors.Select(_transform.Apply));
}
```

```csharp
public class ColorPalette
{
    public IReadOnlyList<RgbColor> Colors { get; }

    public ColorPalette(IEnumerable<RgbColor> colors)
    {
        Colors = colors.ToList().AsReadOnly();
    }
}
```
