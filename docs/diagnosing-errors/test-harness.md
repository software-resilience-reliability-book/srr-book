# Test Harnesses

## Creating a Test Harness

To reproduce a runtime error, we need to create a **test harness** that can control the environment and reproduce the error. This can be as simple as a console application that can be run from the command line, or a more complex web application that can be deployed to a test environment.

The primary goal of a test harness is to exactly match the environment with the error:

- Same versions of code and dependencies
- Same configuration values
- Same input data

<mark>TODO:</mark>

- Write finished product of example domain application.
- Break apart into pieces as needed for chapter snippets.
- This one should be extremely basic; it will just show that the library has no startup app, so a test harness is needed. Use a scenario where the user has reported a problem with some input, so we just call the library with that input.

<mark>END TODO</mark>

<!-- prettier-ignore -->
!!! check "Check Your Exception Settings"
    Most IDEs offer a way to configure which types of exceptions are caught by the debugger. By default, VS Code will only break on unhandled exceptions, that are not wrapped in a `try`/`catch` block.

    If you want to break on all exceptions, open the "Run and Debug" menu and make sure that "All Exceptions" is checked under the "Breakpoints" submenu.

    ![VS Code exception settings menu](../images/exception-settings.png)
