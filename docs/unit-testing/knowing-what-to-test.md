# Knowing What to Test

## What is Test Coverage?

**Test coverage** is a measure of the extent to which a test suite exercises the codebase. There are many automated tools that perform **static analysis** to determine which lines of code are under test and calculate the percentage of overall code that is touched by the test suite.

Trying to maximize this metric is not a productive use of developement time, as test coverage in itself does not guarantee that the codebase is thoroughly tested. It is very easy to write a test that does nothing useful.

This leads to the question: "What parts of the codebase should we test?"

## What is Worth Testing?

Tests may be cheap, but they aren't free. The cost of "too many tests" usually manifests in the form of increased maintenance overhead and cognitive load.

Tests should focus on code that is either high-value or high-risk.

**Test Code That...**

- Implements core domain logic and business rules
- Enforces explicitly defined requirements
- Has high complexity
- Would cause costly or catastrophic failures if broken

Code with these characteristics is typically found in the domain layer, such as our `ColorTransform` project as opposed to the UI layer, the `ColorTransform.Web` project.

**Avoid Testing Code That...**

- Is trivial or has minimal complexity
- Primarily maps one piece of code to another

These cases are better covered by integration or end-to-end tests, discussed in a later chapter.

<!-- prettier-ignore -->
!!! info "What Not to Test"
    Our `RgbColor` class has some code that assigns provided component values to attributes:

    ```csharp
    public RgbColor(int red, int green, int blue)
    {
        ValidateRange(red, nameof(red));
        ValidateRange(green, nameof(green));
        ValidateRange(blue, nameof(blue));

        Red = red;
        Green = green;
        Blue = blue;
    }
    ```

    We did not write tests to ensure that the red, green, and blue values that the caller passed in are correctly assigned to the Red, Green, and Blue attributes on the RgbColor object.

    This is trivial functionality. If a class constructor is not assigning values that were passed in, it would likely cause downstream errors that later tests would catch.
