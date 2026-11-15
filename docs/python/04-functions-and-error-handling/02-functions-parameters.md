---
title: Function Parameters, Arguments & Variable Scope (LEGB)
sidebar_label: Function Parameters, Arguments & Variable Scope (LEGB)
sidebar_position: 2
---

# Python Notes: Function Parameters, Arguments & Variable Scope (LEGB)

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 3 — Functions & Data Structures (Building the Dice Fight Game / Reusable Functions)
- **Lesson Topic:** Function Parameters vs. Arguments, Positional Ordering & Local vs. Global Scope
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~024g](https://scrimba.com/learn-python-c03/~024g)

:::

---

## 2. Concept Breakdown

:::note

This lesson upgrades functions from static, hardcoded routines into reusable, dynamic building blocks by introducing **parameters**, **arguments**, and **variable scope**:

- **Parameters vs. Arguments:**
  - **Parameter:** The variable name listed inside the parentheses in the function definition (`def greet(name):`). Think of defining a parameter as declaring a local variable placeholder.
  - **Argument:** The actual value passed into the function when you call it (`greet("Jenny")`). Think of passing an argument as assigning a value to that parameter variable (`name = "Jenny"`).
- **Positional Argument Matching:** By default, Python maps arguments to parameters strictly by left-to-right position. Passing arguments in the wrong order binds values to the wrong parameter names.
- **Variable Scope (Local vs. Global):**
  - **Global Scope:** Variables defined at the top level of a file (`shop_name = "The Coffee Shop"`). Any function in the file can *read* global variables, but relying on globals couples your functions to external state.
  - **Local Scope:** Variables created inside a function—including **all parameters** and any variables assigned inside the function body (`letters = list(word)`). Local variables exist only while that specific function call is executing and are destroyed as soon as the function finishes. Keeping state scoped locally makes functions self-contained, predictable, and reusable across any file or project.

:::

---

## 3. JS vs. Python Mental Bridge

:::info

### Parameters, Arguments & Scope Side-by-Side

```javascript
// JavaScript (ES6+)
const shopName = "The Coffee Shop"; // Module/Global scope

function greet(name, unreadMessages) { // Parameters
  const prefix = "Welcome";            // Function-scoped local variable
  console.log(`${prefix}, ${name}! You have ${unreadMessages} new messages at ${shopName}.`);
}

greet("Jenny", 15); // Arguments passed positionally
// console.log(prefix); // ReferenceError: prefix is not defined
```

```python
# Python 3
shop_name = "The Coffee Shop"  # Global scope

def greet(name, unread_messages):  # Parameters
    prefix = "Welcome"             # Local variable
    print(f"{prefix}, {name}! You have {unread_messages} new messages at {shop_name}.")

greet("Jenny", 15)  # Arguments passed positionally
# print(prefix)     # NameError: name 'prefix' is not defined
```

### Key Scoping & Argument Differences for JS Developers

| Concept | JavaScript (ES6+) | Python 3 | Key Difference |
| :--- | :--- | :--- | :--- |
| **Block Scope (`if`, `for`, `while`)** | `let` and `const` are block-scoped `{}` | **No block scope** | Variables created inside `if`, `for`, or `while` belong to the enclosing function (or global scope). Only `def`, `class`, and comprehensions create new scopes. |
| **Missing Arguments** | Missing params default to `undefined` (`greet("Jenny")` runs) | **`TypeError` crash** | Python strictly enforces parameter counts unless default values are defined. |
| **Extra Arguments** | Extra arguments are silently ignored | **`TypeError` crash** | Passing more arguments than defined parameters raises an immediate `TypeError`. |
| **Keyword Arguments** | Simulated via destructured objects `greet({ name: "Jenny" })` | **Built-in natively** | Python lets you pass arguments by name (`greet(unread_messages=15, name="Jenny")`) in any order. |

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code

#### Demo 1: Single Parameter & Multiple Calls
```python
# 'name' is the parameter (variable placeholder)
def greet(name):
    print(f"Welcome, {name}!")

# Each call passes a different argument (value) into 'name'
greet("Jenny")   # name = "Jenny"  -> Output: Welcome, Jenny!
greet("Marcus")  # name = "Marcus" -> Output: Welcome, Marcus!
greet("Mary")    # name = "Mary"   -> Output: Welcome, Mary!
greet("Sam")     # name = "Sam"    -> Output: Welcome, Sam!
```
**Why this works:** Each invocation creates a fresh local binding for `name`, executes the `print()`, and cleans up `name` before the next call runs.

#### Demo 2: Multiple Parameters & Positional Order
```python
def greet(name, unread_messages):
    print(f"Welcome, {name}! You have {unread_messages} new messages.")

# 1. Correct positional order: arg 1 -> name, arg 2 -> unread_messages
greet("Jenny", 15)
# Output: Welcome, Jenny! You have 15 new messages.

# 2. Swapped positional order: arg 1 (15) -> name, arg 2 ("Jenny") -> unread_messages
greet(15, "Jenny")
# Output: Welcome, 15! You have Jenny new messages.
```

:::warning

**Why Swapping Arguments Didn't Crash Here:** Because Python is dynamically typed and f-strings convert both `int` and `str` via `str()`, `greet(15, "Jenny")` produced a nonsense sentence instead of an error. If the function had performed math on `unread_messages` (e.g., `unread_messages + 1`), swapping the arguments would have crashed with a `TypeError: can only concatenate str (not "int") to str`.

:::

#### Demo 3: Reading Global Scope Inside a Function
```python
shop_name = "The Coffee Shop"

def show_welcome():
    # Python looks for 'shop_name' locally; not finding it, looks outward to global scope
    print(f"Welcome to {shop_name}")

show_welcome()
# Output: Welcome to The Coffee Shop
```

#### Demo 4: Why Local Scope Makes Functions Reusable (Global Coupling vs. Local Parameters)
```python
# TIGHTLY COUPLED (Relies on global state — hard to reuse):
tax_rate = 0.08
price = 100

def print_total_coupled():
    total = price + (price * tax_rate)
    print(f"Total: ${total:.2f}")

print_total_coupled()
# Output: Total: $108.00
# To calculate a different item or tax rate, you have to mutate global variables!
```

```python
# DECOUPLED & REUSABLE (All data passed via local parameters):
def print_total_reusable(price, tax_rate):
    # 'price', 'tax_rate', and 'total' are 100% isolated inside this function call
    total = price + (price * tax_rate)
    print(f"Total: ${total:.2f}")

print_total_reusable(100, 0.08)  # Output: Total: $108.00
print_total_reusable(45, 0.065)  # Output: Total: $47.92
print_total_reusable(20, 0.0)    # Output: Total: $20.00
```

```python
# Another pattern where scoping a variable locally can work too.
def print_total_reusable(price):
    # Single place to change tax_rate when tax_rates change
    # Goes anywhere the function goes.
    tax_rate = 0.08

    total = price + (price * tax_rate)
    print(f"Total: ${total:.2f}")

print_total_reusable(100)  # Output: Total: $108.00
print_total_reusable(45)  # Output: Total: $48.60
print_total_reusable(20)    # Output: Total: $21.60
```

---

### Part B: The Challenge Code & Solutions

#### Challenge 1: `add_numbers(a, b)`
```python
# Note: In your draft, print({a + b}) wrapped the sum in curly braces {},
# which creates a Python set (e.g., {4}, {9}) instead of printing a plain integer!
# Remove the outer braces so print() receives the integer directly:

def add_numbers(a, b):
    print(a + b)

add_numbers(2, 2)
# Output: 4

add_numbers(5, 4)
# Output: 9

add_numbers(10, 45)
# Output: 55
```

:::danger

**Watch Out for `{a + b}` Outside of f-Strings:**
In Python, `{}` without an `f` prefix in front of quotes creates a **set** data structure, not a code block or expression wrapper:
```python
print({2 + 2})  # Output: {4}  <-- Type is <class 'set'>!
print(2 + 2)    # Output: 4    <-- Type is <class 'int'>!
```

:::

#### Challenge 2: `scramble_word(word)`
```python
import random

def scramble_word(word):
    # 'letters' is strictly local to scramble_word(); it does not leak into global scope
    letters = list(word)
    random.shuffle(letters)
    print(f"Scrambled word: {''.join(letters)}")

scramble_word("functions")
# Possible Output: Scrambled word: ntuifocsn

scramble_word("python")
# Possible Output: Scrambled word: nohtyp
```

:::note

**Double Quotes Inside Double-Quoted f-Strings (Python 3.12+ vs. Older Python):**
In Python 3.12+, reusing double quotes inside an f-string (`f"Scrambled word: {"".join(letters)}"`) is valid syntax. In Python 3.11 and earlier, reusing the same quote type inside `{}` raises a `SyntaxError: f-string: expecting '}'`. Using single quotes inside (`f"Scrambled word: {''.join(letters)}"`) works across **all** Python 3 versions.

:::

---

## 5. Deep Dive: Python's LEGB Scope Lookup Rule

When you reference a variable inside a function, Python searches for it in four scopes in strict **LEGB** order:
1. **L — Local:** Variables assigned or passed as parameters inside the current `def` function.
2. **E — Enclosing:** Variables in outer functions (when functions are nested inside other functions, like closures in JS).
3. **G — Global:** Variables defined at the top level of the module/file.
4. **B — Built-in:** Python's preloaded names (`print`, `len`, `list`, `int`, `TypeError`).

```python
level = "Global"

def outer():
    level = "Enclosing"

    def inner():
        level = "Local"
        print(level)  # Finds 'Local' first and stops searching

    inner()
    print(level)      # Finds 'Enclosing'

outer()
print(level)          # Finds 'Global'

# Output:
# Local
# Enclosing
# Global
```

---

## 6. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Missing or Extra Arguments (`TypeError`)
JavaScript is permissive with function arity (argument count); Python is strict:

```python
def greet(name, unread_messages):
    print(f"Welcome, {name}! You have {unread_messages} new messages.")

# INCORRECT (Missing 1 argument):
# greet("Jenny")
# Raises -> TypeError: greet() missing 1 required positional argument: 'unread_messages'

# INCORRECT (1 extra argument):
# greet("Jenny", 15, "VIP")
# Raises -> TypeError: greet() takes 2 positional arguments but 3 were given
```

### 2. Shadowing a Global Variable & Expecting the Global to Change
Assigning to a variable name inside a function creates a **brand-new local variable** that shadows the global variable without modifying it:

```python
discount = 10

def apply_promo():
    discount = 50  # Creates a LOCAL 'discount' variable; does NOT change global 'discount'!
    print(f"Inside function: {discount}%")

apply_promo()
print(f"Outside function: {discount}%")

# Output:
# Inside function: 50%
# Outside function: 10%
```

:::

:::warning

### 3. Assuming `if` or `while` Blocks Create Local Scope
Unlike JavaScript's `let`/`const`, Python does **not** scope variables to `if`, `for`, or `while` blocks:

```python
# JavaScript:
# if (true) {
#   const secret = "123";
# }
# console.log(secret); // ReferenceError: secret is not defined

# Python:
if True:
    secret = "123"

print(secret)
# Output: 123 (Leaks into the enclosing function or global scope!)
```

### 4. Shadowing Built-in Names (`list`, `str`, `id`, `sum`)
Because **Built-in (B)** is the *last* step in LEGB lookup, naming a parameter or variable `list` or `str` overrides Python's built-in type constructor in that scope:

```python
# INCORRECT:
def broken_scramble(list):  # Shadows built-in list()!
    # letters = list("word")  # Raises -> TypeError: 'str' object is not callable
    pass

# CORRECT:
def working_scramble(word):
    letters = list(word)
    return letters
```

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Keyword Arguments for Self-Documenting Calls
Even without changing the function definition, Python allows callers to pass arguments by parameter name—preventing positional mix-ups like `greet(15, "Jenny")`:

```python
def greet(name, unread_messages):
    print(f"Welcome, {name}! You have {unread_messages} new messages.")

# Order no longer matters when using keyword arguments:
greet(unread_messages=15, name="Jenny")
# Output: Welcome, Jenny! You have 15 new messages.
```

### Pattern 2: Default Parameter Values (Just Like JS Default Params)
You can make parameters optional by providing fallback values in the signature:

```python
# JavaScript equivalent: function greet(name, unreadMessages = 0) { ... }
def greet(name, unread_messages=0):
    print(f"Welcome, {name}! You have {unread_messages} new messages.")

greet("Marcus")      # Uses default 0 -> Output: Welcome, Marcus! You have 0 new messages.
greet("Jenny", 15)   # Overrides with 15 -> Output: Welcome, Jenny! You have 15 new messages.
```

### Pattern 3: Returning Values Instead of Printing Inside Helpers
Printing inside a helper function locks output to the terminal. Returning a value keeps the function pure so the caller decides whether to print it, store it, or pass it to another function:

```python
import random

def scramble_word(word):
    letters = list(word)
    random.shuffle(letters)
    return "".join(letters)

# Caller can print, store in a list, or compare:
scrambled = scramble_word("functions")
print(f"Scrambled word: {scrambled}")
```

:::