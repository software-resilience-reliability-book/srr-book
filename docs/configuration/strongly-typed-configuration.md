# Strongly-Typed Configuration

## Why Use Strongly-Typed Configuration?

The same benefits that we mentioned in the "Leveraging the Type System" section can be applied to configuration settings. By creating custom classes to represent configuration settings, we can ensure that the settings are validated and type-safe.

## Creating a Strongly-Typed Configuration Class

Imagine that we have an application that needs to send confirmation and password reset emails to users. We need to define a host name, port number, and email address for the email server. The configuration might look like this:

```json
{
  "Email": {
    "Host": "smtp.example.com",
    "Port": 587,
    "FromAddress": "no-reply@example.com"
  }
}
```

We can create a strongly-typed class to represent this configuration:

```csharp
public class EmailOptions
{
    [Required]
    public string Host { get; set; }
    [Range(1, 65535)]
    public int Port { get; set; }
    [Required]
    public string FromAddress { get; set; }
}
```

This is simply a class with properties for each of the configuration settings. The data annotations (`[Required]`, `[Range]`) define validation rules that will be enforced at startup.

## Using the Configuration Class

The `EmailOptions` class can now be registered in the `Program.cs` file and provided to any class that needs access to the settings. Assuming `_options` is an instance of `EmailOptions`, we can access the configuration settings like this:

```csharp
// Instead of configuration["Email:Host"]
string host = _options.Host;
// Instead of configuration["Email:Port"]
int port = _options.Port;
// Instead of configuration["Email:FromAddress"]
string from = _options.FromAddress;
```

This approach helps avoid typos in the names of settings, missing keys from the configuration file, and other runtime errors.

<!-- prettier-ignore -->
!!! info "Optional custom title"
    We have skipped over the registration and injection of the `EmailOptions` class in order to focus on the core concept of strongly-typed configuration.

    As of this writing the [Microsoft documentation for `IOptions`](https://learn.microsoft.com/en-us/dotnet/core/extensions/options) is quite technical. We recommend finding a more accessible tutorial if you plan to use strongly typed configurations in .NET.
