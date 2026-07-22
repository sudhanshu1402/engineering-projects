# E-commerce (stub)

A tiny PHP script that defines a `Product` class and prints a hardcoded product list. It's a practice stub, not a real store.

## What it does

`index.php` declares a `Product` class with a name and price, builds an array of two products (a Laptop and a Mouse), then loops over them and echoes each one as an HTML line.

That's the whole program. There's no cart, no checkout, no database, no framework.

## Stack

Plain PHP. No Composer, no dependencies, no build step. The file even labels itself "Simple E-commerce Stub" in a comment.

## Run it

With the PHP CLI:

```bash
php index.php
```

Or serve it and open in a browser (the output uses `<br>` tags):

```bash
php -S localhost:8000
# then visit http://localhost:8000
```

## Output

```
Product: Laptop - $1000<br>
Product: Mouse - $20<br>
```

## Scope

This is a learning exercise sitting in a "hard" folder, but the code is beginner-level: one class, one constructor, one loop. If you're looking for an actual e-commerce implementation, this isn't it yet — it's the starting point where you'd add a cart, inventory, and persistence.
