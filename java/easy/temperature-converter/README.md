# Temperature Converter

A small command-line Java program that converts a temperature between Celsius and Fahrenheit.

## What it does

Reads a number and a unit from standard input, then converts:

- `C` -> Fahrenheit, using `(temp * 9 / 5) + 32`
- `F` -> Celsius, using `(temp - 32) * 5 / 9`

Any other unit prints `Invalid unit selected.`

This is a beginner practice exercise (Scanner input, basic arithmetic, if/else). Nothing more to it.

## Stack

Plain Java, standard library only (`java.util.Scanner`). No build tool or dependencies.

## Build & run

```bash
javac TemperatureConverter.java
java TemperatureConverter
```

## Example

```
Enter temperature value: 100
Enter unit (C/F): C
100.0 C = 212.0 F
```

```
Enter temperature value: 32
Enter unit (C/F): F
32.0 F = 0.0 C
```

## Notes

- Input is read with `Scanner.nextDouble()`, so a non-numeric value throws an `InputMismatchException`. There's no input validation beyond the unit check.
- Only the first character of the unit is used, and it's uppercased, so `c`, `Celsius`, or `cold` all read as `C`.
- Output uses Java's default `double` formatting (e.g. `212.0`), not rounded.
