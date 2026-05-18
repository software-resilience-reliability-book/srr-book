# Print Statements and Logging

## Why Debuggers Don't Always Work

Debuggers are an essential tool for diagnosing runtime errors, but sometimes rigging up a full test harness is not feasible. For example: we often cannot test against the exact data that lives in a production system (the live version of the application that a client is using).

Simple "debug print" statements are a quick and easy way to get a sense of what is happening in the program. This can be in the form of terminal output, or can be more structured logging that writes to a data store.

Take the following example:

```csharp linenums="1"
// Dummy data; we don't actually know these values in advance.
static (string City, int Temperature)[] GetMinDailyTemperatures() =>
    [("New York", 10), ("Los Angeles", 20), ("Chicago", 0), ("Houston", 30)];

static int Divide(int a, int b) => a / b;

static void ProcessData()
{
    (string City, int Temperature)[] data = GetMinDailyTemperatures();

    int result = 0;
    foreach (var (City, Temperature) in data)
    {
        result += Divide(100, Temperature);
    }
}

ProcessData();
```

If we run this code in our test harness we will be able to see a clear error message, but let's pretend that we don't actually know what `GetMinDailyTemperatures` will return. This function may be pulling in values from a weather API whose output changes on a daily basis.

We could find ourselves faced with an `Attempted to divide by zero` error logged in the production application: but by the time we go to rig up our test harness, the data has already changed and the error is no longer reproducible!

## Using Print Statements to Trace Execution

To figure out what is happening we can add print statements to build a trace. This will show us the values being passed in and the result of each operation - the same things we would check if we had a debugger attached:

```csharp linenums="1"
// Dummy data; we don't actually know these values in advance.
static (string City, int Temperature)[] GetMinDailyTemperatures() =>
    [("New York", 10), ("Los Angeles", 20), ("Chicago", 0), ("Houston", 30)];

static int Divide(int a, int b) => a / b;

static void ProcessData()
{
    Console.WriteLine("DEBUG: Entering ProcessData");
    (string City, int Temperature)[] data = GetMinDailyTemperatures();
    Console.WriteLine($"DEBUG: Retrieved {data.Length} items");

    int result = 0;
    foreach (var (City, Temperature) in data)
    {
        Console.WriteLine($"DEBUG: Processing city {City}, temperature {Temperature}");
        result += Divide(100, Temperature);
        Console.WriteLine($"DEBUG: result is now {result}");
    }

    Console.WriteLine($"DEBUG: Final result: {result}");
}

ProcessData();
```

When we run this code we will see the following output:

```text
DEBUG: Entering ProcessData
DEBUG: Retrieved 4 items
DEBUG: Processing city New York, temperature 10
DEBUG: result is now 10
DEBUG: Processing city Los Angeles, temperature 20
DEBUG: result is now 15
DEBUG: Processing city Chicago, temperature 0
Unhandled exception. System.DivideByZeroException: Attempted to divide by zero.
```

The next time we see this error we can check the logs and pinpoint the issue: The daily min temperature for Chicago was 0 degrees on this particular day.

<!-- prettier-ignore -->
!!! info "Toggling Logging and Trace Statements"
    We kept the example above simple by using `Console.WriteLine` function calls. This is perfectly valid to get quick feedback during active development, but should not be used in production code.

    In a real-world application we would typically add a way to configure the level of logging, and where the output is written to. We will look at how to use configuration files to do this in a later chapter.
