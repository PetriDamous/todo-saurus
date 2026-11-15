---
title: Functions (def), Separation of Concerns & random.randint()
sidebar_label: Functions, Separation of Concerns & random.randint()
sidebar_position: 1
---

# Python Notes: Functions (`def`), Separation of Concerns & `random.randint()`

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 3 — Functions & Data Structures (Building the Dice Fight Game / Code Organization)
- **Lesson Topic:** Defining & Calling Functions (`def`), Function Composition, Separation of Concerns & `random.randint()`
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~07pl](https://scrimba.com/learn-python-c03/~07pl)

:::

---

## 2. Concept Breakdown

:::note

This lesson introduces **functions**—reusable, named blocks of code that perform a specific task—alongside a foundational software engineering principle: **Separation of Concerns**:

- **Defining Functions (`def`):** Python uses the `def` keyword followed by a `snake_case` function name, parentheses `()`, and a colon `:`. All code belonging to the function must be indented (4 spaces by PEP 8 convention).
- **Defining vs. Calling:** Writing a `def` block only registers the instructions in memory—nothing executes until you invoke (call) the function by name with parentheses (`play_game()`).
- **Separation of Concerns & Composition:** Instead of writing one giant, tangled script, you break a program down into small, single-purpose functions (`show_welcome()`, `roll_dice()`, `throw_dice()`) and connect them inside an orchestrator function (`play_game()`). Each function owns one clear responsibility.
- **`random.randint(a, b)`:** A method from Python's built-in `random` module that returns a random integer between `a` and `b`, **inclusive of both endpoints** (so `random.randint(1, 6)` can return `1`, `2`, `3`, `4`, `5`, or `6`).

:::

---

## 3. JS vs. Python Mental Bridge

:::info

### Function Declaration & Invocation

```javascript
// JavaScript (ES6+)
function showWelcome() {
  console.log("");
  console.log("Welcome to Dice Fight!");
  console.log("");
}

// Calling the function
showWelcome();
```

```python
# Python 3
def show_welcome():
    print()
    print("Welcome to Dice Fight!")
    print()

# Calling the function
show_welcome()
```

### Key Syntax Differences for JS Developers

| Concept | JavaScript (ES6+) | Python 3 | Key Difference |
| :--- | :--- | :--- | :--- |
| **Function Keyword** | `function` (or `const fn = () =>`) | `def` | Short for "define". |
| **Naming Convention** | `camelCase` (`rollDice`) | `snake_case` (`roll_dice`) | Python PEP 8 standardizes on lowercase with underscores. |
| **Block Delimiters** | Curly braces `{ ... }` | Colon `:` + 4-space indentation | Unindenting marks the end of the function body. |
| **Hoisting** | `function` declarations are hoisted | **Not hoisted** | Functions must be defined *before* the line where they are called. |
| **Random Integer (1–6)** | `Math.floor(Math.random() * 6) + 1` | `random.randint(1, 6)` | Python's `randint` is inclusive on both ends and requires zero math formulas. |

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code (Dice Fight)

```python
import random

# 1. Single-responsibility helper: rolls one 6-sided die
def roll_dice():
    roll = random.randint(1, 6)
    print(f"You rolled a {roll}!")

# 2. Composes roll_dice() twice to simulate throwing two dice
def throw_dice():
    roll_dice()
    roll_dice()

# 3. UI display concern: prints the formatted game banner
def show_welcome():
    print()
    print("Welcome to Dice Fight!")
    print()

# 4. Orchestrator function: connects the workflow in order
def play_game():
    show_welcome()
    throw_dice()

# 5. Entry point: kicks off execution
play_game()
```

**Execution Trace & Output:**
```text

Welcome to Dice Fight!

You rolled a 4!
You rolled a 2!
```

:::note

**How the Call Stack Flows:**
1. Python reads all four `def` blocks and stores them in memory without printing anything.
2. Execution hits `play_game()` at the bottom.
3. `play_game()` calls `show_welcome()`, which prints the blank line, title, and blank line, then returns control to `play_game()`.
4. `play_game()` calls `throw_dice()`, which calls `roll_dice()` twice in sequence.
5. Once `throw_dice()` finishes, `play_game()` finishes, and the program exits.

:::

---

### Part B: The Challenge Code & Solution (Coworker Coffee Run)

```python
# Global data variables
coworkers = 6
coffee_price = 5

# 1. Announces the coffee run to the office
def annouce_run():
    print("I am headed to the coffee shop! Who wants a latte?")

# 2. Calculates and prints the order summary using an f-string
def total_cost():    
    print(f"{coworkers} lattes comes to ${coffee_price * coworkers}")

# 3. Prints "You're welcome!" twice per call (2 responses per call)
def thank_you():
    print("You're welcome!")
    print("You're welcome!")

# 4. Orchestrates the entire coffee run workflow
def coffee_run():
    annouce_run()
    total_cost()
    # 6 coworkers / 2 prints per thank_you() call = 3 calls needed
    thank_you()
    thank_you()
    thank_you()

# Start the program
coffee_run()
```

**Terminal Output:**
```text
I am headed to the coffee shop! Who wants a latte?
6 lattes comes to $30
You're welcome!
You're welcome!
You're welcome!
You're welcome!
You're welcome!
You're welcome!
```

:::tip

**Why Separation of Concerns Shines Here:**
Notice how `coffee_run()` reads like a high-level table of contents (`annouce_run()`, `total_cost()`, `thank_you()`). If you later need to change how the price is formatted or add sales tax, you only touch `total_cost()` without risking bugs in the announcement or thank-you logic.

*(Minor spelling detail: `annouce_run` works fine because both the definition and call match, though spelling it `announce_run` keeps code easier to search later.)*

:::

---

## 5. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Calling a Function Before Defining It (`NameError`)
In JavaScript, `function` declarations are hoisted to the top of their scope, so you can call `playGame()` on line 1 and define `function playGame()` on line 20. **Python executes top-to-bottom and does not hoist functions:**

```python
# INCORRECT:
play_game()  # Raises -> NameError: name 'play_game' is not defined

def play_game():
    print("Starting...")
```

```python
# CORRECT (Define first, call second):
def play_game():
    print("Starting...")

play_game()
# Output: Starting...
```

:::

:::warning

### 2. Referencing a Function Without Parentheses (`()`)
In both Python and JavaScript, functions are first-class objects. Writing a function's name without `()` refers to the function object itself rather than executing it:

```python
def greet():
    print("Hello!")

# INCORRECT (Does not run the function!):
greet
# Output: (Nothing happens!)

print(greet)
# Output: <function greet at 0x104a2b1f0>

# CORRECT:
greet()
# Output: Hello!
```

### 3. Forgetting the Colon (`:`) or Indentation (`IndentationError`)

```python
# INCORRECT (Missing colon):
# def greet()
#     print("Hello!")
# Raises -> SyntaxError: expected ':'

# INCORRECT (Missing indentation):
# def greet():
# print("Hello!")
# Raises -> IndentationError: expected an indented block

# CORRECT:
def greet():
    print("Hello!")
```

### 4. Off-by-One Assumption with `random.randint(a, b)`
Unlike Python's `range(1, 6)` or list slicing `[1:6]` (which exclude the upper bound `6`), `random.randint(1, 6)` **includes both `1` and `6`**:

```python
import random

# Simulates a standard 6-sided die (can return 1, 2, 3, 4, 5, or 6)
die_roll = random.randint(1, 6)

# INCORRECT (Simulates a 7-sided die!):
wrong_die = random.randint(1, 7)
```

:::

---

## 6. Edge Cases to Watch For

:::note

### 1. Empty Function Stubs (`pass`)
In JavaScript, you can write an empty placeholder function with `{}`. In Python, an empty indented block causes an `IndentationError`. When scaffolding out functions before writing their logic, use `pass`:

```python
# INCORRECT:
# def calculate_tax():
# Raises -> IndentationError: expected an indented block

# CORRECT:
def calculate_tax():
    pass  # Valid placeholder; does nothing without crashing

calculate_tax()
# Output: (Nothing printed, zero errors)
```

:::

:::danger

### 2. Reading vs. Modifying Outer Variables Inside a Function (`UnboundLocalError`)
In JavaScript, an inner function can freely read and reassign outer `let` variables (`coworkers = coworkers + 1`). In Python, functions can **read** outer variables freely, but assigning to a variable inside a function makes Python treat that variable as strictly local—crashing if you try to read it before assigning:

```python
coworkers = 6

# WORKS: Reading an outer variable
def show_count():
    print(f"Total coworkers: {coworkers}")

show_count()
# Output: Total coworkers: 6
```

```python
coworkers = 6

# CRASHES: Trying to modify an outer variable directly inside a function
def add_coworker():
    coworkers = coworkers + 1
    print(coworkers)

add_coworker()
# Raises -> UnboundLocalError: cannot access local variable 'coworkers' where it is not associated with a value
```

```python
# CORRECT FIX: Pass the value in as a parameter and return the updated result
def add_coworker(current_count):
    return current_count + 1

coworkers = 6
coworkers = add_coworker(coworkers)
print(coworkers)
# Output: 7
```

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Standard Python Script Structure (`main()` Entry Point)
As your programs grow, organizing helper functions at the top and grouping execution inside a single orchestrator function (`coffee_run()` or `main()`) keeps global scope clean:

```python
import random

def roll_die(sides):
    return random.randint(1, sides)

def main():
    first_roll = roll_die(6)
    second_roll = roll_die(6)
    print(f"Rolled {first_roll} and {second_roll} (Total: {first_roll + second_roll})")

main()
# Possible Output: Rolled 3 and 5 (Total: 8)
```

### Pattern 2: Replacing Repeated Calls with a Loop
When calling a function a fixed number of times (like calling `thank_you()` 3 times for 6 coworkers), a `while` loop scales effortlessly if `coworkers` changes from `6` to `20`:

```python
def thank_all(coworker_count):
    count = 0
    while count < coworker_count:
        print("You're welcome!")
        count += 1

thank_all(6)
# Output: Prints "You're welcome!" 6 times
```

:::