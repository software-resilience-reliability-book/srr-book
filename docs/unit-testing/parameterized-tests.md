# Parameterized Tests

## What are Parameterized Tests?

**Parameterized tests** are a way to run the same test with different inputs.

Rather than writing multiple tests that have the same Arrange-Act-Assert logic, we can use parameterized tests reuse a single test.

Let's again look at the `IsPassing` function:

```csharp
public static bool IsPassing(int score)
{
    if (score < 0 || score > 100)
        throw new ArgumentOutOfRangeException(nameof(score));

    return score >= 60;
}
```

We defined our segments as follows:

| Category                    | Example Inputs |
| --------------------------- | -------------- |
| Golden Path, Passing Course | 99, 75         |
| Golden Path, Failing Course | 50, 24         |
| Edge Cases / Boundaries     | 0, 100         |
| Error Conditions            | -1, 101        |

There is no need to write a test function each for:

`reports_pass_for_99` and `reports_pass_for_75`

We can make a single test function: `reports_pass_for_passing_score`.

## Creating a Parameterized Test with xUnit

Each testing framework has its own way of creating parameterized tests.

In xUnit, we can use the `Theory` attribute. Here's what our test would look like:

```csharp
[Theory]
[InlineData(99)]
[InlineData(75)]
public void reports_pass_for_passing_score(int score)
{
    var result = IsPassing(score);
    Assert.True(result);
}
```

The `[InlineData]` attribute is used to provide the input values for the test. Whatever is in this attribute will be passed to the test function as the `score` parameter.

The above test will be run twice, once with `99` and once with `75`.

## Providing Multiple Inputs

If you open the `src/ColorTransform/Models/RgbColor` file, you will see that our RGB class does not allow the Red, Green, or Blue values to be outside of the range 0-255. It would be cumbersome to write a test for each of the boundary values of each component.

We can instead use paramaterized testing. Here is a snippet from `tests/ColorTransform.Tests/RgbColorTests.cs`:

```csharp
[Theory]
[InlineData(-1, 0, 0)]
[InlineData(0, -1, 0)]
[InlineData(0, 0, -1)]
[InlineData(256, 0, 0)]
[InlineData(0, 256, 0)]
[InlineData(0, 0, 256)]
public void color_fails_when_component_values_are_out_of_range(int r, int g, int b)
{
    Assert.Throws<ArgumentOutOfRangeException>(() => new RgbColor(r, g, b));
}
```

The first time the test is run, `r` will be `-1`, `g` will be `0`, and `b` will be `0`.

The second time the test is run, `r` will be `0`, `g` will be `-1`, and `b` will be `0`. And so on.

We have tested the `-1` boundary for each component, as well as the `256` boundary for each component.
