# Types of Configuration

"Configuration" may refer to any number of things. Below are a few common sources of configuration values.

## Command Line Arguments

**Command line arguments** are values that are passed to the application at startup via the command line. An example is the `--project` argument to the `dotnet run` command, which specifies the project to run.

By default, the application is launched from the root directory of the project, but we can also launch a specific project by passing the project name as an argument. Here's how we would run the web application included in the reference project if our current working directory in the terminal is the root directory of the project:

```bash
dotnet run --project src/ColorTransform.Web
```

If we instead wanted to run the test harness, we would pass the `ColorTransform.Harness` project name:

```bash
dotnet run --project tests/ColorTransform.Harness
```

Allowing for the project path to be provided provides greater flexibility in how the CLI command can be used.

## Environment Settings

Environment settings are system-level variables that can be read by the application to determine settings or environment. Many modern applications run inside of **containers**, which are isolated environments that are used to run the application - apart from the host operating system. These containers are often configured with environment variables that determine the application's behavior.

An example docker configuration file might have the following environment variables:

```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    environment:
      APP_NAME: "Colorful Solutions LLC"
      SUPPORT_EMAIL: "colorfulsolutions@example.com"
      MAX_UPLOAD_SIZE_MB: 10
```

The same application is often deployed for multiple clients, where each client has their own "version" of the application.

This configuration file comes from a fictional web application that many clients may use. Configuration settings are set under the "environment" key.

While this client may prefer a max upload size of 10MB, another client may prefer a max upload size of 20MB. They can do so in their own configuration file:

```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    environment:
      APP_NAME: "The Modern Palette LLC"
      SUPPORT_EMAIL: "tmp@example.com"
      MAX_UPLOAD_SIZE_MB: 25
```

By extracting these client-specific values to configuration settings, each client is able to have an independent application configuration.

## Configuration File Settings

Configuration file settings are key-value settings that are stored in an application specific configuration file format. We are using this term generally to refer to a broad range of configuration file formats, including JSON, XML, and INI files.

.NET uses a JSON-based configuration file format called `appsettings.json`. While it can store settings that pertain to the .NET environment generally, it can also be used to store application specific settings such as database connection strings, API keys, and other configuration values.

Here are some example settings, organized into sections.

```json
{
  "App": {
    "Name": "Colorful Solutions LLC",
    "SupportEmail": "colorfulsolutions@example.com"
  },
  "Server": {
    "Port": 8080,
    "MaxUploadSizeMb": 10,
    "AllowedHosts": ["localhost", "example.com"]
  },
  "Database": {
    "Host": "localhost",
    "Port": 5432,
    "Name": "myapp_db"
  },
  "Logging": {
    "Level": "Debug",
    "WriteToFile": true,
    "LogFilePath": "/var/log/myapp.log"
  }
}
```

The above settings apply to our development environment. In production, we may want to override some of these settings. One of the most common reasons to do so is to point to a different database server.

```json
{
  // ...
  "Database": {
    "Host": "production-db.example.com",
    "Port": 5432,
    "Name": "production_db"
  }
  // ...
}
```
