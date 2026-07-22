# microservices-demo

A Maven multi-module skeleton for a Spring Boot microservices setup. Right now it's just the parent POM — the module sources aren't here yet.

## What's actually in this directory

One file: `pom.xml`. It's a parent aggregator POM (`packaging=pom`) that inherits from `spring-boot-starter-parent` 3.1.2 and declares three child modules:

- `discovery-service` — intended as a Eureka service registry
- `api-gateway` — intended as a Spring Cloud Gateway entry point
- `order-service` — intended as a domain service

None of those module directories exist in this folder. The POM points at them, but the code hasn't been written.

## Build status

`mvn clean install` will **fail** as-is. Maven tries to resolve the three declared modules and can't find them:

```
Child module .../discovery-service of .../pom.xml does not exist
```

To get a green build you'd need to either create the module directories (each with its own `pom.xml` and `src/`) or remove the `<modules>` block.

## Intended architecture

The plan the POM implies:

```
Client ── HTTP ──> API Gateway ──> Order Service
                        │
                        └── all services register with Eureka
```

Standard three-piece pattern: a discovery server, a gateway that routes to services, and at least one business service behind it.

## Scope note

This is a scaffold, not a working app. It's the parent POM stage of a microservices exercise — the module implementations are still to be built. Don't expect it to run.

## Stack (declared)

- Java / Spring Boot 3.1.2, Spring Cloud (implied by Eureka + Gateway)
- Maven multi-module build
