---
title: The list() Function, .split() & sorted()
sidebar_label: list(), .split() & sorted()
sidebar_position: 3
---

# Python Logic and Loops: The `list()` Function, `.split()` & `sorted()`

:::info

**Lesson Goal:** Learn how to convert strings into lists, manipulate individual characters, use the `sorted()` function, and understand why this is useful for solving problems like detecting anagrams. This lesson is also your first real introduction to treating strings as sequences of characters rather than just blocks of text. [[scrimba.com]](https://scrimba.com)

:::

---

## Section Overview

The instructor explains that to scramble a word, we need to:
1. Break the word into individual letters
2. Rearrange the letters
3. Put the letters back together

Python cannot easily rearrange letters directly inside a string, so we first convert the string into a list. [[scrimba.com]](https://scrimba.com)

This introduces:
- String indexing
- Character access
- The `list()` function
- The `sorted()` function
- Anagram detection

---

## Strings As Sequences

:::note

Before we can understand `list()`, we need to understand something important about strings. A string is not just a block of text—Python treats a string as an ordered sequence of characters.

:::

```python
word = "listen"
```

Visual representation:

```text
Character:   l   i   s   t   e   n
Index:       0   1   2   3   4   5
```

This means Python knows where every character is located.

### Accessing Characters By Index

```python
print("listen"[3])
# Output: t
```

The instructor demonstrates this exact concept using the word `"listen"` and accessing the letter `t` at index `3`. [[scrimba.com]](https://scrimba.com)

### JavaScript Comparison
- **JavaScript:** `console.log("listen"[3]);` -> Output: `t`
- **Python:** `print("listen"[3])` -> Output: `t`

### Negative Indexing on Strings

:::tip

```python
word = "dog"
print(word[-1])
# Output: g
```
Python lets you count backwards (`0` = first, `-1` = last, `-2` = second last). This works for both strings and lists.

:::

### Mental Model

:::info

Think of a string as a row of numbered boxes:

```text
┌───┬───┬───┬───┬───┬───┐
│ l │ i │ s │ t │ e │ n │
└───┴───┴───┴───┴───┴───┘
  0   1   2   3   4   5
```

When you do `word[3]`, Python goes to box `3` and returns `t`.

:::

### Strings Are Difficult To Rearrange

---

## The `list()` Function

### Purpose
The `list()` function converts an iterable (something you can loop through) into a list. The course compares it to `int()` and `float()`, which also convert data from one form to another: [[scrimba.com]](https://scrimba.com)

- String → Integer: `int("5")` → `5`
- String → Float: `float("5.5")` → `5.5`
- String → List: `list("listen")` → `['l', 'i', 's', 't', 'e', 'n']`

### What `list()` Actually Does

```python
word = "dog"
letters = list(word)
print(letters)
# Output: ['d', 'o', 'g']
```

### Visual Representation

```text
Before: "dog"
Memory model:
┌─────────┐
│  "dog"  │
└─────────┘
One string.

After: list("dog")
Memory model:
┌───┬───┬───┐
│ d │ o │ g │
└───┴───┴───┘
A list containing three separate elements.
```

### JavaScript Comparison

:::info

- **Python:** `list("dog")`
- **JavaScript equivalent:** `"dog".split("")` or `Array.from("dog")` -> `["d", "o", "g"]`

:::

---

## `list()` vs `.split()`

This is one of the most important comparisons in this section:
- **`list`** = a data type (container)
- **`split()`** = a string method that breaks a string at a separator and returns a list

### Side-by-Side Comparison

#### `list()` — Break into individual characters
```python
list("dog")
# Output: ['d', 'o', 'g']

list("big dog")
# Output: ['b', 'i', 'g', ' ', 'd', 'o', 'g']  <-- Space is included!
```

#### `.split()` — Break at a separator
```python
"dog".split()
# Output: ['dog']  <-- No spaces found, so 1 word = 1 list item

"big dog".split()
# Output: ['big', 'dog']  <-- Splits on whitespace into words

"dog,cat,bird".split(",")
# Output: ['dog', 'cat', 'bird']  <-- Splits at custom comma separator
```

### Real-World Analogy

:::info

Imagine `"dog,cat,bird"` is a whole pizza. `split()` is the pizza cutter. After cutting, you have individual slices—the result of using the cutter is a `list`.

:::

### Quick Rule

:::tip

- Want `['d', 'o', 'g']` (characters)? Use `list("dog")` (≈ JS `"dog".split("")`).
- Want `['dog', 'cat', 'bird']` (words)? Use `"dog cat bird".split()` (≈ JS `"dog cat bird".split(" ")`).

:::

---

## The `sorted()` Function

### Purpose
Sort items alphabetically: [[scrimba.com]](https://scrimba.com)

```python
letters = list("listen")
print(sorted(letters))
# Before: ['l', 'i', 's', 't', 'e', 'n']
# After:  ['e', 'i', 'l', 'n', 's', 't']
```

### Important Discovery: `sorted()` Does NOT Mutate

:::warning

Many JavaScript developers assume `sorted(letters)` changes `letters` in place like `letters.sort()` in JS. **It doesn't.**

```python
letters = ['l', 'i', 's', 't', 'e', 'n']
sorted_letters = sorted(letters)

print(letters)         # ['l', 'i', 's', 't', 'e', 'n'] (Still unchanged!)
print(sorted_letters)  # ['e', 'i', 'l', 'n', 's', 't'] (New sorted list)
```

:::

:::note
*(Note: Python lists also have an in-place `.sort()` method—`animals.sort()`—which mutates the original list directly like JavaScript's `.sort()`, whereas `sorted(animals)` is a built-in function that returns a new list).*
:::


### Why `sorted()` and `len()` Are Functions
Coming from JavaScript, your instinct may be `animals.sort()` or `animals.length`. Python frequently prefers built-in functions (`sorted(animals)`, `len(animals)`, `type(val)`) that operate on values and return new values rather than mutating existing ones.

---

## Anagrams & Challenge Breakdown

### Definition
An **anagram** is two words made using the exact same letters in a different order (e.g., `listen` → `silent`, `evil` → `vile`, `night` → `thing`).

### Why Sorting Works
```python
first_word = list("listen")
second_word = list("silent")

print(sorted(first_word))   # ['e', 'i', 'l', 'n', 's', 't']
print(sorted(second_word))  # ['e', 'i', 'l', 'n', 's', 't']
```
Because both sorted lists match, `listen` and `silent` are anagrams. [[scrimba.com]](https://scrimba.com)

### Challenge Breakdown
```python
earth_list = list(earth)
heart_list = list(heart)
print(sorted(earth_list))
print(sorted(heart_list))
# Output:
# ['a', 'e', 'h', 'r', 't']
# ['a', 'e', 'h', 'r', 't']
```
Match! Therefore `earth` and `heart` are anagrams (and `below` / `elbow` match too, while `night` and `tight` produce different sorted lists and are not anagrams). [[scrimba.com]](https://scrimba.com)

### JavaScript Equivalent Strategy

:::info

```javascript
const first = "listen";
const second = "silent";
const result = first.split("").sort().join("") === second.split("").sort().join("");
console.log(result); // true
```

:::

### Things The Course Didn't Cover: You Don't Actually Need `list()`

:::tip

Python can sort a string directly because strings are iterable:
```python
sorted("listen") == sorted("silent")  # Output: True
sorted("dog")                         # Output: ['d', 'g', 'o'] (returns a list!)
```
The course intentionally introduces `list()` first to teach list conversion and manipulation.

:::

---

## Common Beginner Mistakes & Key Takeaways

### Common Mistakes

:::warning

1. **Confusing `list()` with `split()`:** `list("dog")` → `['d', 'o', 'g']`, whereas `"dog".split()` → `['dog']`.
2. **Thinking `sorted()` changes the original list:** Always store or print the returned list (`new_list = sorted(letters)`).

:::

### Key Takeaways

:::tip

1. Strings are ordered sequences of characters. [\[scrimba.com\]](https://scrimba.com)
2. Individual characters can be accessed using indexes. [\[scrimba.com\]](https://scrimba.com)
3. `list()` converts a string into a list of individual characters. [\[scrimba.com\]](https://scrimba.com)
4. `list()` is a type conversion function similar to `int()` and `float()`. [\[scrimba.com\]](https://scrimba.com)
5. `split()` and `list()` solve different problems.
6. `sorted()` returns a new alphabetically sorted list. [\[scrimba.com\]](https://scrimba.com)
7. Sorting letters allows us to compare words and detect anagrams. [\[scrimba.com\]](https://scrimba.com)
8. A Python list is closest to a JavaScript array.
9. `list("dog")` is conceptually similar to JavaScript's `"dog".split("")`.
10. Understanding strings as sequences is the foundation for upcoming topics involving lists, loops, and text processing.
You can read characters from strings, but you cannot easily rearrange characters in strings. [[scrimba.com]](https://scrimba.com) That is why Python developers convert strings into lists (`['l', 'i', 's', 't', 'e', 'n']`) to sort, shuffle, and manipulate letters.

:::