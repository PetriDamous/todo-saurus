---
title: Function Return Values
sidebar_label: Function Return Values
sidebar_position: 3
---

# Python Notes: Function `return` Values, `None` vs. `print()`, & the `math` Module

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 3 — Functions & Data Structures (Building the Dice Fight Game / Data Pipelines)
- **Lesson Topic:** Returning Values from Functions (`return`), `print()` vs. `return`, Implicit `None`, & `math.ceil()`
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~05zh](https://scrimba.com/learn-python-c03/~05zh)

:::

---

## 2. Concept Breakdown

:::note

This lesson shifts functions from terminal-printing side-effect routines into composable **data-producing functions** using `return`:

- **`print()` vs. `return`:**
  - `print()` sends text to standard output (the terminal) for a human to read. It does **not** pass data back to your Python program.
  - `return` immediately exits the current function and sends a value back to the exact spot where the function was called, allowing you to store it in a variable, perform further math on it, or pass it directly as an argument into another function.
- **Implicit `None` Return:** In Python, every function returns a value. If a function finishes executing without hitting a `return` statement—or hits a bare `return` with no expression—Python implicitly returns `None` (analogous to `undefined` in JavaScript).
- **Function Composition & Pipelines:** Returning values lets you chain functions together cleanly: `slices = slices_needed(10)` feeds directly into `pizzas = pizzas_needed(slices)` (or nested as `pizzas_needed(slices_needed(10))`).
- **The Built-in `math` Module (`math.ceil()`):** Python's standard library includes the `math` module for mathematical operations. `math.ceil(x)` rounds a number **up** to the nearest whole integer (ceiling).

:::

---

## 3. JS vs. Python Mental Bridge

:::info

### Returning Values & Default Empty Return

```javascript
// JavaScript (ES6+)
function slicesNeeded(guests) {
  return guests * 2;
}

function pizzasNeeded(slices) {
  return Math.ceil(slices / 8);
}

const slices = slicesNeeded(10); // 20
const pizzas = pizzasNeeded(slices); // 3
console.log(pizzas); // 3
```

```python
# Python 3
import math

def slices_needed(guests):
    return guests * 2

def pizzas_needed(slices):
    return math.ceil(slices / 8)

slices = slices_needed(10)  # 20
pizzas = pizzas_needed(slices)  # 3
print(pizzas)  # Output: 3
```

### Key Differences for JS Developers

| Concept | JavaScript (ES6+) | Python 3 | Key Difference |
| :--- | :--- | :--- | :--- |
| **Default Return Value** | `undefined` | `None` | A Python function with no `return` statement returns `None` (`type(fn())` is `NoneType`). |
| **Arrow Implicit Return** | `const double = x => x * 2;` | **No implicit return** | Python `def` functions *always* require an explicit `return` keyword (even 1-line functions). |
| **Ceiling Rounding** | `Math.ceil(2.5)` -> `3` | `import math; math.ceil(2.5)` -> `3` | `Math` is global in JS; `math` must be explicitly imported in Python. |
| **Early Exit** | `if (!valid) return null;` | `if not valid: return None` | Both immediately terminate function execution upon hitting `return`. |

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code

#### Demo 1: The Broken Pipeline (`print()` Instead of `return`)
```python
import math

def slices_needed(guests):
    # Prints 20 to the console, then reaches the end and implicitly returns None!
    print(guests * 2)

def pizzas_needed(slices):
    # Receives slices = None -> attempts None / 8 -> CRASH!
    return math.ceil(slices / 8)

slices = slices_needed(10)
# Terminal displays: 20
# Variable 'slices' actually holds: None

pizzas = pizzas_needed(slices)
# Raises -> TypeError: unsupported operand type(s) for /: 'NoneType' and 'int'
```
**Why this breaks:** `slices_needed(10)` printed `20` on screen, fooling you into thinking it produced `20`, while actually returning `None`. When `pizzas_needed(None)` tried to execute `None / 8`, Python crashed with a `TypeError`.

#### Demo 2: The Working Data Pipeline (`return` + `math.ceil()`)
```python
import math

def slices_needed(guests):
    return guests * 2

def pizzas_needed(slices):
    return math.ceil(slices / 8)

# Step 1: Compute total slices (10 * 2 = 20)
slices = slices_needed(10)

# Step 2: Divide by 8 slices per pizza (20 / 8 = 2.5) and round up (math.ceil(2.5) = 3)
pizzas = pizzas_needed(slices)

print(pizzas)
# Output: 3
```
**Execution Trace:**
1. `slices_needed(10)` evaluates `10 * 2` -> `20` and hands `20` back to the caller.
2. `slices` stores the integer `20`.
3. `pizzas_needed(20)` evaluates `20 / 8` -> `2.5` (a `float`).
4. `math.ceil(2.5)` rounds `2.5` up to `3` (an `int`, because you cannot order 2.5 pizzas).
5. `pizzas` stores `3`, and `print(pizzas)` outputs `3`.

---

### Part B: The Challenge Code & Solutions

#### Challenge 1: `room_area(length, width)`
```python
def room_area(length, width):
    return length * width

# Note: Naming the result variable 'area' instead of 'room_area' avoids overwriting
# the function name itself in global scope (see Pitfall #1 below!)
area = room_area(width=10, length=12)
print(f"The room is {area} square feet.")
# Output: The room is 120 square feet.
```

#### Challenge 2: `add_tax(price)`
```python
def add_tax(price):
    return price * 1.08

price_with_tax = add_tax(50)

# Using :.2f formats 54.0 as 54.00 for currency display
print(f"With tax, that comes to ${price_with_tax:.2f}.")
# Output: With tax, that comes to $54.00.
```

#### Challenge 3: `full_name(first, last)`
```python
def full_name(first, last):
    # Joins the two strings with a single space separator
    return " ".join([first, last])
    # Alternative using f-string: return f"{first} {last}"
    # Other Alternative return first + " " + last

name = full_name(first="Mike", last="Reed")

print(f"Welcome, {name}!")
# Output: Welcome, Mike Reed!
```

---

## 5. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Overwriting a Function Name with Its Return Value (`TypeError: 'int' object is not callable`)
Because Python functions are stored as regular variables in the current namespace, assigning a return value to the **exact same name** as the function destroys your reference to the function:

```python
def room_area(length, width):
    return length * width

# First call works, BUT reassigns the name 'room_area' from <function> to 120 (int)!
room_area = room_area(width=10, length=12)
print(room_area)
# Output: 120

# Calling it a second time CRASHES because 'room_area' is now the integer 120:
second_room = room_area(8, 10)
# Raises -> TypeError: 'int' object is not callable
```

```python
# CORRECT FIX: Give the function a verb/action name and the variable a noun name
def calculate_room_area(length, width):
    return length * width

first_room = calculate_room_area(12, 10)
second_room = calculate_room_area(8, 10)
print(first_room, second_room)
# Output: 120 80
```

### 2. Unreachable Code After `return` (Silent Dead Code)
Any code written after a `return` statement inside the same branch is **never executed**. Python does not throw a syntax error—it simply exits the function the instant `return` runs:

```python
def add_tax(price):
    return price * 1.08
    # DEAD CODE: Never runs!
    print("Tax calculated!")

total = add_tax(50)
print(total)
# Output: 54.0  ("Tax calculated!" is never printed)
```

:::

:::warning

### 3. Returning Early Inside a Loop by Accident
Be careful with indentation when placing `return` inside a loop—if `return` is indented inside the loop body, it will exit the **entire function** on the very first iteration:

```python
# BUG: Exits on the first item instead of processing the whole list
def find_even_numbers_broken(numbers):
    evens = []
    for num in numbers:
        if num % 2 == 0:
            evens.append(num)
        return evens  # <-- Indented inside the loop! Exits immediately after checking 1!

print(find_even_numbers_broken([1, 2, 3, 4]))
# Output: []
```

```python
# CORRECT FIX: Unindent 'return' so it runs AFTER the loop finishes
def find_even_numbers(numbers):
    evens = []
    for num in numbers:
        if num % 2 == 0:
            evens.append(num)
    return evens

print(find_even_numbers([1, 2, 3, 4]))
# Output: [2, 4]
```

:::

---

## 6. Edge Cases to Watch For

:::note

### 1. Returning Multiple Values (Implicit Tuple Packing & Unpacking)
Unlike JavaScript, where you must wrap multiple return values in an object `{ area, perimeter }` or array `[area, perimeter]`, Python lets you separate multiple return values with commas. Python automatically packs them into a `tuple`:

```python
def room_metrics(length, width):
    area = length * width
    perimeter = 2 * (length + width)
    return area, perimeter  # Implicitly returns (120, 44)

# Unpack directly into two variables on the receiving end:
area, perimeter = room_metrics(12, 10)
print(f"Area: {area} sq ft, Perimeter: {perimeter} ft")
# Output: Area: 120 sq ft, Perimeter: 44 ft
```

### 2. Guard Clauses (Early Returns for Edge Cases)
Returning early at the top of a function keeps validation flat and eliminates deep `if / else` nesting:

```python
def add_tax(price):
    if price < 0:
        return 0.0  # Early exit for invalid negative price
    return price * 1.08

print(add_tax(-15))  # Output: 0.0
print(add_tax(50))   # Output: 54.0
```

### 3. `math.ceil()` vs. `math.floor()` vs. `round()`
```python
import math

print(math.ceil(2.1))   # Output: 3  (Always rounds UP to next integer)
print(math.floor(2.9))  # Output: 2  (Always rounds DOWN to previous integer)
print(round(2.5))       # Output: 2  (Banker's rounding: rounds .5 to nearest EVEN integer!)
print(round(3.5))       # Output: 4  (Banker's rounding: rounds .5 to nearest EVEN integer!)
```

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Composing Pure Calculation Functions + Formatting at the Edge
Keep business logic functions pure (returning raw `int` or `float` values) and apply string formatting (`:.2f`, `$`, `%`) only at the final display layer:

```python
def subtotal(price, quantity):
    return price * quantity

def apply_tax(amount, tax_rate=0.08):
    return amount * (1 + tax_rate)

# Compose functions together cleanly:
raw_total = apply_tax(subtotal(price=25.00, quantity=3))
print(f"Final Checkout Total: ${raw_total:.2f}")
# Output: Final Checkout Total: $81.00
```

### Pattern 2: Other Essential `math` Module Functions
```python
import math

print(math.sqrt(64))     # Output: 8.0   (Square root, returns float)
print(math.pi)           # Output: 3.141592653589793
print(math.fabs(-42.5))  # Output: 42.5  (Absolute value as float; built-in abs(-42) returns int)
```

:::