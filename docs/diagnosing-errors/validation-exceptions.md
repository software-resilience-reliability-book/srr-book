# Validating Runtime Input

## Handling Expected Runtime Errors

<!-- In some cases, we can anticipate that an error will occur and handle it appropriately. For example, if we are expecting a user to provide a valid email address, we can validate the input before processing it.

```csharp linenums="1"
static bool IsValidEmail(string email) =>
    email.Contains("@") && email.Contains(".");

static void ProcessEmail(string email)
{
    if (!IsValidEmail(email))
    {
        throw new ArgumentException("Invalid email address");
    }
}
```

Prefer validation to exception handling when possible.

Exceptions form part of the contract of the application. It is the caller's responsibility to handle them.

Alternatives to exceptions: .NET example would be Result<T>

This will need broken into multiple pages, so may as well do so for compile-time error page as well.

-->
