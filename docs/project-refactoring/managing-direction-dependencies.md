# Managing Direction of Dependencies

Aside from isolating functionality into logical independent units, modularity within an application can also help to enforce direction of dependencies.

... direction of dependencies ...

... current project looks like this. note that library reference represents core functionality that does not depend on any other projects.

![library modularity](../images/library-modularity.svg){ width="400" }

... suppose we wanted to add a mobile app as a second front-end option for our users. We could simply point it at the same library.

<!-- TODO: diagram showing public API of library, kind of like a class diagram? Is there one for this? May have to make custom -->

<!-- Dependencies Have Direction

A module that depends on another is a consuming module
The consumed module has no knowledge of its consumers
Core palette library vs. its frontends as the primary example

The Controlling Module

In a well-structured project, low-level modules don't need to know about each other
A higher-level controlling module consumes them and coordinates their behavior
Game libraries as the primary example

What Breaks When Direction Is Ignored

When a low-level module consumes a higher-level one, isolation breaks down
Physics importing from AI as a concrete example of what goes wrong
Brief mention that this pattern will appear in common real-world architectures (e.g. data access layers) even if not demonstrated here -->
