---
title: Equality & Comparison Operators (==, !=, >, <, >=, <=)
sidebar_label: Equality & Comparison Operators
sidebar_position: 1
---

# Python Logic and Loops: Equality & Comparison Operators

## Part 1: Equality Operators (`==` and `!=`)

**Lesson Goal:** Learn how Python compares values, understand Boolean results (`True` and `False`), use equality operators with user input, and understand why comparisons are case-sensitive. This is the foundation for all conditional logic that you'll learn later (`if`, `elif`, `else`). [[scrimba.com]](https://scrimba.com)

### Why This Lesson Matters

Up until now we've mostly been:
- Storing data
- Displaying data
- Transforming data

Now we're entering: **Decision Making**

Programming becomes interesting when a program can ask:
- Are these values the same?
- Are they different?
- Did the user enter the correct password?
- Did the user enter a valid promo code?

To answer these questions we need comparison operators.

### The Equality Operator (`==`)

#### Purpose
Checks whether two values are equal.

```python
password = "SECRET"
user_password = "SECRET"
print(password == user_password)
# Output: True
```
Both values match.

#### Mental Model
Think of `==` as asking: *Do these two values contain the same thing?*

```text
"SECRET"  ==  "SECRET"
   │             │
   └────Same─────┘
Result: True
```

#### JavaScript Comparison
- **Python:** `password == user_password`
- **JavaScript:** `password === userPassword`

