# Writing Effective Tests

## Naming Conventions

Borrowing again from Khorikov's book, some recommendations for naming tests are:

- _"Name the test as if you were describing the scenario to a non-programmer who is familiar with the problem domain"_. Someone with an understanding of the application should be able to read the names of the tests and easily know what each is verifying.
- _"Don't follow a rigid naming policy"_. There is no need to apply artificial constraints to test names just to make them fit a naming scheme.

Refactoring code is a common practice, and method names often change. In order to ensure that tests are resistent to refactoring, it is best to avoid tying the test name to a particular method.

## Fixing an Earlier Test

Let's again bring up our test from earlier:

```csharp
[Fact]
public void hex_string_creates_rgb_color_when_valid()
{
    var converter = new HexConverter();

    var color = converter.FromHexString("#FF5511");

    Assert.Equal(255, color.Red);
    Assert.Equal(85, color.Green);
    Assert.Equal(17, color.Blue);
}
```

While writing this section we noticed that the name for this test doesn't meet the first recommendation from above. If we were to hand this off to a non-programmer, how would they interpret "creates RGB color"?

A better name for this test is `hex_string_creates_correct_rbg_component_values`. That is what this test really verifies.

<!-- prettier-ignore -->
!!! info "Aren't We Testing Multiple Things?"
    Sticking with our "single, atomic fact about a unit of behavior" definition for a test, we should typically aim for out tests to assert "one thing per test". The test above is actually testing that each component is correct, so we could have written three tests for it: one to verify the red value, one for green, and one for blue.

    In this case we considered the multiple assertions to be acceptible for this unit of behavior, but this is more of an exception to the general rule. It is ideal to have a test assert only one thing. Tests are cheap, and it is okay to have many tests.

## Creating a Test Suite

Suppose we want to test the following functionality:

```csharp
public RgbColor FromHexString(string hex)
{
    hex = hex.TrimStart('#');

    if (hex.Length != 6)
        throw new ArgumentException("Hex color must be 6 characters.", nameof(hex));

    if (!System.Text.RegularExpressions.Regex.IsMatch(hex, "^[0-9A-Fa-f]{6}$"))
        throw new ArgumentException("Hex color must contain only hex characters.", nameof(hex));

    return new RgbColor(
        Convert.ToInt32(hex[0..2], 16),
        Convert.ToInt32(hex[2..4], 16),
        Convert.ToInt32(hex[4..6], 16)
    );
}
```

Let's consider the external behavior that should be verified by our tests:

- It should be okay to pass in a hex string with a leading `#` character.
- It should be okay to pass in a hex string without a leading `#` character.
- A hex string that is not 6 characters long should be rejected.
- A hex string that contains characters other than hex characters (0-9, A-F, a-f) should be rejected.
- When a valid 6-character hex string is provided, the `FromHexString` method should return an `RgbColor` object with the correct RGB component values.

We could break these down into the following tests, one per behavior:

- `hex_string_with_leading_hash_creates_rgb_color`
- `hex_string_without_leading_hash_creates_rgb_color`
- `hex_string_fails_when_not_six_characters`
- `hex_string_fails_when_contains_invalid_hex_characters`
- `hex_string_creates_correct_rbg_component_values`

If we do this, however, it would be difficult to write the first two tests without also verifying the bahavior of the last test. We can instead prefer this list:

- `hex_string_fails_when_not_six_characters`
- `hex_string_fails_when_contains_invalid_hex_characters`
- `hex_string_with_leading_hash_creates_correct_rbg_component_values`
- `hex_string_without_leading_hash_creates_correct_rbg_component_values`

## Summary of What to Test

We can view our system under test (in this case the `FromHexString` method) as a black box. We can only see the inputs and outputs, not the internal workings.

Our test suite from above tested the following:

| Behavior         | Description                                                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Return Values    | Test all segmented input / output combinations.                                                                                                                        |
| Error Conditions | Test that the error contract for the system under test is met. If an exception should be thrown, check for this. If an error value should be returned, check for this. |
