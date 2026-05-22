# Why Testing?

It may seem as if tests only exist to help us catch errors in the code, but they serve a broad set of purposes.

## Behavior Verification

Software is built to meet requirements and specifications. Tests can be used to verify that an application meets expectations prior to release.

This may be more or less formal. Some development teams use methodologies that tightly integrate tests into acceptance criteria for a release. Even if this is not the case, developers still use tests to verify that the code meets internal expectations - that the code is doing its job as expected. Tests are proof that the code works.

## Documentation

Tests serve as living documentation of the expected behavior of the code. Reading a suite of tests tells us exactly what is expected from the part of the application that is under test.

## Regression Detection

A **regression** is a change in the behavior of the application that is not intended. In a fragile codebase, changing one thing may cause another thing to break. Tests help to verify that parts of the application that work today will continue to work whenever code is modified.

## Codebase Organization

The ease with which tests can be written and maintained can serve as a signal of the quality of the codebase. When a codebase is difficult to test, it is often a signal that the code is due to be refactored. Tests help developers work in small, manageable increments to design a **modular** and **decoupled** codebase.
