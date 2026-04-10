# TCP Server with Controller-Based Routing

This project is a small C# application that demonstrates a minimal web framework running over raw TCP.

It includes a custom router, a basic controller discovery system, and a TCP server that accepts HTTP-style requests.

## Project structure

- `Program.cs` - application entry point. Builds the app, registers controllers, and starts the server.
- `WebApplication.cs` - mini web framework implementation with route mapping and controller routing.
- `ServiceCollection.cs` - discovers controller classes by scanning the assembly.
- `Router.cs` - registers and resolves routes for incoming requests.
- `TcpServer.cs` - listens on a TCP port and parses simple HTTP requests.
- `Endpoint.cs` - represents a route endpoint with method, path, and handler.
- `HttpMethodAttribute.cs` - defines custom attributes for `HttpGet` and `HttpPost` on controller methods.
- `UserController.cs` - example controller with a simple endpoint.

## How it works

1. `Program.cs` creates the application builder.
2. Controllers are registered via `Services.AddControllers()`.
3. `MapControllers()` scans for methods decorated with `HttpGet` and `HttpPost`.
4. The router maps those methods as endpoints.
5. `TcpServer` listens for TCP connections on port `5005`.
6. Incoming requests are parsed and forwarded to the router.
7. Responses are returned over the TCP connection.

## Running the project

1. Open the solution in your C# IDE or use the .NET CLI.
2. Run the project.
3. The server listens on `localhost:5005`.

## Example request

Send a GET request to:

```
http://localhost:5005/codecamp
```

Or request the controller route:

```
http://localhost:5005/user
```

## Notes

- This project is a learning example and does not implement full HTTP parsing.
- It is designed to show how routing and controller discovery can work in a minimal framework.
