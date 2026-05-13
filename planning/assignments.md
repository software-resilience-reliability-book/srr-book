# Tentative Assignment List

**Incomplete: should have one per module; needs mapped to module numbers**

All assignments are refactoring and testing assignments formed around a "text parsing and transformation" library.

Assignments parallel examples provided in the text.

To make instructor grading feasible and objective, all assignments must have rubrics. Rubrics must have granular scoring categories (x points for "contains few to no errors", X points for "contains some errors", X points for "contains significant errors", 0 pts for "incomplete or does not demonstrate fundamental understanding". Rubric structure across assignments should be as cohesive as possible; always have points for general stuff like submission and code quality, then have specific points for assignment's refactor or testing.

---

## Assignment X: Troubleshoot and Stabilize

**Starter:** Word-counter console app with one or more failing builds and runtime bugs.

**Student work:** Diagnose and fix all issues. Submit a short written diagnosis alongside the corrected code.

**Primary objectives:** Refactoring fundamentals, error diagnosis.

---

## Assignment X: Unit Testing an Existing Codebase

**Starter:** Working parser with a scaffolded but empty test project. Includes one fully-written example test as a reference pattern.

**Student work:** Implement tests for a specified list of 6–8 behaviors. One or two listed behaviors are currently incorrect in the code, surfacing regression detection organically.

**Primary objectives:** Unit testing, test harnesses, automated testing procedures.

---

## Assignment X: Externalized Configuration

**Starter:** Parser with hardcoded values and a provided options class. Tests exist and must continue to pass.

**Student work:** Move three or four specified hardcoded values into `appsettings.json`, bind them through the provided options class, and add an `appsettings.Development.json` that overrides one value.

**Primary objectives:** Externalized configuration, environment-specific configuration files.

---

## Assignment X: Refactoring Toward Modularity

**Starter:** Single-project parser with code sections clearly marked by header comments (IO, parsing, output). Tests exist and must continue to pass.

**Student work:** Extract one marked section into a separate class library project per instructor-provided target structure. Update references and verify tests still pass.

**Primary objectives:** Refactoring, codebase organization, modularity, tests as a safety net for change.

---

## Assignment X: Dependency Management

**Starter:** Multi-project parser with a marked section of hand-rolled code to be replaced.

**Student work:** Add a specified NuGet package, use it to replace the marked section, and answer short written questions about the installed version, its dependencies, and semantic versioning expectations for a hypothetical major-version release.

**Primary objectives:** Package management, semantic versioning.

---

## Assignment X: Integration Testing

**Starter:** Parser with a rule-fetching component and existing unit tests.

**Student work:** Write two or three integration tests against a provided local file source, including at least one failure-mode test (e.g., missing file). Submit a brief written reflection on how development and production configurations would differ for this codebase.

**Primary objectives:** Integration testing, test type tradeoffs, environment-aware deployment (in reflection form).

---
