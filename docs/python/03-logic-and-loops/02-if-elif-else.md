---
title: Conditionals (if / elif / else) & Evaluation Order
sidebar_label: Conditionals (if / elif / else)
sidebar_position: 2
---

# Python Notes: Conditionals, Type Conversion & Evaluation Order

## Part 1: `if / else` Statements & Converting User Input (`int()`)

### 1. Course Module & Lesson Title
- **Module:** Module 2 — Control Flow & Logic (Building the Word-Scramble Game / Logic Foundations)
- **Lesson Topic:** `if / else` Statements & Converting User Input (`int()`)

### 2. Concept Breakdown
This lesson introduces binary branching logic using `if` and `else`, alongside dynamic terminal input handling:
- **Indentation-as-Syntax (Off-side rule):** Unlike JavaScript, which delimits blocks with curly braces `{}` and uses indentation purely for readability, Python uses whitespace indentation to define code scope. Standard Python style (PEP 8) mandates **4 spaces** per indentation level.
- **The Colon (`:`):** Every conditional block header (`if`, `elif`, `else`) ends with a colon `:`, which signals the start of an indented block.
- **Input Coercion:** `input()` always captures keyboard input as a string (`str`). Comparison operators like `>=` or `<` cannot compare strings to integers directly in Python without raising a `TypeError`. Wrapping `input()` in `int()` explicitly converts the numeric string into an integer.

### 3. JS vs. Python Mental Bridge

| Concept | JavaScript (ES6+) | Python 3 | Key Difference |
| :--- | :--- | :--- | :--- |
| **Block Delimiters** | `{ /* code block */ }` | Indentation (4 spaces) + `:` | Python has no curly braces for code blocks. |
| **Parentheses around Condition** | `if (score >= 60) { … }` | `if score >= 60:` | Parentheses are optional in Python; colons are required. |
| **Else Branching** | `else { … }` | `else:` | Block ends when indentation returns to parent level. |
| **String to Integer** | `parseInt(str, 10)` or `Number(str)` | `int(str)` | `int()` strictly parses whole numbers; throws `ValueError` on decimals. |
| **Logging / Printing** | `console.log("…")` | `print("…")` | `print()` automatically appends a newline `\n`. |
| **Comparison Operators** | `===`, `!==`, `>=`, `<=` | `==`, `!=`, `>=`, `<=` | Python uses standard `==` for value equality; there is no `===`. |

### 4. Code Walkthrough

```python
# 1. Takes user input as a string, then immediately casts it to an integer
student_score = int(input("What is your score? "))

# 2. Evaluates whether the integer is greater than or equal to 60
if student_score >= 60:
    # 4 spaces of indentation define this block as the 'if' body
    print("You passed!!!")
else:
    # Executes when the 'if' condition evaluates to False
    print("You didn't pass this time")
```
- `input("What is your score? ")`: Pauses execution, prints the prompt to the terminal, and waits for the user to press Enter. The returned value is of type `str` (e.g., `"75"`).
- `int(...)`: Converts `"75"` into `75`.
- `if student_score >= 60:`: Evaluates the expression. If `True`, the indented block runs; if `False`, execution jumps to the `else:` branch.

### 5. Common Pitfalls & Gotchas for JS Devs
- **Indentation Errors (`IndentationError`):** Mixing tabs and spaces, or using 2 spaces in one file and 4 in another, will crash the interpreter. Stick to 4 spaces everywhere.
- **Strict Typing on Comparisons (`TypeError`):**
  - JavaScript: `"75" >= 60` evaluates to `true` due to implicit coercion.
  - Python: `"75" >= 60` immediately crashes with `TypeError: '>=' not supported between instances of 'str' and 'int'`.
- **Float Parsing Crash (`ValueError`):**
  - In JS, `parseInt("60.5")` returns `60`.
  - In Python, `int("60.5")` raises a `ValueError: invalid literal for int() with base 10: '60.5'`. If a user might enter decimals, parse with `float()` first.
- **No Triple Equals (`===`):** Python does not have a `===` operator. Use `==` to check equality of values. The keyword `is` exists in Python, but it checks object identity (memory address, like pointer equality), not equality.

### 6. Edge Cases & Practical Patterns
- **Non-Numeric Strings / Decimals:** If the user inputs `"abc"` or `""`, `int()` raises `ValueError`. If the score includes decimals (e.g., `59.5`), use `float()`:
  ```python
  score = float(input("Enter score: "))

  if score >= 60.0:
      print("Passed")
  else:
      print("Failed")
  ```
- **Ternary Operator Comparison:**
  - JavaScript: `const status = score >= 60 ? "Pass" : "Fail";`

---

## Part 2: Multi-Branch Conditionals (`elif`) & Evaluation Order

### 1. Course Module & Lesson Title
- **Module:** Module 2 — Control Flow & Logic (Building the Word-Scramble Game / Decision Trees)
- **Lesson Topic:** Chaining Conditionals with `elif` & Short-Circuit Evaluation Order

