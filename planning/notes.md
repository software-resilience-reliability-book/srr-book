# Content Planning

mkdocs preview command:

```
mkdocs serve --livereload
```

## Format

Book is compiled with mkdocs.

## Examples from full color transformation library solution

Tast harnessing: Program.cs as means to step into HexConverter
Test naming conventions: all of the tests
Isolating test functionality / mocks: PaletteTransformerTest (see the mock)
Protecting invariants / guard clauses: Constructor for RgbColor ensures we can assume a valid color after construction
Dependency injection (if we get to this): PaletteTransformer

## TODO

Make the icons in the asides consistent.

Make chapter pages look like chapter pages.

Nice to have: a map of how each project in the final solution references to each other

- src/library
- src/api or web or whatever consumer
- tests/harness
- tests/tests

## Chapters

These do not need to be (and should not be) a one to one mapping with the course modules.

They should be granular, so that pagination works well and it reads like a text.
