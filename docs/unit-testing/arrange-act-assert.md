# The Arrange-Act-Assert Pattern

## The Goal of a Unit Test

Tests should be treated as their own self-contained program, much like running a controlled experiment in a lab. Each test should be **repeatable** and **deterministic**. The output of a test should be the same every time it is run.

The **Arrange-Act-Assert (AAA)** pattern can be used to achieve this:

| Step    | Description                                                                                                                 |
| ------- | --------------------------------------------------------------------------------------------------------------------------- |
| Arrange | Set up the test environment. This includes creating any objects and data that the **system under test** requires.           |
| Act     | Perform the action that is being tested. This usually involves the system under test calling a method that is being tested. |
| Assert  | Verify the expected outcome. This includes checking the result of the action.                                               |

## Examining a Unit Test

Let's explore the AAA pattern by example. Our color transform library contains a `HexConverter` class. This class has a `FromHexString` method that converts a hex string, such as "#FF0000", to its equivalent RGB color representation, such as "(255, 0, 0)".

The **model** for the RGB color is mostly a simple data container with properties for the red, green, and blue components:

```csharp
public record RgbColor
{
    public int Red { get; }
    public int Green { get; }
    public int Blue { get; }
    // ...
}
```

The test for the `FromHexString` method is as follows:

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

Let's break down our steps one by one:

`Arrange`
: We create an instance of the `HexConverter` class. That was all that was needed to set up the test environment.

`Act`
: We call the `FromHexString` method with the string "#000000". This is the action that is being tested.

`Assert`
: We verify that the result is an RGB color with the red, green, and blue components all set to 0. This is the expected outcome of the action. If the results are not as expected, the test will report a failure.

## Creating a Failing Test

Let's modify our implementation of the `FromHexString` method so that we can see what a failing test looks like. Open the `src/ColorTransform/Utilities/HexConverter.cs` file and check the following lines:

```csharp linenums="21"
return new RgbColor(
    Convert.ToInt32(hex[0..2], 16), // red
    Convert.ToInt32(hex[2..4], 16), // green
    Convert.ToInt32(hex[4..6], 16) // blue
);
```

In this case `hex` is the hex string that was passed into the function. The `0..2` is a range that starts at index 0 and goes up to, but not including, index 2. This pulls off the first two characters of the hex string - the red component.

`2..4` does the same for the next two characters - the green component.

`4..6` does the same for the last two characters - the blue component.

To break our code, change the last line to only go to index 5:

```csharp linenums="21"
return new RgbColor(
    Convert.ToInt32(hex[0..2], 16), // red
    Convert.ToInt32(hex[2..4], 16), // green
    Convert.ToInt32(hex[4..5], 16) // blue
);
```

## Interpreting the Test Results

Now run the tests again. You should see a failure:

```text linenums="1"
mpjovanovich: dotnet test
Restore complete (0.6s)
  ColorTransform net10.0 succeeded (0.1s) → src/ColorTransform/bin/Debug/net10.0/ColorTransform.dll
  ColorTransform.Tests net10.0 succeeded (0.1s) → tests/ColorTransform.Tests/bin/Debug/net10.0/ColorTransform.Tests.dll
[xUnit.net 00:00:00.00] xUnit.net VSTest Adapter v3.1.4+50e68bbb8b (64-bit .NET 10.0.7)
[xUnit.net 00:00:00.05]   Discovering: ColorTransform.Tests
[xUnit.net 00:00:00.11]   Discovered:  ColorTransform.Tests
[xUnit.net 00:00:00.14]   Starting:    ColorTransform.Tests
[xUnit.net 00:00:00.21]     ColorTransform.Tests.HexConverterTests.hex_string_creates_rgb_color_when_valid [FAIL]
[xUnit.net 00:00:00.21]       Assert.Equal() Failure: Values differ
[xUnit.net 00:00:00.21]       Expected: 17
[xUnit.net 00:00:00.21]       Actual:   1
[xUnit.net 00:00:00.21]       Stack Trace:
[xUnit.net 00:00:00.21]         /home/mpjovanovich/git/color-transform/tests/ColorTransform.Tests/HexConverterTests.cs(18,0): at ColorTransform.Tests.HexConverterTests.hex_string_creates_rgb_color_when_valid()
[xUnit.net 00:00:00.21]            at System.Reflection.MethodBaseInvoker.InterpretedInvoke_Method(Object obj, IntPtr* args)
[xUnit.net 00:00:00.21]            at System.Reflection.MethodBaseInvoker.InvokeWithNoArgs(Object obj, BindingFlags invokeAttr)
[xUnit.net 00:00:00.21]   Finished:    ColorTransform.Tests
  ColorTransform.Tests test net10.0 failed with 1 error(s) (0.7s)
    /home/mpjovanovich/git/color-transform/tests/ColorTransform.Tests/HexConverterTests.cs(18): error TESTERROR:
      ColorTransform.Tests.HexConverterTests.hex_string_creates_rgb_color_when_valid (8ms): Error Message: Assert.Equal() Failure: Values differ
      Expected: 17
      Actual:   1
      Stack Trace:
         at ColorTransform.Tests.HexConverterTests.hex_string_creates_rgb_color_when_valid() in /home/mpjovanovich/git/color-transform/tests/Col
      orTransform.Tests/HexConverterTests.cs:line 18
         at System.Reflection.MethodBaseInvoker.InterpretedInvoke_Method(Object obj, IntPtr* args)
         at System.Reflection.MethodBaseInvoker.InvokeWithNoArgs(Object obj, BindingFlags invokeAttr)

Test summary: total: 31, failed: 1, succeeded: 30, skipped: 0, duration: 0.7s
Build failed with 1 error(s) in 1.7s
```

The summary tells us that there was one failure.

`ColorTransform.Tests.HexConverterTests.hex_string_creates_rgb_color_when_valid [FAIL]` tells us the name of the test that failed.

`Assert.Equal() Failure: Values differ` tells us that the test failed because the expected and actual values were different.

`Expected: 17` tells us the expected value that was passed to the `Assert.Equal` method.

`Actual:   1` tells us the actual value that was returned by the test.

In this case, since we only pulled off the first character for the blue component it did not convert `11` to it's equivalent decimal value of 17. It converted only the first character, `1`, to 1.
