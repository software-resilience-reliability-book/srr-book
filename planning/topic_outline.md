## Module 0: Course Resources

- "Course Guide" document, as was done with other courses. This shows expected prerequisite knowledge, intended way to move through modules, where to find resources and common FAQ info. 
- C# survival doc, mostly pointing to external resources

## Module 1: Understanding Build Systems

- What a build does (compile, resolve references, produce artifacts)
- The .NET build pipeline: `dotnet restore`, `build`, `publish`
- Reading build output: warnings vs errors
- Common build failures: missing packages, version conflicts, missing references
- Understanding that the IDE debugger is its own program separate from the (usually CLI driven) build process

## Module 2: Testing Fundamentals and Test Types

- Why tests exist: regression detection, documentation of intent, requirements verification
- Unit, integration, end-to-end — definitions and tradeoffs
- Arrange-Act-Assert; red green refactor
- What makes a test valuable (verifies outcomes, not implementation)
- note: keep this very introductory

## Module 3: Recognizing and Diagnosing Common Errors

- Compile-time vs runtime vs logic errors, and how these manifest
- Exception bubbling and best practices for handling
- Reading stack traces
- Silent failures?
- Errors form part of the contract (expected behavior) of the application and should be included in tests. 

## Module : Leveraging the Type System to Strengthen Software

- Using types to prevent invalid states
- Enums instead of magic values
- DTOs and layer boundaries
- Custom exception types

## Module : Configuration and Externalized Settings

- Why externalize: deployment flexibility, the image server / file path example
- `appsettings.json`
- Strongly-typed configuration, noting that configuration failures are typically critical and should be handled with a "fail fast" approach. 
- What belongs in config vs code

## Module : Environment Management

- What "environment" means: Development, Staging, Production
-  rephrase the below behavior
  - `ASPNETCORE_ENVIRONMENT`
  - `appsettings.{Environment}.json` override behaviors
- Debug vs Release builds (eg what is excluded from prod build)
- Environment-specific settings, such as pointing to a development data store instead of prod

## Module : Codebase Organization and Project Structure

- Single Responsibility Principle applied at the project level
- Choosing a project structure that promotes modularity and decoupling
- Internal vs external dependencies (project reference vs package reference)

## Module : Dependency Management

- Package managers
- Semantic versioning: what major/minor/patch imply
- What constitutes a breaking change
