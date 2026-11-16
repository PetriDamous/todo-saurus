---
title: Unpacking Tuples Inside `for` Loops & Conditional Branching
sidebar_label: Unpacking Tuples Inside `for` Loops & Conditional Branching
sidebar_position: 5
---

# Python Notes: Unpacking Tuples Inside `for` Loops & Conditional Branching

## 1. Course Module & Lesson Title

:::info

- **Module:** Module 3 — Functions & Data Structures (Iterating Over Structured Records)
- **Lesson Topic:** Iterating Over a List of Tuples, Two-Step vs. Inline Tuple Unpacking & Conditional Loop Logic (`if / else`)
- **Scrimba URL:** [https://scrimba.com/learn-python-c03/~06tm](https://scrimba.com/learn-python-c03/~06tm)

:::

---

## 2. Concept Breakdown

:::note

This lesson combines three core Python patterns—**lists of tuples**, **tuple unpacking**, and **`for` loops with `if / else` branching**—to process structured records cleanly:

- **Lists of Tuples as Lightweight Records:** Storing fixed-schema rows inside a list—such as `[("The Wailers", "reggae", 45), ("Daft Punk", "electronic", 90)]`—is a standard Python pattern for tabular or database-like records where each row has an immutable structure (`(band, genre, minutes)`), while the outer list remains dynamic.
- **Two Ways to Unpack Inside a `for` Loop:**
  1. **Two-Step Unpacking (Inside the Loop Body):** Capture the whole tuple in a single loop variable (`for band in lineup:`) and unpack it on the first indented line (`name, genre, minutes = band`). Useful when you also need the raw tuple object (`band`) intact.
  2. **Inline Header Unpacking (Pythonic Shorthand):** Unpack the tuple directly inside the `for` header (`for band, genre, minutes in lineup:`), eliminating the intermediate variable.
- **Per-Iteration Decision Making (`if / else` Inside `for`):** Nesting an `if / else` block inside a `for` loop (indented 4 spaces for the loop, 8 spaces for the conditional bodies) lets you evaluate business rules on every single record dynamically.

:::

---

## 3. JS vs. Python Mental Bridge

:::info

### Unpacking Structured Rows in Loops

```javascript
// JavaScript (ES6+) - Array of fixed-length arrays + inline array destructuring
const lineup = [
  ["The Wailers", "reggae", 45],
  ["Daft Punk", "electronic", 90],
  ["Adele", "pop", 60],
  ["Metallica", "metal", 100],
];

for (const [band, genre, minutes] of lineup) {
  if (minutes >= 90) {
    console.log(`${band} (${genre}) plays a long set: ${minutes} minutes`);
  } else {
    console.log(`${band} (${genre}) plays ${minutes} minutes`);
  }
}
```

```python
# Python 3 - List of immutable tuples + inline tuple unpacking
lineup = [
    ("The Wailers", "reggae", 45),
    ("Daft Punk", "electronic", 90),
    ("Adele", "pop", 60),
    ("Metallica", "metal", 100),
]

for band, genre, minutes in lineup:
    if minutes >= 90:
        print(f"{band} ({genre}) plays a long set: {minutes} minutes")
    else:
        print(f"{band} ({genre}) plays {minutes} minutes")
```

### Key Syntax Differences for JS Developers

| Concept | JavaScript (ES6+) | Python 3 | Key Difference |
| :--- | :--- | :--- | :--- |
| **Inline Destructuring / Unpacking** | `for (const [a, b, c] of items)` | `for a, b, c in items:` | Python requires no square brackets or parentheses around the unpacked target variables. |
| **Two-Step Unpacking** | `const [a, b] = item;` | `a, b = item` | Right-hand sequence is unpacked positionally into comma-separated variables on the left. |
| **Nested Block Depth** | Controlled by `{ ... }` braces | 4 spaces (`for`) -> 8 spaces (`if`/`else`) | Each nested colon (`:`) adds +4 spaces of indentation. |
| **Record Immutability** | Inner arrays are mutable unless frozen | Inner `tuple` items are immutable | Attempting `lineup[0][2] = 60` raises a `TypeError`. |

:::

---

## 4. Code Walkthrough

### Part A: Instructor Demos & Scratchpad Code (Potluck Guests)

```python
guests = [("Marcus", "lasagna"), ("Lena", "salad"), ("Sarah", "brownies")]

# Two-step unpacking:
# 1. 'guest' receives one 2-element tuple per iteration (e.g., ("Marcus", "lasagna"))
# 2. 'name, dish = guest' unpacks that tuple into two individual string variables
for guest in guests:
    name, dish = guest
    print(f"{name} is bringing {dish}")
```

**Iteration-by-Iteration Trace & Output:**
```text
Pass 1: guest = ("Marcus", "lasagna") -> name = "Marcus", dish = "lasagna" -> prints "Marcus is bringing lasagna"
Pass 2: guest = ("Lena", "salad")     -> name = "Lena", dish = "salad"     -> prints "Lena is bringing salad"
Pass 3: guest = ("Sarah", "brownies") -> name = "Sarah", dish = "brownies" -> prints "Sarah is bringing brownies"
```

**Alternative Inline Header Unpacking (Identical Output):**
```python
guests = [("Marcus", "lasagna"), ("Lena", "salad"), ("Sarah", "brownies")]

for name, dish in guests:
    print(f"{name} is bringing {dish}")
```

---

### Part B: The Challenge Code & Solution (Festival Lineup)

```python
lineup = [
    ("The Wailers", "reggae", 45),
    ("Daft Punk", "electronic", 90),
    ("Adele", "pop", 60),
    ("Metallica", "metal", 100),
]

# Two-step unpacking approach (your solution):
for band in lineup:
    name, genre, minutes = band
    if minutes >= 90:
        print(f"{name} ({genre}) plays a long set: {minutes} minutes")
    else:
        print(f"{name} ({genre}) plays {minutes} minutes")
```

**Inline Header Unpacking Alternative (Cleaner Variable Naming):**
```python
for band, genre, minutes in lineup:
    if minutes >= 90:
        print(f"{band} ({genre}) plays a long set: {minutes} minutes")
    else:
        print(f"{band} ({genre}) plays {minutes} minutes")
```

**Terminal Output (Both Versions):**
```text
The Wailers (reggae) plays 45 minutes
Daft Punk (electronic) plays a long set: 90 minutes
Adele (pop) plays 60 minutes
Metallica (metal) plays a long set: 100 minutes
```

:::tip

**Notice Why `>= 90` Is Required Instead of `> 90`:**
The prompt specifies *"any act playing 90 minutes or more."* Daft Punk plays exactly `90` minutes—using `minutes > 90` would fail the boundary condition and print the normal message for Daft Punk instead of the `"long set"` message.

:::

---

## 5. Common Pitfalls & Gotchas for JS Devs

:::danger

### 1. Variable Count Mismatch During Tuple Unpacking (`ValueError`)
In JavaScript, `const [a, b] = ["x", "y", "z"]` silently drops `"z"`. In Python, if even **one** tuple inside the list has a different number of elements than your unpacking target, Python crashes at runtime on that iteration:

```python
lineup = [
    ("The Wailers", "reggae", 45),
    ("Mystery Headliner", "rock"),  # Only 2 items instead of 3!
]

for band, genre, minutes in lineup:
    print(f"{band} ({genre}) - {minutes}m")

# Pass 1 Output: The Wailers (reggae) - 45m
# Pass 2 Raises -> ValueError: not enough values to unpack (expected 3, got 2)
```

```python
# Similarly, having TOO MANY items in a tuple crashes with:
bad_lineup = [("Metallica", "metal", 100, "Main Stage")]
for band, genre, minutes in bad_lineup:
    print(band)
# Raises -> ValueError: too many values to unpack (expected 3)
```

### 2. Reusing the Outer Tuple Variable Name When Unpacking
In your challenge code, naming the tuple `band` and unpacking `name, genre, minutes = band` worked cleanly because `name` was distinct from `band`. If you accidentally unpack into the **same** variable name (`band, genre, minutes = band`), it still works on that line, *but* `band` is overwritten from a `tuple` to a `str`, which breaks any subsequent line in the loop expecting `band` to still be the full tuple:

```python
lineup = [("The Wailers", "reggae", 45)]

for band in lineup:
    band, genre, minutes = band  # Overwrites 'band' from tuple to str!
    print(band)                  # Output: The Wailers
    # print(band[2])             # Bug! Now indexes string index 2 ('e') instead of tuple index 2 (45)!
```

:::

:::warning

### 3. Attempting to Mutate a Tuple Field Inside the Loop (`TypeError`)
Because each item in `lineup` is a `tuple` (not a `list`), trying to add encore minutes directly to `act[2]` crashes:

```python
lineup = [("The Wailers", "reggae", 45)]

for act in lineup:
    # INCORRECT:
    # act[2] += 15
    # Raises -> TypeError: 'tuple' object does not support item assignment
    pass

# CORRECT FIX: Build a new list of updated tuples
extended_lineup = []
for band, genre, minutes in lineup:
    extended_lineup.append((band, genre, minutes + 15))

print(extended_lineup)
# Output: [('The Wailers', 'reggae', 60)]
```

### 4. Off-by-One Indentation on `else:`
`else:` must align **vertically with its matching `if`** (8 spaces in, inside the 4-space `for` block). Aligning `else:` with `for` (4 spaces in) creates a completely different Python construct (`for...else`, which only runs if the loop finishes without hitting `break`):

```python
# BUG: 'else:' is aligned with 'for' instead of 'if'!
for band, genre, minutes in lineup:
    if minutes >= 90:
        print(f"{band} plays a long set")
else:
    # Runs ONCE after the entire loop ends—and 'band' holds the last item ("Metallica")!
    print(f"{band} plays {minutes} minutes")
```

:::

---

## 6. Edge Cases to Watch For

:::note

### 1. Variable-Length Tuples with Star Unpacking (`*`)
If some tuples in a collection carry optional trailing metadata (like a stage name), Python's star operator `*` captures remaining items into a `list` (just like JavaScript's rest operator `...rest`):

