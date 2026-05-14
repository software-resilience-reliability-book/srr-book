# Reliabile Software

Healthy software is **reliable**. It runs as expected without failure. Given the complexity of most software systems, it is amazing that they are able to operate without significant issues, but this doesn't come without discipline and careful attention to detail.

Software is an **asset**. It provides meaningful value to its owners and users.

The code that makes up the software is a **liability**. Developers and maintainers must ensure that it continues to work. Every time the system changes, the code must be modified to support the new requirements. Additional functionality introduces points of failure to the system.

To revisit the quote from the start of this book:

> ...one of the most critical indicators of a software application’s health is how easily, safely, and quickly it can be modified.

This book isn't meant to cover all of the practices that a software developer might take to ensure reliable software, but we will examine how to write and structure code in ways that keep it robust.

We will examine common failure modes, and look at how to prevent them. Because most failures happen when the codebase is changed, we will learn how to ensure that future changes don't break existing functionality.
