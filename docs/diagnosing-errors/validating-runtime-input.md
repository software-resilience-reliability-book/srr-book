# Validating Runtime Input

## Sources of External Data

It is rare to have an application that does not have some source of external data feeding into it.

This data may come from:

- Command line input
- Web forms or API requests
- Databases
- Parsed data files (CSV, XML, JSON, etc.)
- Configuration files
- Environment variables
- Command line arguments
- File paths or network resource locations

External data is a leading cause of runtime errors. Because values are not known in advance, the system must be programmed defensively to handle unexpected values.

All external inputs must be treated as untrusted data and potential points of failure.

<!-- prettier-ignore -->
!!! warning "Know your Secure Coding Practices!"
    In this book we do not cover the security aspects of handling external data. Our focus is on sanitizing and validating the data to ensure it is in a format that the application can process.

    Secure coding practices form a necessary part of a software developer's skillset, and should be studied in depth.

## Types of Input Validation

**Validation** checks whether the provided value is allowed according to the business rules that are in place and the data types that the application uses. The categories below provide some guidelines on what to look for in the context of user input. Be aware, though, that this input may come from any of the sources listed above.

| Category               | What to check                                                                  | Example                                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **Required**           | Are empty values allowed for the field?                                        | User leaves a required field blank.                                                                                       |
| **Type**               | Can the input be converted to the type your code expects?                      | User types `one` when a number is required.                                                                               |
| **Numeric shape**      | After parsing, is the value the right kind of number?                          | User enters `3.14` when only whole numbers are allowed, or `1.5` when an integer count is required.                       |
| **Range**              | Is the value within allowed business limits (min/max)?                         | User enters age `-99` or `500`.                                                                                           |
| **Overflow**           | Is the value too large or too small for the type or storage that will hold it? | User enters a 20-digit number that does not fit in a 32-bit integer, or a total that exceeds a database column's maximum. |
| **Format**             | Does the text follow the expected layout (separators, order, units)?           | User types `12/31/2025` when the app expects `2025-12-31`.                                                                |
| **Length**             | Does the input have the expected number of characters or items?                | User enters a 4-digit PIN with only 3 digits, or a username longer than the 50-character limit.                           |
| **Allowed characters** | Does the input use only characters your rules permit?                          | User types letters in a digits-only field, or includes spaces in a code that must be alphanumeric.                        |
| **Pattern**            | Does the input match a required structure (often a regex)?                     | User types `bob.example.com` when an email must contain `@` and a domain.                                                 |
