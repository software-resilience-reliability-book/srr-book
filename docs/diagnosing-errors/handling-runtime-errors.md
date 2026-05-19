# Handling Runtime Errors

## Failing Fast

Depending on the type of error and complexity of the system handling it, it may be appropriate to **fail fast**. This means that the application should immediately stop after logging the error information.

A fail fast approach is appropriate when continuing the application would potentially put it in a corrupt or unpredictable state. This usually happens when the error is difficult to recover from or of a type that is not expected to occur under normal operation.

Most applications have a **global error handler** near the entry point of the application, for example in the `Program.cs` file. This handler will catch all unhandled exceptions and log them. This is a good place to fail fast.

In most cases failing fast is used as a last resort. However, failing fast is better than continuing to run an application in a faulty state, which may lead to silent failures or data corruption.

## Failing Gracefully

**Failing gracefully** means that an application continues to run even after experiencing an error. Upon encountering an error the application may do any of the following:

- Log the error for later review
- Display a secure message to the user
- Retry the operation
- Fall back to a default value
- Continue to the next operation
- Terminate the application (to be avoided if possible)

In order to fail gracefully, the application must signal that it has encountered an error. This forms part of the error contract of the application.
