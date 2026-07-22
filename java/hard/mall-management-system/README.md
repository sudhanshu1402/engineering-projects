# Mall Management System

A console-based Java program that simulates managing a shopping mall ("Palladium Mall") from three roles: admin, shop owner, and customer. It's a student project built around core Java: inheritance, abstract classes, `switch` menus, and reading data from flat `.txt` files.

## What it does

You launch the program and pick who you are:

1. **Admin** — logs in against `admin-up.txt`, then can view floor plans, shop details (`shop-details.txt`), and employee details (`emp-details.txt`).
2. **Shop Owner** — logs in against `shop-owner-up.txt`. The login returns which shop index (0–9) matched the credentials, and every menu after that is scoped to that shop: its employees (`emp-detailss1.txt` … `emp-detailss10.txt`), a hardcoded shop description, and its inventory (`inv-detailss1.txt` … `inv-detailss10.txt`).
3. **Customer** — no real login. Can list all shops (`shop-list.txt`), pick a floor plan, or read the mall description.

Every role reads records line-by-line from text files and prints them to the console. The whole thing loops: after each action it asks "Press 1 to Retry" and starts over.

The 10 shops are Nike, Pantaloons, Max, Adidas, Puma, Hypercity, Shoppers Stop, Brand Factory, Westside, and Hamleys.

## How it's structured

One source file, `final-test1.java`, with the `FinalTest1` main class plus a small class hierarchy:

- `person` (abstract) → `p1` — collects name/email/etc. and handles the admin and shop-owner logins. Returns an `int`: `1` for admin success, a `0–9` shop index for shop owners, `-1` on failure.
- `admin` (abstract) → `a11` — `floor_plan()`, `shop_mngmt()`, `emp_mngmt()`.
- `shopowner` (abstract) → `s1` — `employee_mngmt()`, `shopdet()`, `inventory()`, each keyed by the shop index.
- `customer` (abstract) → `c1` — `shop_list()`, `floor_plan()`, `mall_desc()`.

Login logic uses `String.compareTo` on lines pulled from the credential files. Shop-owner credentials are stored as alternating username/password lines (`shop1`, `pw1`, `shop2`, `pw2`, …).

## Data files

- `admin-up.txt` — admin username then password (`admin` / `a1`).
- `shop-owner-up.txt` — 10 username/password pairs.
- `shop-list.txt`, `shop-details.txt` — mall-wide catalog.
- `emp-detailss1..10.txt`, `inv-detailss1..10.txt` — per-shop employees and inventory, three fields per record (name/age/salary, or no/name/quantity).
- `1st-floor`, `2nd-floor`, `3rd-floor` (`.txt` / `.jpg`) — floor plan images. The floor-plan code reads these with `ImageIO.read` into a `BufferedImage` but never displays them; it just prints a confirmation line.

## Build & run

`.replit` compiles and runs it:

```bash
javac $(find . -name '*.java')
java FinalTest1
```

## Heads-up before it runs

The file paths are hardcoded to the original author's Windows machine, e.g.:

```java
File file = new File("C:\\Users\\HP\\Desktop\\project\\admin_up.txt");
```

Two things break outside that machine:

1. The absolute `C:\Users\HP\...` paths won't exist anywhere else.
2. The code expects **underscore** names (`admin_up.txt`, `emp_detailss1.txt`) but the files in this folder use **hyphens** (`admin-up.txt`, `emp-detailss1.txt`).

To run it locally you'd need to change the `new File(...)` paths to point at the hyphenated files in this directory (or rename the files). There are a lot of these string literals, one per case branch.

## Honest scope

This is a learning project, not production software. Credentials sit in plaintext, paths are hardcoded, add/remove menu options are stubbed (the `case 1:`/`case 2:` branches in shop and employee management are empty — only "show" works), and array sizes are fixed to exactly the sample data. It's a solid exercise in OOP structure and file I/O in plain Java, and it reads that way.
