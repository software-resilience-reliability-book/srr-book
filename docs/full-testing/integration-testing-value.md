# Value of the Integration Tests

The test that we walked through confirmed that all of the components involved in the test worked together to produce the expected HTML value. If any component along the way had failed, the final assertion would have failed.

It is very possible to have working unit tests for each component, but to find that the system does not work as intended once these components are integrated. Imagine if we changed the method signature on one of the functions in the color library, or decided to throw a new type of exception.

Integration testing tests communication and coordination between components. It makes sure that the contracts between a unit and its consumers, those parts of the system that interface with it, remain unbroken.