```python
lineup = [
    ("The Wailers", "reggae", 45),
    ("Metallica", "metal", 100, "Main Stage", "Pyrotechnics"),
]

# JavaScript equivalent: const [band, genre, minutes, ...extras] = act;
for band, genre, minutes, *extras in lineup:
    print(f"{band}: {minutes}m | Extras: {extras}")

# Output:
# The Wailers: 45m | Extras: []
# Metallica: 100m | Extras: ['Main Stage', 'Pyrotechnics']
```

### 2. Ignoring Unused Tuple Fields with `_`
If you only need `band` and `minutes` and don't care about `genre`, use `_` as the standard Python throwaway variable so linters don't flag an unused variable:

```python
lineup = [
    ("The Wailers", "reggae", 45),
    ("Daft Punk", "electronic", 90),
]

for band, _, minutes in lineup:
    print(f"{band}: {minutes} mins")

# Output:
# The Wailers: 45 mins
# Daft Punk: 90 mins
```

:::

---

## 7. Practical Patterns & Reusable Recipes

:::tip

### Pattern 1: Filtering & Transforming Structured Tuples into Summary Lists
Combine tuple unpacking with an accumulator list to extract specific records matching a condition:

```python
def get_headliners(lineup, min_minutes=90):
    headliners = []
    for band, genre, minutes in lineup:
        if minutes >= min_minutes:
            headliners.append(f"{band} ({genre})")
    return headliners

lineup = [
    ("The Wailers", "reggae", 45),
    ("Daft Punk", "electronic", 90),
    ("Adele", "pop", 60),
    ("Metallica", "metal", 100),
]

print(get_headliners(lineup))
# Output: ['Daft Punk (electronic)', 'Metallica (metal)']
```

### Pattern 2: Pairing `enumerate()` with Tuple Unpacking (Nested Unpacking)
When combining `enumerate()` with a list of tuples, wrap the unpacked tuple variables in parentheses `()` inside the `for` header:

```python
lineup = [
    ("The Wailers", "reggae", 45),
    ("Daft Punk", "electronic", 90),
]

for slot, (band, genre, minutes) in enumerate(lineup, start=1):
    print(f"Slot #{slot}: {band} [{genre}] - {minutes} min")

# Output:
# Slot #1: The Wailers [reggae] - 45 min
# Slot #2: Daft Punk [electronic] - 90 min
```

:::