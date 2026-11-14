---
title: Python Fundamentals Notes (Through a JavaScript Developer's Eyes)
sidebar_label: JS Dev Fundamentals & PayUp
sidebar_position: 4
---

# Python Fundamentals Notes (Through a JavaScript Developer's Eyes)

**Audience:** Experienced JavaScript/React/GraphQL developer learning Python.

These notes contain everything we've covered through the PayUp project, including course material, deeper explanations we discussed, JavaScript comparisons, and concepts the course did not explicitly explain.

---

## Section Overview

:::info

At this stage, you are not really learning programming.
You are learning:

```text
How Python expresses programming concepts I already know.
```

Most of the concepts so far are universal programming concepts:
- Variables
- Input
- Output
- Strings
- Data Types
- Type Conversion
- Basic Arithmetic
- String Formatting

The challenge is learning Python's syntax and conventions.

:::

---

## Variables

### What Is A Variable?

A variable is a named container that stores data.

Example:

```python
name = "Dimitri"
```

Think of a variable like a labeled storage box.

```text
name
┌─────────┐
│ Dimitri │
└─────────┘
```

Whenever Python sees:

```python
name
```

it retrieves:

```text
"Dimitri"
```

### Variable Assignment

Python uses `=` for assignment.

Example:

```python
age = 35
```

:::note

Read this as:
> Assign 35 to age.
> Not: age equals 35

:::

### JavaScript Comparison

:::info

JavaScript:

```javascript
const age = 35;
```

Python:

```python
age = 35
```

Differences:
- No `const`
- No `let`
- No `var`
- No semicolon

:::

### Variable Reassignment

Variables can be updated.

Example:

```python
score = 10
```

Later:

```python
score = 20
```

Now `score` contains `20`, not `10`. The previous value is replaced.

### Mental Model

:::info

Think of a whiteboard.
Initially:
```python
score = 10
```
Later: erase and replace with:
```python
score = 20
```

:::

---

## Data Types

Python stores different kinds of information using different types.

### String (`str`)

Text data.

Example:

```python
name = "Dimitri"
```

Checking the type:

```python
print(type(name))
```

JavaScript Comparison:

```javascript
typeof "Dimitri"
// Output: string
```

### Integer (`int`)

Whole numbers.

Example:

```python
age = 35
```

JavaScript Comparison:

```javascript
typeof 35
// Output: number
```

### Float (`float`)

Numbers with decimal values.

Example:

```python
price = 19.99
```

### Why Floats Exist

:::note

JavaScript hides this distinction.

JavaScript:

```javascript
typeof 35
// Output: number

typeof 35.5
// Output: number
```

Same type.

Python is more explicit: `35` is `int`, while `35.5` is `float`.

:::

### `None`

Python's equivalent of `null`.

Example:

```python
result = None
```

Meaning: No value.

Mental Model:
- JavaScript: `const result = null;`
- Python: `result = None`
- Both mean: Nothing here.

### Type Inspection

- Python: `type(value)`
- JavaScript: `typeof value`
- Purpose: Tell me what kind of data this is.

Examples:

```python
type("hello")
type(5)
type(5.5)
```

---

## Input

The course introduced `input()`.

### What It Does

Asks the user for information.

Example:

```python
name = input("Enter your name: ")
```

Terminal:

```text
Enter your name:
```

User enters: `Dimitri`
Stored value: `"Dimitri"`

### JavaScript Comparison

:::info

JavaScript:

```javascript
const name = prompt("Enter your name:");
```

Python:

```python
name = input("Enter your name: ")
```

:::

### Important Rule

:::warning

Input always returns a string.

Example:
User enters: `35`
Python stores: `"35"`, not `35`.
Type: `str`

:::

---

## Type Conversion

Because input returns strings, we often convert values.

### `int()`

Convert to integer.

Example:

```python
age = int(input("Age: "))
```

User enters: `35`
Stored value: `35`
Type: `int`

### `float()`

Convert to floating-point number.

Example:

```python
cost = float(input("Cost: "))
```

User enters: `19.99`
Stored value: `19.99`
Type: `float`

### JavaScript Comparison

:::info

JavaScript:
```javascript
Number(prompt())
// or
parseFloat(prompt())
```

Python:
```python
int()
float()
```

:::

---

## `print()` & f-Strings

### `print()`

Used to display information.

Example:

```python
print("Hello")
# Output: Hello
```

#### Blank Lines
```python
print()
```
Creates an empty line. Used for formatting.

### f-Strings

One of the most important Python features.

Example:

```python
name = "Dimitri"
print(f"Hello {name}")
# Output: Hello Dimitri
```

#### What The `f` Means

:::note

The `f` tells Python:
> Evaluate expressions inside `{}` and insert the result into the string.

:::

#### JavaScript Comparison

:::info

- JavaScript: ``console.log(`Hello ${name}`);``
- Python: `print(f"Hello {name}")`
- Same concept. Different syntax.

:::

#### Expressions Inside f-Strings
```python
a = 5
b = 10
print(f"{a + b}")
# Output: 15
```

Python evaluates the expression before printing.

### String Multiplication

Python allows:

```python
"=" * 5
# Output: =====

print("=" * 40)
# Output: ========================================
```

:::tip

Very useful for terminal formatting.

:::

---

## Percentage Calculations

This was introduced in the PayUp project.

### Service Charge Formula

```python
service_charge_total = cost * service_charge / 100
```

Suppose `cost = 100` and `service_charge = 20`:
- Calculation: `100 * 20 / 100`
- Step 1: `100 * 20` → Result: `2000`
- Step 2: `2000 / 100` → Result: `20`
- Meaning: 20% of $100 = $20

### General Formula

To compute `X% of Y`, use `Y * X / 100`:
- `85 * 18 / 100` → Result: `15.3`
- `50 * 10 / 100` → Result: `5`

### Order Of Operations (PEMDAS)

:::note

Python follows standard math rules:
1. Parentheses
2. Exponents
3. Multiplication/Division
4. Addition/Subtraction

Multiplication and division share equal priority. Python evaluates them left-to-right:

```python
100 * 20 / 100
# becomes 2000 / 100, then 20
```

:::

---

## Float Formatting

The PayUp project introduced `:.2f`.

Example:

```python
cost = 25
print(f"${cost:.2f}")
# Output: $25.00
```

### Understanding `:.2f`

Component breakdown:
- `:` — Begin formatting instructions.
- `.2` — Show 2 decimals.
- `f` — Display as floating-point number.

More Examples:

```python
value = 15.6789
print(f"{value:.2f}")
# Output: 15.68

value = 5
print(f"{value:.2f}")
# Output: 5.00
```

### JavaScript Comparison

:::info

- Python: `f"{value:.2f}"`
- JavaScript: `value.toFixed(2)`
  ```javascript
  (15.6789).toFixed(2)
  // Output: 15.68
  ```

:::

### Important Discovery

:::warning

Formatting creates a string:

```python
formatted = f"{15.6789:.2f}"
print(type(formatted))
```

Formatting is for display only. Not calculations.

:::

### `round()`

The course didn't explicitly cover this.

Example:

```python
round(15.6789, 2)
# Result: 15.68
```

Type remains `float`.

**Difference:**
- Display Formatting: `f"{value:.2f}"` → String output.
- Data Manipulation: `round(value, 2)` → Float value.

---

## Comments

Python comments begin with `#`:

```python
# This is a comment
```

Python ignores it.
Uses:
- Notes
- Instructions
- Documentation
- Reminders

---

## String Methods & Immutability

### `strip()`

Removes whitespace from both sides.

Example:

```python
name = "  Dimitri  "
print(name.strip())
# Output: Dimitri
```

JavaScript Comparison: `name.trim()`

### `lstrip()` & `rstrip()`

```python
# Removes whitespace on the left side
"  Dimitri  ".lstrip()
# Output: Dimitri (with right-side spaces preserved)

# Removes whitespace on the right side
"  Dimitri  ".rstrip() 
# Output: Dimitri (with left-side spaces preserved)
```

### `strip()` With Arguments

You can remove characters.

Example:

```python
"###hello###".strip("#")
# Output: hello
```

:::warning

**Important Rule:** Only removes characters from Beginning and End, not the middle:

```python
"##he#llo##".strip("#")
# Output: he#llo
```

:::

### `split()`

One of the most useful string methods.

:::info
Purpose: Break a **string** into pieces. Returns a list.
:::

Example:

```python
sentence = "hello world"
parts = sentence.split()
print(parts)
# Output: ['hello', 'world']
```

**JavaScript Comparison:**
- JavaScript: `"hello world".split(" ");`
- Python: `"hello world".split()`

**Custom Separator:**

```python
data = "apple,banana,orange"
print(data.split(","))
# Output: ['apple', 'banana', 'orange']
```

**Why `split()` Is Important:**
- Parsing user input
- Reading files
- Processing CSV data
- Building lists from text

### String Immutability

:::warning

**Strings do not change:**

```python
name = "  Dimitri  "
name.strip()
```

does not change `name`. 

**You must do:**

```python
name = name.strip()
```

to save the new value. 

:::

:::info
**Why?** 

Methods return new strings. The original string remains untouched.
:::

---

## JavaScript To Python Translation Guide

| JavaScript | Python |
| :--- | :--- |
| `console.log()` | `print()` |
| `prompt()` | `input()` |
| `typeof` | `type()` |
| `null` | `None` |
| `Number()` | `int()` / `float()` |
| `${name}` | `{name}` in f-string |
| `template literal` | `f-string` |
| `trim()` | `strip()` |
| `toFixed(2)` | `:.2f` |
| `"a".repeat(5)` | `"a" * 5` |
| `split()` | `split()` |

### Developer Perspective

:::tip

At this point, Python should feel familiar. You are not learning Programming—you are learning Python vocabulary.
The major new ideas later in the course will likely be:
- Lists
- Tuples
- Dictionaries
- Functions
- Error Handling
- Modules
- JSON
- File Handling
- FastAPI
- CrewAI (outside the course)

That's where Python starts feeling like its own language rather than a different syntax for concepts you already know from JavaScript. 🐍🚀
Variables do not remember old values.

:::
````