---
title: Tuples, Immutability & Tuple Unpacking
sidebar_label: Tuples & Unpacking
sidebar_position: 5
---

# Python Notes: Tuples, Immutability & Tuple Unpacking

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 2 — Control Flow & Logic (Building the Word-Scramble Game / Data Structures)
- **Lesson Topic:** Tuples, Lists vs. Tuples & Sequence Unpacking
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~0zoz](https://scrimba.com/learn-python-c03/~0zoz)

:::

---

## 2. Concept Breakdown

This lesson introduces tuples (`tuple`), one of Python's four built-in collection data types (alongside `list`, `dict`, and `set`), and demonstrates unpacking:

- **What is a Tuple?** An ordered, indexed collection of elements wrapped in parentheses `()`. Just like a list, a tuple can hold mixed data types (e.g., `("notebooks", 42)`) and allows duplicate values.
- **Difference Between Tuples and Lists:**
  - **Lists (`[]`) are mutable:** You can add, remove, or overwrite elements after creation (`my_list[0] = "new"`). Lists are meant for dynamic, homogenous collections that grow or shrink over time.
  - **Tuples (`()`) are immutable:** Once created, you cannot change, add, or remove items (`my_tuple[0] = "new"` raises a `TypeError`). Tuples are used for fixed records or grouped data that belong together as a single unit (such as RGB color coordinates, `(latitude, longitude)` pairs, or database rows).
  - **Performance & Safety:** Because tuples are fixed in size, Python allocates a single static block of memory for them, making them slightly faster and more memory-efficient than lists—and guaranteeing data integrity against accidental mutation.
- **Tuple Unpacking:** A clean syntax that extracts all elements from a tuple and assigns them to individual variables in a single statement (`red, green, blue = steel_blue`).

---

## 3. JS vs. Python Mental Bridge

:::info

### Does JavaScript Have Tuples?
Vanilla JavaScript does not have a native tuple type (the TC39 Record & Tuple proposal never reached standard ES adoption). In JS, developers simulate tuples using standard Arrays, TypeScript tuple types (`[string, number]`), or `Object.freeze()`:

```javascript
// JavaScript (ES6+) - Simulating an immutable tuple
const steelBlue = Object.freeze([70, 130, 180]);

// Attempting to mutate fails silently (or throws TypeError in strict mode)
// steelBlue[0] = 255;
console.log(steelBlue[1]); // 130
```

```python
# Python 3 - Native tuple syntax
steel_blue = (70, 130, 180)

# Attempting to mutate immediately raises a TypeError
# steel_blue[0] = 255  -> TypeError: 'tuple' object does not support item assignment
print(steel_blue[1]) # Output: 130
```

### Tuple Unpacking vs. Array Destructuring
Python's unpacking works almost identically to JavaScript's array destructuring, minus the square brackets on the left side:

```javascript
// JavaScript (ES6+) - Array Destructuring
const steelBlue = [70, 130, 180];
const [red, green, blue] = steelBlue;

console.log(red);   // 70
console.log(green); // 130
console.log(blue);  // 180
```

```python
# Python 3 - Tuple Unpacking
steel_blue = (70, 130, 180)
red, green, blue = steel_blue

print(red)   # Output: 70
print(green) # Output: 130
print(blue)  # Output: 180
```

### Lists vs. Tuples Side-by-Side

```python
# LIST: Mutable (can change contents)
shopping_list = ["milk", "eggs"]
shopping_list.append("bread")
shopping_list[0] = "oat milk"
print(shopping_list) # Output: ['oat milk', 'eggs', 'bread']

# TUPLE: Immutable (locked after creation)
coordinates = (29.4241, -98.4936)
# coordinates[0] = 30.0000  # Crashes with TypeError!
print(coordinates) # Output: (29.4241, -98.4936)
```

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code

#### Demo 1: Accessing Elements via Bracket Notation
```python
steel_blue = (70, 130, 180)

# Tuples are zero-indexed, just like lists and JS arrays
print(steel_blue[1])
# Output: 130
```
:::note
**Why this works:** Even though tuples are defined with parentheses `()`, you still access elements by index using square brackets `[]`.
:::

#### Demo 2: Basic Tuple Unpacking
```python
steel_blue = (70, 130, 180)

# Unpacks the 3 items in order into 3 matching variables
red, green, blue = steel_blue

print(red)   # Output: 70
print(green) # Output: 130
print(blue)  # Output: 180
```
:::note
**Why this works:** Python counts the items on the right (`3`) and matches them position-by-position to the variable names on the left (`red`, `green`, `blue`).
:::

#### Demo 3: A List of Tuples (Nested Data Structure)
```python
color_palette = [
  (70, 130, 180),   # Index 0
  (240, 128, 128),  # Index 1
  (60, 179, 113)    # Index 2
]

# Accessing the first tuple inside the list
print(color_palette[0])
# Output: (70, 130, 180)

# Unpacking the first tuple (index 0) and formatting with an f-string
red, green, blue = color_palette[0]
print(f"RGB: {red}, {green}, {blue}")
# Output: RGB: 70, 130, 180

# Reusing the same variable names to unpack the second tuple (index 1)
red, green, blue = color_palette[1]
print(f"RGB: {red}, {green}, {blue}")
# Output: RGB: 240, 128, 128
```
:::note
**Why this works:** Combining a mutable `list` outer container with immutable `tuple` inner records is a core Python pattern. You can add or remove colors from `color_palette`, while each individual RGB color stays protected as an immutable 3-part unit.
:::

---

### Part B: The Challenge Code & Solution

```python
# A list containing 3 tuples; each tuple pairs a string (item name) with an int (stock count)
inventory = [
    ("notebooks", 42),
    ("pens", 130),
    ("staplers", 8),
]

# 1. Access each tuple by list index and unpack its two values into descriptive variables
notebooks, notebooks_stock = inventory[0]
pens, pens_stock = inventory[1]
staplers, staplers_stock = inventory[2]

# 2. Format and print each unpacked pair using f-strings
print(f"{notebooks}: {notebooks_stock} in stock")
# Output: notebooks: 42 in stock

print(f"{pens}: {pens_stock} in stock")
# Output: pens: 130 in stock

print(f"{staplers}: {staplers_stock} in stock")
# Output: staplers: 8 in stock
```

---

## 5. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Unpacking Count Mismatch (`ValueError`)
In JavaScript, destructuring fewer variables than array elements silently ignores the extras, and extra variables become `undefined`. In Python, the variable count must match the tuple length exactly:

```python
# JavaScript:
# const [a, b] = [1, 2, 3]; // Works! a = 1, b = 2

# Python:
point = (10, 20, 30)

# INCORRECT (Too few variables):
# x, y = point
# Raises -> ValueError: too many values to unpack (expected 2)

# INCORRECT (Too many variables):
# x, y, z, w = point
# Raises -> ValueError: not enough values to unpack (expected 4, got 3)
```

:::

:::warning

### 2. Single-Element Tuple Trailing Comma Trap
Parentheses in Python are also used for grouping math expressions (`(5 + 3)`). To create a tuple with only one item, you must include a trailing comma:

```python
not_a_tuple = ("notebooks")
print(type(not_a_tuple))
# Output: <class 'str'> (Python treated the parentheses as grouping!)

actual_tuple = ("notebooks",)
print(type(actual_tuple))
# Output: <class 'tuple'> (The trailing comma makes it a tuple)
```

### 3. Mutating a Mutable Object Inside a Tuple
While a tuple itself cannot have items reassigned, if a tuple holds a mutable object (like a list), that inner list can still be modified:

```python
record = ("Alice", [90, 85])

# You cannot replace the list itself:
# record[1] = [100]  # Raises -> TypeError: 'tuple' object does not support item assignment

# You CAN mutate the list inside the tuple:
record[1].append(95)
print(record)
# Output: ('Alice', [90, 85, 95])
```

:::

---

## 6. Edge Cases to Watch For

:::note

### Swapping Variables Without a Temporary Variable
Because Python evaluates the right side of an assignment as an implicit tuple before unpacking it into the left side, swapping two variables takes one line:

```python
a = "first"
b = "second"

# Implicitly creates ("second", "first") and unpacks into a, b
a, b = b, a

print(a) # Output: "second"
print(b) # Output: "first"
```

### Ignoring Unwanted Values with `_`
If a tuple has values you don't need, Python convention uses an underscore `_` as a throwaway variable name:

```python
user_record = ("jsmith", "jsmith@example.com", "admin")

# Only grab username and role, ignoring email
username, _, role = user_record
print(f"{username} ({role})")
# Output: jsmith (admin)
```

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Unpacking Directly Inside a `for` Loop (Preview of Next Concept)
Instead of manually unpacking `inventory[0]`, `inventory[1]`, `inventory[2]`, Python lets you unpack tuples right in the `for` loop header:

```python
inventory = [
    ("notebooks", 42),
    ("pens", 130),
    ("staplers", 8),
]

for item, stock in inventory:
    print(f"{item}: {stock} in stock")

# Output:
# notebooks: 42 in stock
# pens: 130 in stock
# staplers: 8 in stock
```

### Pattern 2: Returning Multiple Values from a Function
Python functions frequently return tuples to pass back multiple pieces of data cleanly (similar to returning an object or array in JS):

```python
def get_dimensions():
    return (1920, 1080)

width, height = get_dimensions()
print(f"{width}x{height}")
# Output: 1920x1080
```

:::
