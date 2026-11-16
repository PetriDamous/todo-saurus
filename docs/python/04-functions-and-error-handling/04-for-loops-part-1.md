---
title: for Loops, Iterables & Indentation-Scoped Execution
sidebar_label: for Loops, Iterables & Indentation-Scoped Execution
sidebar_position: 4
---

# Python Notes: `for` Loops, Iterables & Indentation-Scoped Execution Part 1

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 3 — Functions & Data Structures (Iterating Over Collections)
- **Lesson Topic:** `for...in` Loops, Iterable Sequences, Naming Conventions (`plural` / `singular`) & Post-Loop Execution
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~0yz7](https://scrimba.com/learn-python-c03/~0yz7)

:::

---

## 2. Concept Breakdown

:::note

This lesson introduces Python's `for` loop, which iterates directly over the elements of any **iterable** collection (such as a `list`, `str`, or `tuple`) without needing manual index counters or `.length` bounds checks:

- **How `for item in collection:` Works:** On each pass of the loop, Python pulls the next element from the iterable, binds it to the inline loop variable (`guest`, `nominee`), and executes the indented body. Once the collection runs out of items, the loop terminates automatically and execution continues at the next unindented line.
- **No Index Boilerplate:** Unlike traditional C-style `for (let i = 0; i < arr.length; i++)` loops, Python's `for` loop behaves like JavaScript's `for...of` loop—giving you the actual element value directly.
- **Plural / Singular Naming Convention:** Name the collection as a plural noun (`guests`, `nominees`) and the loop variable as its singular counterpart (`guest`, `nominee`). This makes every line inside the loop self-documenting (`for nominee in nominees:`).
- **Indentation Controls Loop Boundaries:** Any line indented inside the `for` block runs once *per item*. The first unindented line after the loop runs *once* after all iterations finish.

:::

---

## 3. JS vs. Python Mental Bridge

:::info

### Iterating Over an Array / List

```javascript
// JavaScript (ES6+) - for...of loop (closest equivalent)
const guests = ["Marcus", "Lena", "Sarah", "Priya"];

for (const guest of guests) {
  console.log(`Welcome, ${guest}!`);
}

console.log("That's everyone!");
```

```python
# Python 3 - for...in loop
guests = ["Marcus", "Lena", "Sarah", "Priya"]

for guest in guests:
    print(f"Welcome, {guest}!")

print("That's everyone!")
```

### Critical Warning: Python `for...in` vs. JavaScript `for...in`

| Feature | JavaScript `for...in` | JavaScript `for...of` | Python `for...in` |
| :--- | :--- | :--- | :--- |
| **What it yields on an Array/List** | **Index keys as strings** (`"0"`, `"1"`, `"2"`) | **Actual element values** (`"Marcus"`, `"Lena"`) | **Actual element values** (`"Marcus"`, `"Lena"`) |
| **Syntax** | `for (const i in arr)` | `for (const item of arr)` | `for item in items:` |
| **Built-in Index + Value** | `arr.forEach((v, i) => ...)` | `for (const [i, v] of arr.entries())` | `for i, v in enumerate(items):` |

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code (Guest Welcome)

```python
guests = ["Marcus", "Lena", "Sarah", "Priya"]

# 'guest' is created automatically by the loop header and reassigned on every pass
for guest in guests:
    print(f"Welcome, {guest}!")

# Unindented: runs once AFTER the loop finishes all 4 iterations
print("That's everyone!")
```

**Iteration-by-Iteration Trace & Output:**
```text
Pass 1: guest = "Marcus" -> prints "Welcome, Marcus!"
Pass 2: guest = "Lena"   -> prints "Welcome, Lena!"
Pass 3: guest = "Sarah"  -> prints "Welcome, Sarah!"
Pass 4: guest = "Priya"  -> prints "Welcome, Priya!"
Loop ends (no items remaining) -> unindented line runs -> prints "That's everyone!"
```

**Terminal Output:**
```text
Welcome, Marcus!
Welcome, Lena!
Welcome, Sarah!
Welcome, Priya!
That's everyone!
```

---

### Part B: The Challenge Code & Solution (Award Night!)

```python
# Dynamic collection: loop adapts automatically whether this list has 1 item or 1,000
nominees = ["PixelPal", "TaskTanic", "SnackMap", "MoodTunes"]

# 1. Iterate over each nominee and print the formatted announcement
for nominee in nominees:
    print(f"Nominated for Best New App: {nominee}")

# 2. Unindented closing statement executes once after all nominees are announced
print("And those are your nominees!")
```

**Terminal Output:**
```text
Nominated for Best New App: PixelPal
Nominated for Best New App: TaskTanic
Nominated for Best New App: SnackMap
Nominated for Best New App: MoodTunes
And those are your nominees!
```

:::tip

**Why Dynamic Iteration Matters:**
Because `for nominee in nominees:` does not hardcode indices like `nominees[0]` through `nominees[3]`, adding `"CodePulse"` or removing `"SnackMap"` requires zero changes to the loop logic—it always processes every element cleanly.

:::

---

## 5. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Accidentally Indenting Post-Loop Code Inside the Loop
In JavaScript, curly braces `{}` visually lock where a loop ends. In Python, accidentally indenting a closing statement places it inside the loop body, causing it to execute on every single iteration:

```python
nominees = ["PixelPal", "TaskTanic", "SnackMap"]

# BUG: Closing line is indented 4 spaces, so it runs inside the loop!
for nominee in nominees:
    print(f"Nominated for Best New App: {nominee}")
    print("And those are your nominees!")

# Output (Broken):
# Nominated for Best New App: PixelPal
# And those are your nominees!
# Nominated for Best New App: TaskTanic
# And those are your nominees!
# Nominated for Best New App: SnackMap
# And those are your nominees!
```

```python
# CORRECT FIX: Unindent the closing print() back to column 0
for nominee in nominees:
    print(f"Nominated for Best New App: {nominee}")

print("And those are your nominees!")
```

### 2. Mutating a List While Iterating Over It
Adding or removing items from the exact list you are currently looping over shifts internal indices and causes Python to skip elements or loop infinitely:

```python
numbers = [1, 2, 3, 4]

# BUG: Removing items in-place during iteration skips elements!
for num in numbers:
    if num % 2 != 0:
        numbers.remove(num)

print(numbers)
# Output: [2, 4] (Works by luck here, but fails on consecutive matches!)

# Demonstration of the skip bug on consecutive odd numbers:
bad_nums = [1, 3, 4]
for num in bad_nums:
    if num % 2 != 0:
        bad_nums.remove(num)  # Removing 1 shifts 3 to index 0; loop moves to index 1 ('4') and skips 3!

print(bad_nums)
# Output: [3, 4]  <-- 3 was skipped!
```

```python
# CORRECT FIX: Build a new list (or iterate over a shallow copy bad_nums[:])
bad_nums = [1, 3, 4]
evens = []

for num in bad_nums:
    if num % 2 == 0:
        evens.append(num)

print(evens)
# Output: [4]
```

:::

:::warning

### 3. Reassigning the Loop Variable Does NOT Mutate the List
Assigning a new value to `nominee` inside the loop only rebinds the temporary local variable—it does not update the element stored inside `nominees`:

```python
nominees = ["pixelpal", "tasktanic"]

for nominee in nominees:
    nominee = nominee.upper()  # Rebinds local variable 'nominee'; list stays unchanged!

print(nominees)
# Output: ['pixelpal', 'tasktanic']
```

```python
# CORRECT FIX: Append transformed values into a new list (or use a list comprehension)
nominees = ["pixelpal", "tasktanic"]
upper_nominees = []

for nominee in nominees:
    upper_nominees.append(nominee.upper())

print(upper_nominees)
# Output: ['PIXELPAL', 'TASKTANIC']
```

:::

---

## 6. Edge Cases to Watch For

:::note

### 1. Iterating Over an Empty List (`[]`)
If `nominees = []`, Python safely skips the loop body (`0` iterations) without throwing an error and immediately runs the unindented code after the loop:

```python
nominees = []

for nominee in nominees:
    print(f"Nominated for Best New App: {nominee}")

print("And those are your nominees!")
# Output: And those are your nominees!
```

### 2. Loop Variable Leaking After Loop Completion
Unlike JavaScript's `for (const x of arr)` (where `x` is block-scoped and destroyed when the loop ends), Python's loop variable remains in the enclosing scope holding the **last** item processed:

```python
nominees = ["PixelPal", "TaskTanic", "MoodTunes"]

for nominee in nominees:
    pass

# 'nominee' still exists after the loop!
print(nominee)
# Output: MoodTunes
```

### 3. Iterating Over Other Built-in Iterables (Strings & Tuples)
Any iterable works in a `for` loop—not just lists:

```python
# Iterating over a string yields one character at a time
for char in "App":
    print(char)
# Output:
# A
# p
# p

# Iterating over a list of tuples with inline unpacking
scores = [("PixelPal", 95), ("MoodTunes", 88)]
for app, score in scores:
    print(f"{app}: {score} pts")
# Output:
# PixelPal: 95 pts
# MoodTunes: 88 pts
```

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Getting Both Index and Value with `enumerate()`
When you need a numbered list (like `1. PixelPal`, `2. TaskTanic`), wrap the iterable in `enumerate(iterable, start=1)` instead of manually tracking a counter variable:

```python
nominees = ["PixelPal", "TaskTanic", "SnackMap", "MoodTunes"]

# JavaScript equivalent: nominees.forEach((nominee, idx) => console.log(`${idx + 1}. ${nominee}`))
for rank, nominee in enumerate(nominees, start=1):
    print(f"{rank}. {nominee}")

# Output:
# 1. PixelPal
# 2. TaskTanic
# 3. SnackMap
# 4. MoodTunes
```

### Pattern 2: Accumulator Pattern (Filtering or Aggregating Inside a Loop)
Initialize an empty list or counter before the loop, update it inside the loop body, and return or print the final result after the loop completes:

```python
def filter_short_names(names, max_length):
    short_names = []
    for name in names:
        if len(name) <= max_length:
            short_names.append(name)
    return short_names

nominees = ["PixelPal", "TaskTanic", "SnackMap", "MoodTunes"]
print(filter_short_names(nominees, 8))
# Output: ['PixelPal', 'SnackMap']
```

:::