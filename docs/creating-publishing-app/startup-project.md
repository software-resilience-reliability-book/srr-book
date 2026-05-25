## The Startup Project

One approach to building this project is to begin by putting everything in the same project and refactoring later. This would not be a good idea for a very large project, but for our application the refactor will be simple.

Start by creating a new directory for the project. This directory will have subdirectories for each of the projects that it contains. We've called our root directory "word-sub".

Within this root directory, create the console application in its own subdirectory. It's best to name this new subdirectory for the console application the same as the project name for consistency:

```bash
mkdir WordSub.App
cd WordSub.App
dotnet new console
```

The file structure should now look like this:

```text
word-sub/
└── WordSub.App
    ├── Program.cs
    └── WordSub.App.csproj
```

We can now look at the `csproj` file for the project in more detail:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net10.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>
</Project>
```

What's important to us is the `<OutputType>` element, which is set to `Exe`. This tells the build system that this project is an executable program, not a library.

The only other file is the `Program.cs` file, which contains some demo text from the project template.
