# Environment Types

In this section we will focus on the difference between a development environment and a production environment. You may hear of other environment types, such as staging or QA, but the main focus here is on configuring the development environment, since this is where developers spend most of their time.

## Development Environment

Developers need to be able to run and modify an application while working on it without affecting users of the live application. To accomplish this, developers recreate the application's environment locally. This is called a **development environment**.

A development environment might include:

### Local Database

A local database can be seeded with a subset of realistic data to allow developers to exercise the application's use cases without impacting the live database. A development environment should never point to a production database, to avoid accidentally modifying production data.

The database often runs on the developer's own machine, though in some cases, if there is a large amount of data, developers may use a shared development database.

Using a local database involves modifying connection strings to point to the local database instance, and sometimes using a different database provider entirely (for example, SQLite instead of SQL Server).

### Local File System

Much like the local database, any files the application needs to access can be placed on the local file system. Developers can then modify file-path settings to point to the local file system rather than the production file system.

### Local Web Server

Applications with a web component require a **dedicated web server** to host a production instance. This typically involves renting infrastructure from a cloud provider or self-hosting server hardware.

A **local web server** can be used during development. With the advent of lightweight web servers - such as [Kestrel](https://learn.microsoft.com/ga-ie/ASPNET/Core/fundamentals/servers/kestrel?view=aspnetcore-10.0) used in .NET Core web applications - it is now possible to run a web server on the developer's own machine.

To use a local web server, developers modify the application's configuration to point to a local web server address rather than the production web server.

## Production Environment

The **production environment** is the environment in which an application is deployed to end users. Software running in production typically has different needs than software running on a development machine. These may include:

- Support for a large number of concurrent users
- Storage and management of a greater quantity of data
- Stronger guarantees about availability and reliability (uptime, response times, etc.)
- Stronger security requirements (authentication, authorization, data protection, etc.)

Each of the components mentioned in the development environment section will differ in the production environment:

- The database is usually hosted on a dedicated server, may be of a different type than in development, and will almost always hold significantly more data.
- The file system usually points to a dedicated storage area, whether local to the production server or hosted in the cloud.
- The web server is usually hosted on a dedicated server.

All of the above may be configured, managed, or owned by the client, depending on the agreement between the client and the software vendor.
