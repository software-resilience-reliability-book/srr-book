# Creating a .NET Project

## Open the Integrated Terminal

From here forward we will assume that you are working from within the Visual Studio Code IDE.

![integrated terminal in Visual Studio Code](../images/integrated-terminal.png)

You can run commands on the **integrated terminal** in Visual Studio Code, which is usually located at the bottom of the screen. If you lose visibility of the terminal, you can open it through the **View** menu.

<!-- prettier-ignore -->
!!! info "Removing Visual Clutter"
    We recommend hiding any "chat" and "agent" AI panes so that you can focus on the code. These additional panes can be distracting when you are learning new concepts.

    Once you can work fluently within the IDE, you can toggle the visibility of these panes as needed. The AI is a great tool to help you understand provided code examples. Early in your career it should be used sparingly to write code.

## Run the `dotnet new` Command

The `dotnet new` command creates a new project in the current directory. We will use the `console` template to create a new console application project.

```bash
dotnet new console
```

This will create several files in the current directory. Open the `Program.cs` file and you will see a basic "Hello, World!" program.

This is currently the only **source code** in the project. Our next step is to turn this code into something that the computer can execute.
