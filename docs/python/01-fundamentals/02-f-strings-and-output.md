---
title: f-Strings, String Multiplication, Comments & Workflow
sidebar_label: f-Strings, Output & Comments
sidebar_position: 2
---

# f-Strings

One of the most important concepts introduced in this lesson is the f-string.

Example:

```python
print(f"Hosted by: {host}")
```

## What Does the f Mean?

The f tells Python:

```text
Evaluate anything inside {}
and insert its value here.
```

## Example

Variable:

```python
host = "Scrimba"
```

Statement:

```python
print(f"Hosted by: {host}")
```

Output:

```text
Hosted by: Scrimba
```

Python replaces:

```text
{host}
```

with the value stored in:

```python
host
```

## JavaScript Comparison

Python:

```python
print(f"Hello {name}")
```

JavaScript:

```javascript
console.log(`Hello ${name}`);
```

The concept is essentially the same:
- Insert variable values into a string.
- Create dynamic output.

## Curly Braces in f-Strings

Whenever you see:

```text
{variable_name}
```

inside an f-string, Python will:
1. Look up the variable.
2. Retrieve its value.
3. Replace the placeholder.

Example:

```python
name = "PetriD"
print(f"Hello {name}")
```

Output:

```text
Hello PetriD

---

# String Multiplication

The invitation uses a line separator:

```python
print("=" * 40)
```

This is a new concept you haven't seen before.

## How It Works

Python can multiply strings.

Example:

```python
"=" * 5
```

Result:

```text
=====
```

So:

```python
"=" * 40
```

creates:

```text
========================================
```

This is often used when formatting terminal output.

---

# Running a Python Program

The instructor demonstrates running the file from the terminal.

Command:

```bash
python script.py
```

This tells Python:

```text
Execute the file named script.py
```

After execution, the program's output appears in the terminal.

## Re-running a Program

The instructor points out that after making changes:

```python
name = "Emily"
```

you can rerun the file to immediately see updated output.

This reinforces an important development cycle:

```text
Edit Code
↓
Save
↓
Run Program
↓
Check Output
↓
Repeat
```

You'll follow this process constantly as a developer.

---

# Comments

The lesson introduces comments.

Example:

```python
# Change the dress code to casual
```

## What Is a Comment?

A comment is text intended for humans rather than Python.
Python ignores comments completely.
Anything following:

```python
#
```

on a line is treated as a comment.

Example:

```python
# This is a comment
name = "Alice"
```

Python only executes:

```python
name = "Alice"
```

The comment is skipped.

## Why Comments Exist

Comments can be used to:
- Explain code
- Leave reminders
- Document decisions
- Think through a problem
- Create challenge instructions

Example:

```python
# Update the user's name
name = "PetriD"
```

---

# Challenge Review

You completed the challenge by changing:

```python
host = "Scrimba"
date = "October 26"
dress_code = "casual"
name = "PetriD"
```

and leaving the rest of the program unchanged.

This is a perfect example of separating:

### Data

```python
name
date
dress_code
```

from

### Program Structure

```python
print(…)
```

Only the data changed, but the output changed automatically.

---

# Mental Model

Think of variables like form fields.

```python
name = "PetriD"
```

is similar to filling out:

```text
Name: PetriD
```

Later, whenever the program needs the name, it checks that field and retrieves the current value.
If you change the field:

```python
name = "Alice"
```

every part of the program using `name` automatically sees the new value.

---

# Common Beginner Mistakes

## Forgetting Quotes Around Text

Incorrect:

```python
name = Alice
```

Python thinks `Alice` is another variable.

Correct:

```python
name = "Alice"
```

## Forgetting the f in an f-string

Incorrect:

```python
print("Hello {name}")
```

Output:

```text
Hello {name}
```

Correct:

```python
print(f"Hello {name}")
```

Output:

```text
Hello Alice
```

## Editing the Wrong Part

Instead of changing:

```python
name = "Alice"
```

a beginner might manually change all the output text.
The better approach is:

```python
name = "PetriD"
```

and let the program update itself.

---

# Key Terms

- **Variable:** A named container that stores a value.
- **String:** Text stored between quotation marks.
- **Assignment:** Storing a value inside a variable using `=`.
- **f-String:** A string prefixed with `f` that can insert variable values using `{}`.
- **`print()`:** A function that displays text or values in the terminal.
- **Comment:** A line beginning with `#` that Python ignores.
- **Terminal:** A command-line interface used to run programs.

---

# Key Takeaways

1. Variables store information that can be reused throughout a program.
2. Changing a variable changes every place that variable is used.
3. Strings are text values enclosed in quotes.
4. `print()` displays output in the terminal.
5. f-strings allow variables to be embedded directly into text.
6. Python can multiply strings using `*`.
7. Comments begin with `#` and are ignored by Python.
8. Separating data from logic makes programs easier to update and maintain.
9. The standard workflow is:
   - Edit code
   - Save
   - Run program
   - Check results
10. The invitation generator is your first example of a complete Python program using variables and dynamic output.
```