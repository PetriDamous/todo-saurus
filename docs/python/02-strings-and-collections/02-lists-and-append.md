---
title: Lists, JS Array Comparison & .append()
sidebar_label: Lists & .append()
sidebar_position: 2
---

# Python Notes: Lists & Appending Elements (`list.append()`)

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 2 — Control Flow & Logic (Building the Word-Scramble Game / Lists)
- **Lesson Topic:** Creating Empty Lists & Mutating Lists in Place with `.append()`
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~03gu](https://scrimba.com/learn-python-c03/~03gu)

:::

---

## 2. Python List vs. JavaScript Array Mental Model

:::info

For a JavaScript developer: **Python List ≈ JavaScript Array**.

```javascript
// JavaScript
const fruits = ["apple", "banana", "orange"];
```

```python
# Python
fruits = ["apple", "banana", "orange"]
```

Immediately you'll notice:
- Square brackets `[]`
- Ordered collection of values
- Index access
- Can contain multiple data types

:::

### Accessing Items
```javascript
// JavaScript
const fruits = ["apple", "banana", "orange"];
console.log(fruits[0]); // apple
```

```python
# Python
fruits = ["apple", "banana", "orange"]
print(fruits[0]) # apple
```

### Length
- **JavaScript:** `fruits.length`
- **Python:** `len(fruits)` — Python uses a built-in function `len()` instead of a property.

### Add & Remove Items
- **Add:** JavaScript `fruits.push("grape");` vs. Python `fruits.append("grape")`
- **Remove:** JavaScript `fruits.pop();` vs. Python `fruits.pop()`

### Mixed Data Types
```python
stuff = [
    "Dimitri",
    35,
    True
]
```
Just like JavaScript (`["Dimitri", 35, true]`), although Python developers typically try to keep collections more consistent.

### Where Lists Start Differing: Negative Indexing & Slicing

#### Negative Indexing (Python Superpower)

:::tip

```python
fruits = ["apple", "banana", "orange"]
print(fruits[-1])
# Output: orange
```
JavaScript doesn't have this behavior. In Python:
- `0` = first item
- `1` = second item
- `2` = third item
- `-1` = last item
- `-2` = second-to-last item

:::

#### Slicing
```python
fruits = ["apple", "banana", "orange", "grape"]
print(fruits[1:3])
# Output: ['banana', 'orange']
```

---

## 3. Concept Breakdown: Mutating Lists with `.append()`

:::note

This lesson introduces lists (`list`)—Python's primary dynamic, ordered collection—and demonstrates how to build a list incrementally using `.append()`:

- **Lists Are Mutable:** Unlike strings (`str`) and tuples (`tuple`), Python lists can be modified in place after creation. You do not need to reassign the variable (`lobby = lobby.append(...)` is a bug!) when adding items.
- **What `.append(item)` Does:** Adds a single element to the very end of an existing list and returns `None`.
- **Dynamic Sizing:** Starting with an empty list (`[]`) and appending items one by one as events occur (such as user inputs or players joining a game) is one of the most common patterns in Python.

:::

---

## 4. JS vs. Python Mental Bridge

:::info

### Creating and Appending to Arrays / Lists

```javascript
// JavaScript (ES6+)
const tasks = [];
tasks.push("Send invoices");
tasks.push("Book the venue");

console.log(tasks); // ["Send invoices", "Book the venue"]
```

```python
# Python 3
tasks = []
tasks.append("Send invoices")
tasks.append("Book the venue")

print(tasks) # Output: ['Send invoices', 'Book the venue']
```

### Key Difference: Return Value of `.push()` vs. `.append()`

In JavaScript, `arr.push(item)` returns the new length of the array. In Python, `list.append(item)` returns `None` because it mutates the list directly in memory:

```javascript
// JavaScript (ES6+)
const arr = ["a", "b"];
const returnVal = arr.push("c");
console.log(returnVal); // 3 (new array length)
```

```python
# Python 3
items = ["a", "b"]
return_val = items.append("c")
print(return_val) # Output: None
print(items)      # Output: ['a', 'b', 'c']
```

:::

---

## 5. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code

#### Demo 1: Initializing an Empty List & Adding Hardcoded Items
```python
tasks = []  # Creates an empty list

tasks.append("Send invoices")
tasks.append("Book the venue")
tasks.append("Reply to emails")

print(tasks)
# Output: ['Send invoices', 'Book the venue', 'Reply to emails']
```
**Why this works:** Each call to `.append()` places the string at the next available index (`0`, then `1`, then `2`), mutating `tasks` directly in memory.

#### Demo 2: Appending Dynamic User Input (`input()`)
```python
tasks = ["Send invoices", "Book the venue", "Reply to emails"]

# Captures text from the terminal as a string
task_item = input("Add an item: ")  # Suppose user types: "Call catering"

# Appends whatever the user typed onto the end of the list
tasks.append(task_item)

print(tasks)
# Output: ['Send invoices', 'Book the venue', 'Reply to emails', 'Call catering']
```
**Why this works:** Variables can be passed directly into `.append()`. Since `tasks` holds strings and `input()` returns a string, the types match cleanly.

---

### Part B: The Challenge Code & Solution

```python
# 1. Start with an empty list
lobby = []

# 2. Append players one at a time and observe the list growing after each step
lobby.append("Xena")
print(lobby)
# Output: ['Xena']

lobby.append("Thor")
print(lobby)
# Output: ['Xena', 'Thor']

lobby.append("Merlin")
print(lobby)
# Output: ['Xena', 'Thor', 'Merlin']

lobby.append("Ripley")
print(lobby)
# Output: ['Xena', 'Thor', 'Merlin', 'Ripley']
```
:::note
*Note on Step 3 of the prompt:* Printing after every `.append()` is great for debugging and watching state mutate step-by-step, while leaving only the final `print(lobby)` at the bottom prints the single final list `['Xena', 'Thor', 'Merlin', 'Ripley']`.
:::

---

## 6. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Reassigning a Variable to `.append()` (Wipes Your List to `None`!)
Because string methods return new strings (`name = name.strip()`), beginners often assume list methods work the same way. Because `.append()` returns `None`, reassigning overwrites your entire list:

```python
lobby = ["Xena"]

# INCORRECT:
lobby = lobby.append("Thor")
print(lobby)
# Output: None (Your list is gone!)

# CORRECT:
lobby = ["Xena"]
lobby.append("Thor")
print(lobby)
# Output: ['Xena', 'Thor']
```

:::

:::warning

### 2. Passing Multiple Arguments to `.append()` (`TypeError`)
In JavaScript, `arr.push("a", "b", "c")` adds three items at once. In Python, `.append()` accepts strictly one argument:

```python
lobby = ["Xena"]

# INCORRECT:
# lobby.append("Thor", "Merlin")
# Raises -> TypeError: list.append() takes exactly one argument (2 given)

# CORRECT (use .extend() to add multiple items from another iterable):
lobby.extend(["Thor", "Merlin"])
print(lobby)
# Output: ['Xena', 'Thor', 'Merlin']
```

### 3. Appending a List Instead of Extending It (Nested Lists)
If you pass a list into `.append()`, Python adds the entire list as a single nested element rather than merging the items:

```python
lobby = ["Xena"]
new_players = ["Thor", "Merlin"]

lobby.append(new_players)
print(lobby)
# Output: ['Xena', ['Thor', 'Merlin']]  <-- Nested list! Length is 2, not 3!
```

:::

---

## 7. Edge Cases to Watch For

:::note

### Inserting at Specific Positions vs. Appending to the End
`.append()` always adds to index `-1` (the end). If you need to insert at the beginning or middle of a list (like JS `arr.unshift()` or `arr.splice()`), use `.insert(index, item)`:

```python
lobby = ["Xena", "Thor"]

# Insert "VIP_Admin" at index 0 (equivalent to JS lobby.unshift("VIP_Admin"))
lobby.insert(0, "VIP_Admin")
print(lobby)
# Output: ['VIP_Admin', 'Xena', 'Thor']
```

:::

---

## 8. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Building a List Inside a `while` Loop
Combining `while` loops with `.append()` lets you collect an unknown number of items until a stop condition is met:

```python
lobby = []

while len(lobby) < 4:
    player = input("Enter player name: ")
    lobby.append(player)

print(f"Lobby full! Players: {lobby}")
```

### Pattern 2: Removing Items from a List (`.pop()` & `.remove()`)
```python
lobby = ["Xena", "Thor", "Merlin", "Ripley"]

# Remove and return the last item (identical to JS arr.pop())
last_player = lobby.pop()
print(last_player) # Output: "Ripley"
print(lobby)       # Output: ['Xena', 'Thor', 'Merlin']

# Remove the first matching item by value (no direct single-call JS equivalent)
lobby.remove("Thor")
print(lobby)       # Output: ['Xena', 'Merlin']
```
JavaScript has something similar with `fruits.slice(1, 3);`, but Python's slicing syntax is built directly into the language.

:::