### 2. Concept Breakdown
This lesson introduces multi-way branching using `if / elif / else` chains and highlights how evaluation order dictates code behavior:
- **The `elif` Keyword:** Python's contraction of `else if`. It allows checking multiple mutually exclusive conditions sequentially without deeply nested indentation.
- **Top-to-Bottom Short-Circuiting:** Python evaluates conditions from top to bottom. The moment one condition evaluates to `True`, Python runs that block and completely skips the rest of the chain.
- **Boundary Chaining Logic in the Challenge:**
  - `signal == 0` catches `0`.
  - `elif signal <= 2:` catches `1` and `2` (since `0` was already handled).
  - `elif signal <= 4:` catches `3` and `4` (since `0`, `1`, and `2` were already handled).
  - `else:` catches `5` (and anything above).

### 3. JS vs. Python Mental Bridge

| Concept | JavaScript (ES6+) | Python 3 | Key Difference |
| :--- | :--- | :--- | :--- |
| **Else If Syntax** | `else if (condition) { … }` | `elif condition:` | Python combines it into the single keyword `elif`. |
| **Chained Comparisons** | `signal >= 1 && signal <= 2` | `1 <= signal <= 2` | Python supports chained comparisons (e.g. `a < b < c`); JS does not. |
| **Strict vs Loose Equality** | `===` vs `==` | `==` | Python's `==` behaves like strict value equality without type coercion. |
| **Logical AND / OR** | `&&`, `\|\|` | `and`, `or` | Python uses plain English words, not symbols. |
| **Logical NOT** | `!condition` | `not condition` | Python uses `not` instead of the bang operator `!`. |

### 4. Code Walkthrough

#### Part A: The Commented Bug Walkthrough (Evaluation Trap)
```python
# test_score = 85
# if test_score >= 80:
#     print("A")
# elif test_score >= 90:
#     print("B")
```
- **Why it breaks:** If a student scores `95`, the interpreter tests `95 >= 80`. That is `True`. The interpreter prints `"A"`, terminates the conditional chain, and never checks `test_score >= 90`.
- **The rule:** When testing ranges, order conditions from **most restrictive to least restrictive** (e.g., `>= 90`, then `>= 80`, then `>= 70`).

#### Part B: The Solution Code
```python
# 1. Hardcoded signal strength test value
signal = 2  # out of 5 bars

# 2. Base case: explicitly check for zero bars
if signal == 0:
    print("50% off, sorry about the Wi-Fi!")

# 3. Catches 1 and 2 (0 has already been eliminated above)
elif signal <= 2:
    print("25% off")

# 4. Catches 3 and 4 (0, 1, and 2 have already been eliminated above)
elif signal <= 4:
    print("10% off")

# 5. Default fallback: catches 5 (and any value > 4)
else:
    print("Full bars, no discount today!")
```

### 5. Common Pitfalls & Gotchas for JS Devs
- **Using `else if` instead of `elif`:** Typing `else if condition:` triggers a `SyntaxError: invalid syntax` in Python.
- **Typing `&&` and `||`:** Writing `if signal >= 1 && signal <= 2:` will fail with a `SyntaxError`. In Python, you must write `if signal >= 1 and signal <= 2:` (or `if 1 <= signal <= 2:`).
- **Loose Equality Surprises Don't Exist:** In JS, `"" == false` or `0 == ""` evaluates to `true`. In Python, `"" == False` and `0 == ""` both evaluate to `False`. Python does not coerce types across equality checks.
- **Fallthrough / Switch statements:** JS has `switch (val) { case ... break; }`. Until Python 3.10, Python had no switch statement at all (relying purely on `if/elif/else`). Python 3.10 introduced `match/case` (pattern matching), which does not require `break` statements.

### 6. Edge Cases to Watch For
- **Negative Numbers:** If `signal = -1`, `signal <= 2` evaluates to `True`, triggering the `"25% off"` discount rather than an error.
- **Numbers Exceeding Max Bars:** If `signal = 10`, it falls through to the `else` branch and prints `"Full bars, no discount today!"`.
- **Boundary Validation:** In production code, guard with a range check: `if not (0 <= signal <= 5): print("Invalid signal")`.

### 7. Practical Patterns & Reusable Recipes

#### Pattern 1: Python Chained Comparison (Idiomatic Python)
```python
# JavaScript equivalent: if (signal >= 1 && signal <= 2)
if 1 <= signal <= 2:
    print("25% off")
elif 3 <= signal <= 4:
    print("10% off")
```

#### Pattern 2: Dictionary Dispatch (Alternative to Long `if/elif` Chains)
When mapping exact discrete values (like signal bars or status codes), Python developers often use dictionaries instead of long `elif` blocks:
```python
discounts = {
    0: "50% off, sorry about the Wi-Fi!",
    1: "25% off",
    2: "25% off",
    3: "10% off",
    4: "10% off",
    5: "Full bars, no discount today!"
}

signal = 2
message = discounts.get(signal, "Invalid signal value")
print(message)
```
  - Python: `status = "Pass" if score >= 60 else "Fail"`