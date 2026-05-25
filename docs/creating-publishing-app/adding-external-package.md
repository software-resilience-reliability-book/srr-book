# Adding an External Package

## External Dependencies

Applications may depend on modules that were authored by the same team, or modules that were authored by a different team outside of the organization. Modules containing code that we have control over are **internal** dependencies. Modules containing code that we do not have control over are **external** dependencies.

For this application we are not going to write the "randomness" logic ourselves. We will rely on an existing third-party library to provide this functionality.

## Adding the `Bogus` Package

We will use the `Bogus` package to generate random words for the word replacement logic. This package will be used by the `WordReplacer` class, so use the `cd` command to navigate back to the WordSub subdirectory. To add the package, run the following command:

```bash
cd ../WordSub
dotnet add package Bogus --version 35.6.5
```

The `Bogus` library is published in an online NuGet package repository. The NuGet package manager resolves the name, downloads the package from the repository, and adds the appropriate reference to the `WordSub` project.

In this case, we have also included the `--version` flag to specify the version of the package we want to use. This ensures that the demo will still work if the package is updated in the future.

The following was added to the `WordSub.csproj` file:

```xml
<ItemGroup>
  <PackageReference Include="Bogus" Version="35.6.5" />
</ItemGroup>
```

Unlike the internal project reference, this uses the `PackageReference` element to specify the package, and contains no path information to point at a project on our local machine. `Bogus` is not our code; we are simply using it in our library.
