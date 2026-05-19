# Content Planning

mkdocs preview command:

```
mkdocs serve --livereload
```

## Book

## Needed Topics (in order of likeliness to make scope)

How to run the demo app:

- Test harness project (debugger in VS Code)
- Test project (`dotnet test`)
- Web app (`dotnet run --project ...`)

Configuration settings

- Footer text configuration for "client name" to go after copyright

maybe...

- Config: "EnabledTransforms": ["invert", "grayscale-average", "tint"]
- Development adds some other one like "grayscale-luminosity"

Adding third party dependencies

- Just use xUnit as an example. Don't muddy things up with more complexity.

Custom exception types

- Just call attention to the fact that we're only catching exceptions that the library throws. Note that for third party libraries we should read the documentation to understand what exceptions are thrown and how to handle them. No need to create our own types.

Dev vs production environments

- Production: user sees a fixed message (“We couldn’t apply that transform.”).
- Development: same failure can show ex.Message (or type + message) in the alert.
- Rig up a dropdown option that deliberately fails with a "detailed error message" to demo this

Configuring build output

- May not have time for practical example.

## Consumer Project

```
├── src/
│ ├── ColorTransform/
│ └── ColorTransform.App/
```

ColorTransform.App = very light basic Blazor app that consumes the library and is there only to illustrate integration testing; shows that the library is meant to be consumed by other projects.

---

## Examples from full color transformation library solution

Tast harnessing: Program.cs as means to step into HexConverter
Test naming conventions: all of the tests
Isolating test functionality / mocks: PaletteTransformerTest (see the mock)
Protecting invariants / guard clauses: Constructor for RgbColor ensures we can assume a valid color after construction
Config settings: client name in footer
Dependency injection (if we get to this): PaletteTransformer
Exception handling / Dev vs Prod config difference: Web app has a fail case build in, which we handle differently per environment.

## TODO

Make the icons in the asides consistent.

Make chapter pages look like chapter pages.

Nice to have: a map of how each project in the final solution references to each other

- src/library
- src/api or web or whatever consumer
- tests/harness
- tests/tests

## Chapters

These do not need to be (and should not be) a one to one mapping with the course modules.

They should be granular, so that pagination works well and it reads like a text.
