# Managing Complexity

Arguably, the most difficult part of building software is **managing complexity**. For a given software problem there may be hundreds of ways to implement a solution. Dozens of these may be practical and effective. How do we know which to choose?

## Design Tradeoffs

In the world of software, there is no "best" solution. Each solution will involve **tradeoffs**. By understanding what is most important to our clients and the consumers of our software, we can adjust the development approaches that we take and get as close as possible.

As an example, when you were first learning to program you probably wrote mostly **procedural** code, with all of your code in one file.

You may later have learned some **object oriented programming (OOP)**, where code is grouped into classes, usually with one file per class. OOP is not inherently better than procedural programming. It offers a tradeoff. There is a reason that small scripts are procedural whereas larger full scale applications tend to be object oriented:

_Procedural_

- Quick initial development
- Code "reads" sequentially so can be easier to understand
- Difficult to maintain in large project
- Poor modularity and code reuse

_Object Oriented_

- Requires planning up front
- Scattered files and extra "boilerplate code" can make it difficult ot understand
- Isolated functionality makes maintence easy in large projects
- Excellent modularity and code reuse

<!-- prettier-ignore -->
!!! info "Right Tool for the Job"
    With the broad range of available options, simply choosing an appropriate technology can be a daunting task. It may be tempting to stick with a technology because you're familiar with it or because it's currently trendy. Some up front research into the pros and cons of each technology can help you make a more informed decision.

    If all you need to do is read a CSV file and create a graph image from the contents, a procedural script written in a language like Python is a good choice.

    If you need a full web application with complex user interactions and domain logic, object oriented programming written in a language like C# is a good choice.
