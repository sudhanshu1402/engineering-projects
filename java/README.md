# Java Projects

> Part of my public learning archive. For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

Java code written during college and self-study, kept public for transparency. The projects range from a 20-line CLI converter to Android apps and a multi-module Spring Boot setup, so I've organized them by difficulty rather than pretending they're all the same weight.

## How it's organized

Four folders by difficulty. Each holds standalone project directories with their own README.

```
java/
├── easy/
├── medium/
├── hard/
└── expert/
```

## Projects

| Project | Level | What it is |
|---------|-------|------------|
| [01-hello-world](easy/01-hello-world) | Easy | Placeholder entry — README only, no code committed. |
| [temperature-converter](easy/temperature-converter) | Easy | ~20-line console app: reads a value and C/F unit from `Scanner`, converts and prints. |
| [online-quiz-system](medium/online-quiz-system) | Medium | JSP web quiz app (12 `.jsp` pages) with admin login, question flow, and scoring. Includes ER/class/architecture diagrams. |
| [scientific-calculator](medium/scientific-calculator) | Medium | Android app (Gradle). Single-`Activity` calculator with custom input parsing and layouts. |
| [mall-management-system](hard/mall-management-system) | Hard | 822-line console app using OOP inheritance (person → admin/shop-owner/customer) and flat-file text storage for employees, inventory, and shops. |
| [photo-manager](hard/photo-manager) | Hard | Android app (Gradle) for tagging and browsing photos. Uses `SQLite` (`MyDatabaseHelper`), a `ContentProvider`, fragments, and RecyclerView adapters. |
| [stock-trading-engine](expert/stock-trading-engine) | Expert | Toy market ticker: seeds a couple of stocks in a `HashMap` and prints random price ticks on a timed loop. Simulation, not a real matching engine. |
| [microservices-demo](expert/microservices-demo) | Expert | Multi-module Spring Boot 3 / Spring Cloud parent `pom.xml` declaring discovery, gateway, and order modules. Currently the parent POM and docs only — module sources aren't committed here. |

## Build & run

There's no single build for the whole folder — each project builds on its own.

- **Plain CLI Java** (`temperature-converter`, `mall-management-system`, `stock-trading-engine`): compile with `javac *.java`, then run the main class, e.g. `java TemperatureConverter`. The mall system reads and writes `.txt` files in its own directory.
- **Android** (`scientific-calculator`, `photo-manager`): open in Android Studio or run `./gradlew assembleDebug` from the project directory.
- **JSP** (`online-quiz-system`): deploy the `.jsp` files to a servlet container (Tomcat).
- **Spring Boot** (`microservices-demo`): `mvn clean install` from the project root once the module sources are present.

## Scope

These are learning and coursework projects. The console apps are small and use flat text files rather than databases; the "expert" folder holds a simulation and an architecture skeleton, not battle-tested systems. Honest about what each one is in its own README.
