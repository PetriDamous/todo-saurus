---
title: while Loops, Loop Control (break) & Constants Convention
sidebar_label: while Loops & Control
sidebar_position: 3
---

# Python Notes: `while` Loops, Loop Control (`break`) & Constants Convention

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 2 — Control Flow & Logic (Building the Word-Scramble Game / Iteration)
- **Lesson Topic:** `while` Loops, Shorthand Incrementing (`+=`), `break` Statements & PEP 8 Constants
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~02nq](https://scrimba.com/learn-python-c03/~02nq)

:::

---

## 2. Concept Breakdown

:::note

This lesson introduces conditional iteration using `while` loops and demonstrates how to control loop termination:

- **How a `while` Loop Works:** A `while` loop repeatedly executes an indented block of code as long as its condition evaluates to `True`. Before every single iteration, Python checks the condition; once it evaluates to `False`, execution exits the loop and moves to the next unindented line.
- **Three Essential Parts of a Counter Loop:**
  1. **Initialization:** Setting a starting variable before the loop (`count = 1`).
  2. **Condition:** The boolean test evaluated on every pass (`while count <= 5:`).
  3. **Update / Step:** Modifying the state inside the loop so it eventually terminates (`count += 1`). Omitting this creates an infinite loop.
- **Early Exit with `break`:** Immediately terminates the loop regardless of whether the `while` condition is still `True`, jumping straight to the code after the loop.
- **Constants Naming Convention (`ALL_CAPS`):** Python has no language-enforced `const` keyword. By universal convention (PEP 8), variables intended to remain unchanged are written in `ALL_SNAKE_CAPS` (e.g., `PASSENGERS = 5`, `TOTAL_LAPS = 10`) to signal to other developers not to reassign them.

:::

---

## 3. JS vs. Python Mental Bridge

:::info

### Basic `while` Loop Syntax

```javascript
// JavaScript (ES6+)
let count = 1;

while (count <= 5) {
  console.log(count);
  count += 1;
}
```

```python
# Python 3
count = 1

while count <= 5:
    print(count)
    count += 1
```

### Increment Operators (`++` vs. `+=`)
JavaScript supports `count++` and `++count`. Python does not have `++` or `--` operators—you must use `+= 1` or `-= 1`:

```javascript
// JavaScript (ES6+)
let count = 1;
count++;    // Works (valid in JS)
count += 1; // Also works
```

```python
# Python 3
count = 1
# count++   -> SyntaxError: invalid syntax!
count += 1  # Standard Python increment
```

### Constants (`const` vs. `ALL_CAPS` Convention)

```javascript
// JavaScript (ES6+) - Enforced by the engine
const TOTAL_LAPS = 10;
// TOTAL_LAPS = 20; // Throws TypeError: Assignment to constant variable.
```

```python
# Python 3 - Convention only (PEP 8), not locked by the interpreter
TOTAL_LAPS = 10
# Python technically allows TOTAL_LAPS = 20, so uppercase is a human warning sign
```

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code

#### Demo 1: Standard Increment (`count = count + 1`)
```python
count = 1

while count <= 5:
    print(count)
    count = count + 1

# Output:
# 1
# 2
# 3
# 4
# 5
```
**Why this works:** On each pass, `count` increases by `1`. Once `count` reaches `6`, `6 <= 5` evaluates to `False`, ending the loop.

#### Demo 2: Augmented Assignment Shorthand (`count += 1`)
```python
count = 1

while count <= 5:
    print(count)
    count += 1  # Identical to count = count + 1

# Output:
# 1
# 2
# 3
# 4
# 5
```
**Why this works:** `+=` is the idiomatic shorthand for updating a variable in place.

#### Demo 3: The Infinite Loop Trap (Missing Update Step)

:::danger

```python
count = 1

# WARNING: Do not run without stopping!
while count <= 5:
    print(count)
    # Missing count += 1!

# Output:
# 1
# 1
# 1 ... (repeats forever until interrupted with Ctrl+C or browser tab freezes)
```
**Why this breaks:** `count` stays `1` forever, meaning `count <= 5` is permanently `True`.

:::

#### Demo 4: Stopping Early with `break`
```python
count = 1

while count <= 5:
    if count == 3:
        break  # Immediately exits the entire while loop
    print(count)
    count += 1

# Output:
# 1
# 2
```
**Execution trace:**
1. `count = 1`: `1 == 3` is `False` -> prints `1` -> `count` becomes `2`.
2. `count = 2`: `2 == 3` is `False` -> prints `2` -> `count` becomes `3`.
3. `count = 3`: `3 == 3` is `True` -> hits `break` -> loop terminates before `print(3)` ever runs.

#### Demo 5: Using `ALL_CAPS` for Constants
```python
TOTAL_LAPS = 10
lap = 1

while lap <= TOTAL_LAPS:
    print(f"Lap: {lap}")
    lap += 1

# Output:
# Lap: 1
# Lap: 2
# ...
# Lap: 10
```
**Why this works:** Naming `TOTAL_LAPS` in uppercase clearly separates the fixed boundary (`10`) from the mutable counter variable (`lap`).

---

### Part B: The Challenge Code & Solution

```python
# Constant representing total passengers in the group booking
PASSENGERS = 5

# Mutable counter tracking the current passenger
passenger_num = 1

# Loop runs from passenger 1 through passenger 5 (inclusive)
while passenger_num <= PASSENGERS:
    print(f"Printing boarding pass {passenger_num} of {PASSENGERS}...")
    passenger_num += 1

# Output:
# Printing boarding pass 1 of 5...
# Printing boarding pass 2 of 5...
# Printing boarding pass 3 of 5...
# Printing boarding pass 4 of 5...
# Printing boarding pass 5 of 5...
```

:::note

*(Note: Adding the trailing `...` inside the f-string matches the exact formatting requested in the challenge prompt: `"Printing boarding pass 1 of 5..."`.)*

:::

---

## 5. Common Pitfalls & Gotchas for JS Devs

:::warning

### 1. Writing `count++` Out of Muscle Memory
```python
# JavaScript habit:
# count++

# In Python, ++ is NOT an increment operator:
x = 5
# x++  -> SyntaxError: invalid syntax

# Subtle trap: ++x DOES NOT error, it acts as two unary plus signs (+(+x))!
++x
print(x)
# Output: 5 (It silently did nothing!)
```

### 2. Off-by-One Errors (`<` vs. `<=`)
```python
PASSENGERS = 5
passenger_num = 1

# Using '<' instead of '<=' stops at 4:
while passenger_num < PASSENGERS:
    print(f"Passenger {passenger_num}")
    passenger_num += 1
# Output: Prints 1, 2, 3, 4 (Misses passenger 5!)
```

### 3. Using `do...while` Loops
JavaScript has `do { ... } while (condition);` to guarantee at least one execution. Python has no `do...while` loop. In Python, you replicate it using `while True:` paired with an `if ...: break` at the bottom:

```python
# Python equivalent of JS do...while
while True:
    user_input = input("Enter 'quit' to exit: ")
    if user_input == "quit":
        break
```

:::

---

## 6. Edge Cases to Watch For

:::danger

### Skipping an Iteration with `continue` vs. Exiting with `break`
- `break` kills the entire loop.
- `continue` skips the rest of the current iteration and jumps straight back to the `while` condition check. **Warning:** Always update your counter before calling `continue`, or you will create an infinite loop!

```python
num = 0

while num < 5:
    num += 1  # Increment BEFORE continue!
    if num == 3:
        continue  # Skips printing 3, moves on to 4
    print(num)

# Output:
# 1
# 2
# 4
# 5
```

:::

:::note

### Zero-Passenger Booking (`PASSENGERS = 0`)
If `PASSENGERS = 0` and `passenger_num = 1`, the initial check `1 <= 0` immediately evaluates to `False`. The loop body runs `0` times, safely printing nothing without crashing.

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Input Validation Loop (Keep Asking Until Valid)
A classic real-world use case for `while` loops is re-prompting a user until they provide valid input:

```python
password = ""

while password != "secret123":
    password = input("Enter password: ")

print("Access granted!")
```

### Pattern 2: Countdown Timer
```python
seconds = 3

while seconds > 0:
    print(f"Launching in {seconds}...")
    seconds -= 1

print("Liftoff!")
# Output:
# Launching in 3...
# Launching in 2...
# Launching in 1...
# Liftoff!
```
:::