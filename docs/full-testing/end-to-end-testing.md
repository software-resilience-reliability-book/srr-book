# End-to-End Testing

## What is End-to-End Testing?

**End-to-end testing** is the process of testing the entire application from start to finish. Rather than focusing on an isolated use case. It is often used to test an entire **user journey** - a full sequence of actions that a user takes to achieve a goal.

## End-to-End Testing by Example

The end-to-end test that we will look at is very similar to the integration test that we just ran. The main difference is that it has a larger scope, and starts with the "user".

Rather than using a "bot" to make HTTP requests...

## Reviewing the Value of the Test

The main benefit of end-to-end testing is that it provides the most confidence that the application works as intended. Both unit and integration tests can pass, but only an end-to-end test automates a real-world scenario in full.

The downside of end-to-end testing is that it is often the most time and resource intensive test type to run. This has been greatly alleviated in recent years through elegant testing frameworks, tools like headless browsers, and containers that can quickly spin up a full environment, even with a realistic test data set.
