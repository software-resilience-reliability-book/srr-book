# Choosing Module Boundaries

Sometimes module boundares are created to isolate related cohesive functionality that should be treated as a single unit. A project may have several libraries, each responsible for a different aspect of the application.

Imagine a simple computer game where the user simply moves a character around the screen. The user may have a following companion, or be chased by an antagonist. This application may have separate libraries for:

| Library            | Description                                    |
| ------------------ | ---------------------------------------------- |
| Input              | Processes keyboard, mouse, or controller input |
| Physics            | Handles movement, collisions, and gravity      |
| AI                 | Controls non-player character (NPC) behaviors  |
| Audio              | Manages sound effects and music                |
| Rendering          | Draws graphics and UI to the screen            |
| Save-Configuration | Handles saving/loading user and game settings  |

Each of these libraries focuses on one aspect of the application.

The Input library has no reason to know about the Physics library. Input is concerned with mapping user actions to intent: "pressing the right arrow key should move the character right." Physics is concerned with resolving positional movement rules in the world: "a character colliding with a wall should stop." Neither needs to know about AI, which governs NPC behavior: "a companion should stay behind the player at some distance X", or Audio, which responds to game events: "a collision with a wall should trigger a thud sound".

The set of overall functionality that any of these modules exposes in its API is likely to be only a small subset of the overall functionality of the module. There may be great complexity inside of the Save-Configuration library, but it may expose only a single class in its public API.

The main consideration when deciding whether to extract functionality into its own module is the _degree of communication across module boundaries_.

These libraries do not directly talk to each other much, if at all. Coordination between them is typically handled by a separate controlling module.
