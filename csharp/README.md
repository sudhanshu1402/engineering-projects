# C# Projects

> Part of my public learning archive. For active, production-grade work see the pinned repos on my [GitHub profile](https://github.com/sudhanshu1402).

C# and .NET code from college and early self-study. These are small practice exercises, mostly console apps, kept public for transparency about how I started. Several of the harder ones are deliberate stubs — the entry point and structure are there, the full logic isn't. I've marked those honestly below.

## How it's organized

Projects are grouped into four folders by difficulty. Each project sits in its own folder with a `program.cs` (or `.xaml` for the WPF one) and a short README.

```
csharp/
├── easy/     hello world, calculator, number guessing
├── medium/   expense tracker, WPF to-do list
├── hard/     TCP chat server, inventory system
└── expert/   stock simulator, ASP.NET ecommerce backend
```

## Projects

### easy
| Project | What it is | State |
|---|---|---|
| `01-hello-world` | Placeholder folder, README only | Empty |
| `console-calculator` | Reads two numbers, prints sum and difference | Working |
| `number-guess` | Guess a random 1–100 number, higher/lower hints in a loop | Working |

### medium
| Project | What it is | State |
|---|---|---|
| `expense-tracker` | Console menu: add expenses to a `List<decimal>`, view running total | Working |
| `to-do-list-wpf` | WPF window (XAML) with a text box, add button, and task list | UI markup only, no code-behind |

### hard
| Project | What it is | State |
|---|---|---|
| `chat-app` | Starts a `TcpListener` on port 8888 | Stub — listens but doesn't accept clients |
| `inventory-system` | Defines an `Item` class and an inventory list | Stub — prints an init message, no CRUD |

### expert
| Project | What it is | State |
|---|---|---|
| `stock-simulator` | Console entry point for a market simulator | Stub — no simulation logic |
| `ecommerce-backend` | ASP.NET Core `Startup` wiring controllers and routing | Stub — startup config only, no controllers |

## Running the console apps

Each console project has its own folder. From inside one:

```bash
cd easy/number-guess
dotnet run
```

Requires the [.NET SDK](https://dotnet.microsoft.com/download). The `.replit` files in most folders let them run on Replit as well.

`console-calculator`, `number-guess`, and `expense-tracker` actually do something end to end. Example run of number-guess:

```
Guess a number between 1 and 100
Guess: 50
Lower
Guess: 25
Higher
Guess: 37
You Win!
```

The WPF project (`to-do-list-wpf`) needs Windows and Visual Studio to build, and only the XAML layout exists — there's no `AddTask_Click` handler behind the button yet.

## Scope

These are learning exercises, not libraries or products. The easy and medium console apps run; the hard and expert ones are scaffolds I set up and didn't finish. Kept as-is to show the progression rather than dressed up after the fact.