As a JavaScript developer, you should mentally translate `==` to `===` (not `==`), because Python's equality operator behaves much more predictably:
- **JavaScript:** `5 == "5"` → `true` (because JavaScript performs type coercion).
- **Python:** `5 == "5"` → `False` (Python doesn't automatically pretend strings and numbers are the same).

#### What Is Being Compared?
```python
promo_code = "FLASH50"
user_promo_code = "FLASH50"
print(promo_code == user_promo_code)
# Result: True

# If user_promo_code = "EXPIRED":
# Result: False (because the values differ)
```

### Boolean Values

The result of a comparison is a Boolean. Python has two Boolean values: `True` and `False` (notice the capitalization).

```python
print(type(True))
# JavaScript equivalent: typeof true -> "boolean"
```

#### Memory Diagram
```text
promo_code ──▶ "FLASH50"
user_promo_code ──▶ "FLASH50"

Comparison: promo_code == user_promo_code
Python checks: "FLASH50" == "FLASH50"
Result: True
```

### The Not Equal Operator (`!=`)

#### Purpose
Checks whether two values are different.

```python
promo_code = "FLASH50"
user_promo_code = "SAVE10"
print(promo_code != user_promo_code)
# Output: True (They are different)
```

#### Mental Model
Read `!=` as: **NOT equal to**.

```text
FLASH50 != SAVE10  ──▶ Different ──▶ Result: True
```

#### Relationship Between `==` And `!=`

| Comparison | Result |
| :--- | :--- |
| `"A" == "A"` | `True` |
| `"A" == "B"` | `False` |
| `"A" != "A"` | `False` |
| `"A" != "B"` | `True` |

### Understanding User Input

```python
promo_code = "FLASH50"
user_promo_code = input("Please enter your promo code: ")

print(promo_code == user_promo_code)
print(promo_code != user_promo_code)
```

Suppose user enters `FLASH50`:
- `promo_code == user_promo_code` → `"FLASH50" == "FLASH50"` → `True`
- `promo_code != user_promo_code` → `"FLASH50" != "FLASH50"` → `False`

### Case Sensitivity

The instructor specifically points out that `FLASH50` and `flash50` produce different results:

```python
promo_code = "FLASH50"
user_promo_code = "flash50"
print(promo_code == user_promo_code)
# Output: False (Because "F" != "f")
```

#### Common Solution: Convert Both Values to Lowercase
```python
promo_code = "FLASH50"
user_promo_code = input("Promo code: ").lower()

print(promo_code.lower() == user_promo_code)
# Now FLASH50, flash50, Flash50, and FlAsH50 all match!
```

**JavaScript Comparison:**
```javascript
promoCode.toLowerCase() === userPromoCode.toLowerCase()
```

### Equality Common Mistakes & Things The Course Didn't Cover

1. **Using Assignment Instead Of Comparison:** `promo_code = user_promo_code` assigns; it does NOT compare. Use `==`.
2. **Forgetting Case Sensitivity:** `"FLASH50" == "flash50"` evaluates to `False`.
3. **Comparing Different Types:** `5 == "5"` evaluates to `False`.

---

## Part 2: Comparison Operators (`>`, `<`, `>=`, `<=`)

**Lesson Goal:** Learn how to compare values, understand how comparison operations produce Boolean values (`True` or `False`), and use comparisons to answer business questions inside your programs. This lesson builds directly on `==` and `!=` and brings us much closer to writing `if` statements. [[scrimba.com]](https://scrimba.com)

### What Is A Comparison Operator?

A comparison operator compares two values and returns `True` or `False`:

```python
age = 20
print(age >= 18)  # Result: True

is_adult = age >= 18
# 20 >= 18 -> True -> is_adult = True
```

**JavaScript Comparison:** `age >= 18` behaves identically in Python and JavaScript.

### Comparison Operator Cheat Sheet

| Operator | Meaning | Example | Result |
| :--- | :--- | :--- | :--- |
| `>` | Greater than | `10 > 5` | `True` |
| `<` | Less than | `5 < 10` | `True` |
| `>=` | Greater than or equal to | `18 >= 18` | `True` |
| `<=` | Less than or equal to | `0 <= 0` | `True` |
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 10` | `True` |

### Using Comparisons Inside F-Strings

```python
age = 20
print(f"Is Old Enough: {age >= 18}")
# Step 1: age >= 18 -> True
# Step 2: Inserts True into the string
# Output: Is Old Enough: True
```
Because `f"{expression}"` evaluates whatever is inside the braces, you can embed any comparison directly (`age >= 18`, `cart_total < 50`, `tickets_left <= 0`).

### Challenge Breakdown

Given:
```python
unread_messages = 0
age = 25
cart_total = 45
tickets_left = 8
```

1. **Unread Messages (`unread_messages > 0`):** `0 > 0` → `False` (*Has unread messages: False*)
2. **Renting A Car (`age >= 25`):** `25 >= 25` → `True` (Equal counts! *Old enough to rent a car: True*)
3. **Free Shipping Threshold (`cart_total < 50`):** `45 < 50` → `True` (*Under the $50 free-shipping minimum: True*)
4. **Sold Out Check (`tickets_left <= 0`):** `8 <= 0` → `False` (*Sold out: False*)

### String Comparisons

Strings can also be compared based on alphabetical (lexicographical) ordering:

```python
print("banana" < "cherry")
# Result: True (Alphabetically, "banana" comes before "cherry")
# JS equivalent: console.log("banana" < "cherry"); -> true
```

### Real-World Examples
- **Message Notifications:** `unread_messages > 0`
- **Age Verification:** `age >= 18`
- **Free Shipping:** `cart_total >= 50`
- **Ticket Sales:** `tickets_left <= 0`

### Common Beginner Mistakes
- **Confusing `>` and `>=`:** `18 > 18` is `False`; `18 >= 18` is `True`.
- **Confusing `<` and `<=`:** `0 < 0` is `False`; `0 <= 0` is `True`.
- **Thinking comparisons produce text:** They produce Booleans (`True` / `False`), not strings (`"True"` / `"False"`).

### JavaScript Translation Guide

| Python | JavaScript Equivalent |
| :--- | :--- |
| `==` | `===` |
| `!=` | `!==` |
| `>` / `<` | `>` / `<` |
| `>=` / `<=` | `>=` / `<=` |
| `True` / `False` | `true` / `false` |
| `bool` | `boolean` |
| `.lower()` | `.toLowerCase()` |

### Key Takeaways
1. `==` checks if two values are equal; `!=` checks if two values are different. [\[scrimba.com\]](https://scrimba.com)
2. Comparisons return Boolean values (`True` or `False`). [\[scrimba.com\]](https://scrimba.com)
3. Python comparisons are case-sensitive (`"FLASH50"` and `"flash50"` are not equal). [\[scrimba.com\]](https://scrimba.com)
4. Python's `==` behaves more like JavaScript's `===`.
5. `>`, `<`, `>=`, and `<=` compare numbers and can also compare strings alphabetically. [\[scrimba.com\]](https://scrimba.com)
6. Comparisons can be stored in variables or placed directly inside f-strings. [\[scrimba.com\]](https://scrimba.com)
7. Comparisons are the foundation of conditional logic (`if`, `elif`, `else`).
4. **Comparisons Return Values:** You can store them in variables (`is_correct = (promo_code == user_promo_code)`) or print them directly, and they become conditions later (`if promo_code == user_promo_code:`).