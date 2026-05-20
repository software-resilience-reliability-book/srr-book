# Testing an Application

## Why Testing?

Earlier in this book we looked at the impact of technical debt on the development process. When an application accumulates technical debt changes become more difficult to make, and the application becomes fragile.

It may seem as if tests only exist to help us catch errors in the code, but they serve a broad set of purposes.

## Regression Detection

A **regression** is a change in the behavior of the application that is not intended. In a fragile codebase, changing one thing may cause another thing to break. Tests help to verify that parts of the application that work today will continue to work whenever code is modified.

## Documentation

Tests serve as living documentation of the expected behavior of the code. Reading a suite of tests tells us exactly what is expected from the part of the application that is under test.

## Requirements Verification

Software is built to meet requirements and specifications. Tests can be used to verify that an application meets expectations prior to release.

## Codebase Organization

The ease with which tests can be written and maintained can serve as a signal of the quality of the codebase. When a codebase is difficult to test, it is often a signal that the code is due to be refactored. Tests help developers work in small, manageable increments to design a **modular** and **decoupled** codebase.
