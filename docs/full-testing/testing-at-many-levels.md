# Testing at Many Levels

## Where We've Been: Unit Tests

Up until now we have focused on creating small and fast unit tests that verify the behavior of a "unit of code". These units of code are usually just a single method (which may call a few helper methods).

We showed that it is possible to isolate the behavior of these small units by passing fake dependencies to the system under test. These fakes simple "dummy code" versions of what a real application would use, but still serve to satisfy the requirements of the system under test. Instead of fetching "real" data from a database, for example, we can pass in a small list of data that we have prepared in advance.

With unit testing, we do not focus on how the unit fits into the rest of the application. We simply verify that it works.

## What's Left to Test?

In this section we will briefly discuss integration and end-to-end testing. These tests ensure that the different pieces of the application work together as expected. They serve to protect against regressions, and provide confidence in the reliability of an application's critical paths.

If unit tests are the most "zoomed in" tests, integration zooms out one step to see how pieces of the application work together, and end-to-end tests zoom out even further to see how it works from the user or consumer's perspective.

| Test Type   | Scope                         | Goals                                                                     |
| ----------- | ----------------------------- | ------------------------------------------------------------------------- |
| Unit        | Single unit of code           | Verify the _behavior_ of a small granular piece of functionality          |
| Integration | Two or more units of code     | Verify the _interaction_ between two or more units of code                |
| End-to-end  | Large part of the application | Verify an entire user story, workflow, or critical path works as expected |
