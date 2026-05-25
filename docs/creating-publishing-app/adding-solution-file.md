# Adding a Solution File

## What is a Solution File?

We could continue changing directories whenever we need to work on different projects, but using a **solution file** will make this process much easier.

In .NET, the solution file groups related projects together and provides a way to perform operations that span multiple projects. It also defines what should be included in the build output; for example, to exclude test projects from application that is released to production.

## Creating a Solution File

Navigate to the root directory of the project and use the dotnet CLI to create a new solution file:

```bash
cd ..
dotnet new sln
```

This will create a new file called `[root directory].sln` in the root directory. If stuck with the root directory name used earlier, "word-sub", then your project structure should look like this:

```text
word-sub/
├── WordSub
│   ├── WordReplacer.cs
│   └── WordSub.csproj
├── WordSub.App
│   ├── Program.cs
│   └── WordSub.App.csproj
└── word-sub.slnx
```

## Adding Projects to the Solution

To add the projects to the solution, run the following commands:

```bash
dotnet sln add WordSub
dotnet sln add WordSub.App
```

Finally, build the solution to ensure that it works, and run the console application. This time you will need to pass the project name to the `dotnet run` command:

```bash
dotnet build
dotnet run --project WordSub.App
```
