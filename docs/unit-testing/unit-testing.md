# Unit Testing

## Scope of Unit Testing

Before we can write a unit test, we need to come to an understanding of what a "unit' is.

According to Vladimir Khorikov in _Unit Testing: Principles, Practices, and Patterns_, a **unit test** should test a "single, atomic fact about a unit of behavior".

In practice many developers define a unit as a single class or method. This approach is often useful, but it is not a necessary assumption. Forcing tests to follow this structure can lead to tests that are too granular (testing so many fine details that the tests are no longer a useful summary of the behavior) or too coarse (not testing enough detail so that valuable behavior is missed in testing).

For example, private methods that are not part of the public API of a class often do not need to be tested. Their behavior is tested implicity by testing public methods that call them.

## What to Test

**_Unit tests should focus on the expected behavior of the application - not the implementation details._**

Tests should approach behavior from the standpoint of the **consumer** of the code. When we discuss other types of tests later in the book, this consumer will be the user. With unit tests, the consumer is typically other parts of the application.

Our code contains behavior that is both internal (necessary for the unit to function) and external (visible to other parts of the application). Unit tests should only focus on the external behavior, not the internal implementation details.

As an example: when you approach a drivethrough window to pick up a sandwich that you have ordered, it should not matter to you whether the sandwich was prepared on a wooden table with four legs, or a steel counter attached to the wall. These are internal concerns. What matters is that you asked for a sandwich and received the correct order.
