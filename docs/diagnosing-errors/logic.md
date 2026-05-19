# Logic Errors

## What is a Logic Error?

A **logic error** is a bug in the program that causes it to behave incorrectly, but not in a way that causes it to crash or throw an exception.

This may come in the form of simple developer mistakes, or business logic rules that are not enforced by the application.

The following code snippet contains a logic error:

```csharp linenums="1"
int[] scores = { 85, 90, 78, 92, 88 };
int total = 0;

for (int i = 0; i < scores.Length; i++)
    total += scores[i];

double average = total / scores.Length;  // integer division truncates
Console.WriteLine($"Average score: {average}");  // prints 86, should be 86.6
```

If you try running this snippet of code, you will see that it does not crash - there is no runtime error. However, the average is calculated as 86, when it should be 86.6. This is a logic error.

In C#, if you divide two integers the result will be an integer. It will truncate the decimal portion of the result, even when we declare the result data type as a double (a data type that supports fractional values).

To fix it we can cast the divisor to a double before performing the division:

```csharp linenums="7"
double average = total / (double)scores.Length;
```

Now when you run the code, you will see that the average is calculated correctly as 86.6.

## Silent Failures

One particularly insidious type of logic error is a **silent failure**. A silent failure is a logic error that is subtle enough to remain undetected for long periods of time.

These errors often manifest themselves as intermittent bugs, where the program appears to work most of the time, but occasionally fails in a way that is not easily reproducible.

<!-- prettier-ignore -->
!!! info "Ephemeral Bugs"
    Systems that involve parallel processing, asynchronous operations, or other complex behaviors are particularly susceptible to silent failures.

    In one case we worked on a system that intermittently calculated a forecast as all zeroes - reporting to the client that they had thousands of dollars more than they actually did!

    We ended up adding extensive trace logging, and after more than two weeks of scrutinizing the output found that it was due to a **race condition** in the code. One process zeroed out some of the values needed for a calculation that the other process was performing, while this other process was in the middle of its own calculation. The bug only occured when the two processes "stepped on each other" at just the right time.
