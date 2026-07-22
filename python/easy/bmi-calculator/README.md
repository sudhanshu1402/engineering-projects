# BMI Calculator

A command-line script that computes Body Mass Index from height and weight, then labels the result.

## What it does

Prompts for height (cm) and weight (kg), calculates BMI with `weight / (height/100)**2`, and prints one of four categories based on the value:

| BMI | Category |
|-----|----------|
| ≤ 18.5 | underweight |
| ≤ 24.9 | healthy |
| ≤ 29.9 | overweight |
| > 29.9 | obese |

## Stack

Plain Python 3, standard library only. No dependencies.

## Run

```bash
python bmi_calculator.py
```

## Example

```
Enter height in cm: 175
Enter weight in kg: 70
Your Body Mass Index is 22.857142857142858
healthy
```

## Notes

- Practice exercise. No input validation — non-numeric input raises `ValueError`, and a height of 0 divides by zero.
- BMI prints unrounded.
- The `.replit` file's run command points at an old filename (`BMI Calculator.py`); the actual script is `bmi_calculator.py`.
