# Chat App

A minimal TCP server stub in C#. Practice piece for the System.Net.Sockets API.

## What it actually does

Opens a `TcpListener` bound to `0.0.0.0:8888`, starts listening, and prints a startup line:

```
Chat Server Started...
```

That's the whole program. It does not accept connections, read messages, or relay anything between clients yet — despite the name. The listener is started and the process then exits. Treat this as the first few lines of a chat server, not a working one.

## Stack

- C# on .NET (`dotnet` CLI)
- `System.Net.Sockets.TcpListener` / `IPAddress`

No `.csproj` is checked in here; `dotnet run` resolves the project from the source in this directory.

## Run

```bash
dotnet run
```

Prints the startup message and returns. (On Replit the `.replit` file wires `run = "dotnet run"` to the Run button.)

## The code

```csharp
TcpListener server = new TcpListener(IPAddress.Any, 8888);
server.Start();
Console.WriteLine("Chat Server Started...");
```

## Scope

Learning exercise, not a finished app. To make it a real chat server you'd add an accept loop (`server.AcceptTcpClient()`), per-client read/write handling (likely on separate threads or async tasks), and message broadcast to connected clients.
