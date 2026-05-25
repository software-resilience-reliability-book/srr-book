# Packaging the Application

So far we have been building and running the application on our own machine. **Packaging** is the step where we create a folder of files that someone else can copy and run—without your source code, project files, or development tools.

<!-- prettier-ignore -->
!!! info "What &quot;Publishing&quot; Means Here"
    The .NET CLI uses the command name `dotnet publish` for this step. This can bring to mind the idea of publishing to a public registry or website where others can download and use the package. However, in this context it simply means creating a release version of the application.

## Release vs Debug

During development we usually build in **Debug** configuration. Debug builds are larger, slower, and include extra information that helps the debugger map running code back to our source files.

For distribution we use **Release** configuration. Release builds are optimized for running the app, not for stepping through it line by line in the debugger.

You do not need to change any project files to switch configurations. We pass `-c Release` on the command line when we package the app.

## Creating the Package

From the root directory of the solution run:

```bash
dotnet publish WordSub.App/WordSub.App.csproj -c Release -o ./publish -p:DebugType=none -p:DebugSymbols=false
```

| Part of the command              | What it does                                                     |
| -------------------------------- | ---------------------------------------------------------------- |
| `dotnet publish`                 | Build the app and gather everything needed to run it elsewhere   |
| `WordSub.App/WordSub.App.csproj` | The executable project we want to package                        |
| `-c Release`                     | Use the Release configuration                                    |
| `-o ./publish`                   | Write output into a new `publish` folder under the solution root |
| `-p:DebugType=none`              | Disable debug symbols                                            |
| `-p:DebugSymbols=false`          | Disable debug symbols                                            |

When the command finishes, you should see a message indicating success and a path ending in `publish`.

Your root directory will now have a `publish` folder:

```text
word-sub/publish/
├── Bogus.dll
├── WordSub.App
├── WordSub.App.deps.json
├── WordSub.App.dll
├── WordSub.App.runtimeconfig.json
└── WordSub.dll
```

## What Is in the Package

The `publish` folder contains **compiled** output—already translated from C# into a form the .NET runtime can execute. For example, the `WordSub.App.dll` file is the compiled version of the main program (`Program.cs`) and the `WordSub.dll` file is the compiled version of the library project (`WordSub.cs`).

The packaged application does not contain source code, debugging information, or any intermediate build artifacts.

<!-- prettier-ignore -->
!!! info "Proving the Files are Compiled"
    If you try opening the dll files in a text editor you will see a lot of gibberish. This is becase the text editor is trying to interpret the binary file as text - ASCII or Unicode characters. Because nothing lines up with the encoding scheme, the text editor symbols appear random.

## Running the CLI Application

All of the files in `publish` folder make up the packaged application.

To run the packaged application, users will need to install the .NET runtime on their machine. After that they can run it on their machine by navigating to the directory containing the files and running the `dotnet` command.

```bash
dotnet WordSub.App.dll
```

You can try this yourself using your publish directory; or better yet, copy and paste the contents of the publish directory into a new directory and try it there. This will better illustrate how the files no longer depend on anything in the source project.
