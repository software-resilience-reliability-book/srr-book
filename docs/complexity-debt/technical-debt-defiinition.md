# What is Technical Debt?

We previously defined **technical debt** as the future costs associated with relying on shortcuts or suboptimal decisions made during software development.

The idea aligns with the proverb "An ounce of prevention is worth a pound of cure": adopting best practices early in the development process can prevent the need for costly fixes later.

![technical debt impact on delivery](../images/tech-debt-impact-on-delivery.svg){ width="600" class="center" }

Let's take a look at the image above.

On the x-axis is "time": the left side is early in the development process, the right side is late in the development process.

On the y-axis is "features delivered": early in the project there are no features. They are added over time.

The two curves represent two different projects:

_Poor Technical Debt Management_

The project in red does not manage technical debt well. This curve roughly has a **logarithmic** shape as the project progresses.

It may seem like quick progress early indicates that the project is off to a good start, but the reality is that the project is likely to fall behind later. It may even reach a point where nothing can be changed without breaking the system, and the project is effectively dead.

_Well-Managed Technical Debt_

The project in blue follows good practices for managing technical debt. This curve roughly has an **exponential** shape as the project progresses.
