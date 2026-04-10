# Controller Based Routing System for TCP Server

This repository contains a minimal TCP-based web server built in C# that implements a controller-style routing system.

The project demonstrates:

- A simple TCP server that accepts HTTP requests over a socket.
- A router for matching incoming requests to handler functions.
- Manual route registration with MapGet and MapPost.
- Automatic controller-based routing using reflection and custom HTTP method attributes.
- A lightweight application builder pattern inspired by ASP.NET Core.

## Features

- WebApplicationFactory.CreateBuilder() to create the application builder.
- uilder.Services.AddControllers() to discover controller classes.
- pp.MapControllers() to register controller actions automatically.
- pp.MapGet(...) for manual GET route registration.
- pp.MapPost(...) for manual POST route registration.
- A minimal Router and TcpServer to route requests and return text responses.

## How it works

1. WebApplicationFactory.CreateBuilder() creates a MiniWebApplicationBuilder.
2. uilder.Services.AddControllers() scans the assembly for classes ending with Controller.
3. uilder.Build() returns a MiniWebApplication with a router and service collection.
4. pp.MapControllers() inspects controller methods marked with HttpGet or HttpPost and maps them.
5. pp.RunAsync(port) starts the TCP server on the given port.

## Example

In Program.cs, the application is configured like this:

`csharp
var builder = WebApplicationFactory.CreateBuilder();
builder.Services.AddControllers();

var app = builder.Build();
app.MapControllers();
app.MapGet("/codecamp", (ctx) => $"We are codecamp batch 3. Response is generated from route: {ctx.Path}");

await app.RunAsync(5005);
`

A sample controller is defined in UserController.cs:

`csharp
[HttpGet("/user")]
public string GetUser()
{
    return "Fetching user from UserController";
}
`

## Running the project

1. Open the solution in Visual Studio or use the .NET CLI.
2. Run the application.
3. Connect to http://localhost:5005/codecamp or http://localhost:5005/user.

## Project structure

- Program.cs - application entry point and route registration.
- WebApplication.cs - builder and application classes.
- ServiceCollection.cs - discovers controller classes.
- Router.cs - stores and resolves route handlers.
- TcpServer.cs - listens for TCP connections and handles requests.
- UserController.cs - example controller with HTTP method attributes.
- HttpMethodAttribute.cs - defines HttpGet and HttpPost route metadata.
