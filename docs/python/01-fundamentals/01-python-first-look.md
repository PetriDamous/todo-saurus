---
title: Python First Look
sidebar_label: Python First Look
sidebar_position: 1
---

# Python Fundamentals

# Python: First Look

## Lesson Overview

This lesson serves as your first real exposure to reading and modifying a Python program. Instead of starting with theory, the instructor presents a working application: a simple invitation generator that prints a formatted invitation to the terminal. The goal is to become comfortable identifying pieces of Python code and understanding how changing data affects program output. [[scrimba.com]](https://scrimba.com/learn-python-c03/~07fk)

The major concepts introduced are:

- Variables
- Strings
- The `print()` function
- Running Python files
- f-strings
- Comments
- Separating data from program logic [[scrimba.com]](https://scrimba.com/learn-python-c03/~07fk)

---

# The Invitation Generator

The lesson begins with a complete Python program:

```python
host = "Scrimba"

date = "April 20"

dress_code = "Black tie"

name = "Alice"

print("=" * 40)

print()

print(f" {name}, you are cordially invited to:")

print()

print(" LEARN PYTHON")

print()

print(f" Hosted by: {host}")

print(f" Date: {date}")

print(f" Dress code: {dress_code}")

print()

print("=" * 40)
```


---

# Variables

## What Is a Variable?

A variable is a named container that stores a value.

Example:

```python
name = "Alice"
```

Here:

- `name` is the variable name.
- `"Alice"` is the value stored in the variable.

Think of variables as labels attached to pieces of information.

Instead of remembering:

```text
"Alice"
```

everywhere in your program, you can simply write:

```python
name
```

and Python will use the stored value.

---

## Why Variables Matter

Variables allow you to separate:

### Data

Information that changes:

```python
name = "Alice"

date = "April 20"

dress_code = "Black tie"
```

from

### Program Logic

The code that performs work:

```python
print(f"Date: {date}")
```

This is one of the most important ideas in all programming.

Instead of rewriting program logic every time data changes, you simply update the variables.

---

## Example

Original:

```python
name = "Alice"
```

Output:

```text
Alice, you are cordially invited to:
```

Change it to:

```python
name = "Emily"
```

Output:

```text
Emily, you are cordially invited to:
```

The rest of the program remains unchanged.

---

# Variable Assignment

Variables are created using the assignment operator:

```python
=
```

Example:

```python
host = "Scrimba"
```

Read this as:

Assign the value "Scrimba" to the variable host

Not:

host equals Scrimba

In programming, `=` generally means "assign" rather than mathematical equality.

---

# Python vs JavaScript

### JavaScript

```javascript
const name = "Alice";
```

### Python

```python
name = "Alice"
```

Notice what Python removes:

- No `const`
- No `let`
- No `var`
- No semicolon

The variable is created automatically when assigned a value.

---

# Strings

## What Is a String?

A string is text surrounded by quotes.

Examples:

```text
"Alice"

"Black tie"

"Scrimba"
```

These are all strings.

In this lesson, every variable stores a string value.

```python
host = "Scrimba"

date = "April 20"

dress_code = "Black tie"

name = "Alice"
```

---

# The print() Function

## Purpose

The `print()` function displays information in the terminal.

Example:

```python
print("Hello")
```

Output:

```text
Hello
```

---

## Printing Variables

Instead of printing raw text, you can print values stored in variables.

Example:

```python
name = "Alice"

print(name)
```

Output:

```text
Alice
```

Python retrieves the value stored in the variable and prints it.

---

# Empty print() Statements

You may have noticed lines like:

```python
print()
```

No arguments are supplied.

This creates a blank line.

Example:

```python
print("Line 1")

print()

print("Line 2")
```

Output:

```text
Line 1

Line 2
```

This is commonly used for formatting console output.
The program uses information stored in variables and combines that information with printed text to produce a formatted invitation.