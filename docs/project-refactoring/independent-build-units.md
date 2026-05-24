# Creating Independent Build Units

## Modular Builds

Extracting functionality into modules gives us the ability to build our application in a modular way. Each module can be built independently of the others. For small projects, this may not be a significant benefit. But for larger projects, it can be a significant improvement in build times and deployment flexibility.

To take an example from the game libraries shown previously: suppose we want the character to jump higher when the space button is pressed. This change belongs in the Physics library. The Physics library is responsible for resolving positional movement rules in the world; this includes gravity, jumping, and other movement behaviors.

Real physics libraries are much more complex, but our library might have a `Character` class with a `Jump` method. We might go into the `Jump` method and modify the `MAX_JUMP_HEIGHT` constant.

In this case, only the Physics module changed, so we only need to:

1. Rebuild the Physics module (and any other modules that depend on it)
2. Reversion the module to indicate that it has changed
3. Redeploy the application if we want this change to go live

It works much like replacing a headlight on a car. We only need to replace the bulb, along with anything "using" the bulb, such as the headlight assembly.

## Single Responsibility Principle for Modules

A significant point of this example is what we do not need to do: modify or rebuild the Input module. The implementation details related to "pressing the space button should cause a jump event" did not change at all. Only the movement rules of the character's jump.

This aligns with the Single Responsibility Principle.

- The Input module has one reason to change: if the input to event mappings change.
- The Physics module has one reason to change: if the movement rules change.
