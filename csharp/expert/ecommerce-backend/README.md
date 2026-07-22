# Ecommerce Backend

A minimal ASP.NET Core startup scaffold in C#. This is a stub, not a working store.

## What's actually here

One file: `startup.cs`. It defines an ASP.NET Core `Startup` class that:

- registers MVC controllers (`services.AddControllers()`)
- enables the developer exception page in development
- wires up routing and maps controller endpoints

That's the whole thing. There are no controllers, no models, no data layer, no cart, no orders, no payments — despite the "ecommerce" name. It's the empty frame you'd start from before building any of that.

## Stack

- C# / .NET (ASP.NET Core)
- Microsoft.AspNetCore.* namespaces (Builder, Hosting, DependencyInjection)

Note: there's no `.csproj` in this directory, so the project won't compile as-is. You'd need a project file (and a `Program`/host entry point calling `UseStartup<Startup>()`) to actually run it.

## Run

`.replit` and the README point at:

```
dotnet run
```

For that to work you'd first have to add a `.csproj` and a host bootstrap. As it stands, `dotnet run` has nothing to build.

## Scope

Practice piece filed under `csharp/expert`. The routing/controller wiring in `Startup.Configure` is real ASP.NET Core boilerplate, but the "expert" and "ecommerce" labels are aspirational — there's no domain logic behind them yet.
