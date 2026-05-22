# Configuration and Environment Management

An application's **configuration** refers to the collection of settings that determine the application's environment and behavior, but are not part of the application's code. These settings are typically stored in a configuration file, and are loaded at runtime.

In this chapter we will examine several sources of configuration values, and come to understand when defining configuration values is beneficial.

<!-- prettier-ignore -->
!!! info "Why are there Two Configuration Files?"
    When you create a .NET project it will often create two configuration files: `appsettings.json` and `appsettings.Development.json`.

    The `appsettings.json` file contains the application's base/default configuration. The `appsettings.Development.json` file contains overrides that are specific to the development environment.

    This is a common practice in other technologies as well.
