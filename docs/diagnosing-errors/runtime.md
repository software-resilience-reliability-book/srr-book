# Runtime Errors

## What is a Runtime Error?

Certain types of errors cannot be detected in advance of the program being run. For example, if we do not know what type of input will be provided to the program we cannot possibly ensure that it is correct at compile time.

**Runtime errors** are problems that happen while a program is running, not while it is being written or compiled. These errors often occur because something unexpected happens while the program is trying to do its work. Examples of common runtime errors include:

- Accessing an item in a collection that doesn't exist
- Trying to use an empty value or record
- Trying to use a file that isn't there
- Trying to connect to the internet or a network when it is not available
- Dividing a number by zero

You will know that your program encountered a runtime error when it throws an **exception**. At this point the exception must be handled, or the program will crash.
