# Companion Code

## Location

This book contains code in two formats:

- Standalone code examples that can be run directly or wired up with minimal effort
- Code examples that are part of a larger solution that is used to demonstrate a concept

The project that is used to illustrate most of the concepts is a [Color Transform Application](https://github.com/software-resilience-reliability-book/color-transform).

We encourage you to clone or download this repository and run the examples for yourself. The best way to learn software development concepts is to read, and try out, existing solutions.

[The Build System](builds/index.md) chapter of this book provides a walkthrough, where a simple console application is created and built using the .NET SDK.

## Running the Code

The Color Transform Application has four projects, which we will approach in the following order:

1. `ColorTransform.Library` - The Color Transform Library. This is a class library that contains the core functionality of the Color Transform Application. It cannot be run directly.

2. `ColorTransform.Harness` - A test harness for the Color Transform Library. It is recommended to use the VS Code debugger to step through the test harness code. Open the `tests/ColorTransform.Harness/Program.cs` file and use the "Run and Debug" feature to start the application.

3. `ColorTransform.Tests` - Tests for the Color Transform Library. These can be run from the root directory with the `dotnet test` command.

4. `ColorTransform.Web` - A web application that uses the Color Transform Library. It can be run from the root directory with the `dotnet run --project src/ColorTransform.Web/ColorTransform.Web.csproj` command. After it is running, you can open it in your browser at `http://localhost:5156`. To stop the application, press `Ctrl+C` in the terminal.

This book will provide guidance on how to run the code as concepts are explained, so you may wish to wait until you come across these sections.
