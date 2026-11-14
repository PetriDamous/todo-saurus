---
title: Store Information with Variables
sidebar_label: Store Info with Variables
sidebar_position: 3
---

# Store Information with Variables

## Lesson Overview

This lesson expands on the concept of variables and focuses on their primary purpose in programming: storing information so it can be used, updated, and reused throughout a program. The lesson uses a future "Pay Up" app as motivation, where values such as meal cost, party size, and tip percentage will need to be stored and manipulated. [scrimba.com]

The major concepts introduced are:
- Variables
- Assignment
- Storing numeric values
- Retrieving stored values
- Reassigning variables
- Updating information in a program [scrimba.com]

---

## Why Variables Matter

Programs often need to remember information.

Examples:
- Meal total
- Tip percentage
- Number of people
- Age
- Score
- Username

Without variables, you would have to manually write these values everywhere in your code.
Variables allow Python to store a value under a name so you can reference it later. [scrimba.com]

---

## Variable Syntax

The lesson introduces this example:

```python
meal_total = 85
```

The structure is:

```python
variable_name = value
```

Breaking it down:

```python
meal_total = 85
```

| Part | Meaning |
| :--- | :--- |
| `meal_total` | Variable name |
| `=` | Assignment operator |
| `85` | Value being stored |

## Assignment Definition

Assignment is the process of storing a value inside a variable using the `=` operator. [scrimba.com]

Example:

```python
meal_total = 85
```

Read this as:

```text
Assign 85 to meal_total
```

Not:

```text
meal_total equals 85
```

In programming, the equals sign typically means:

```text
Store this value here
```


---

## Variables Store Values

After assigning a value:

```python
meal_total = 85
```

Python remembers it.
You can retrieve that value later:

```python
print(meal_total)
```

Output:

```text
85
```

Python looks up the value associated with the variable name and prints it. [scrimba.com]

## Variables Hold Information

Think of a variable like a labeled box.

```python
meal_total = 85
```

Mental model:

```text
meal_total
┌─────┐
│ 85  │
└─────┘
```

The variable name is the label.
The value is what is stored inside.

Whenever Python sees:

```python
meal_total
```

it opens the box and retrieves:

```text
85
```

---

## Updating a Variable

One major advantage of variables is that information can change.

Original:

```python
meal_total = 85
```

Later:

```python
meal_total = 120
```

Now the variable stores:

```text
120
```

instead of:

```text
85
```

The name remains the same.
Only the value changes. [scrimba.com]

## Why Updating Variables Is Useful

Imagine a restaurant bill changes.
Instead of hunting through your program and changing every occurrence of:

```text
85
```

you update one location:

```python
meal_total = 120
```

Every part of the program using:

```python
meal_total
```

automatically receives the new value.
This is one of the biggest benefits of variables.

---

## Challenge: Restaurant Party Size

The challenge asked students to:
1. Create a variable called: `my_party`
2. Store how many people attended a restaurant.
3. Print the value.
4. Update the value.
5. Print it again. [scrimba.com]

### Example Solution

Your solution:

```python
my_party = 5
print(my_party)

my_party = 10
print(my_party)
```

Output:

```text
5
10
```

---

## Variable Reassignment

This lesson introduces an extremely important concept:

**Reassignment**

Variables are not permanent.
You can give them a new value later.

Example:

```python
my_party = 5
```

Then:

```python
my_party = 10
```

Now the variable contains:

```text
10
```

The old value is no longer what the variable stores. [scrimba.com]

## Visualizing Reassignment

Initially:

```python
my_party = 5
```

```text
my_party
↓
5
```

Later:

```python
my_party = 10
```

```text
my_party
↓
10
```

Python updates what the variable points to.
The old value is replaced.

## A Common Beginner Misunderstanding

Consider:

```python
my_party = 5
my_party = 10
```

Some beginners assume Python remembers both values.
It doesn't.
By the time execution reaches the second line:

```python
my_party = 10
```

the variable's current value becomes:

```text
10
```

When:

```python
print(my_party)
```

runs afterward, you'll get:

```text
10
```

not:

```text
5
```

## Variables Can Be Printed Multiple Times

Example:

```python
my_party = 5
print(my_party)

my_party = 10
print(my_party)
```

Output:

```text
5
10
```

The first print uses the first value.
The second print uses the updated value.
This demonstrates that Python evaluates variables using their current value at that moment in execution.

---

## Python vs JavaScript

### Python

```python
my_party = 5
my_party = 10
```

### JavaScript

```javascript
let myParty = 5;
myParty = 10;
```

These behave similarly.

### Important Difference for JavaScript Developers

Many JavaScript developers prefer:

```javascript
const myParty = 5;
```

which prevents reassignment.
Python has no equivalent concept here.
Reassignment is extremely common and expected in Python.
For example:

```python
score = 0
score = 10
score = 25
```

Perfectly normal Python.

---

## Looking Ahead

The lesson does not yet cover calculations, but reassignment becomes especially useful when values change dynamically.

Example:

```python
my_party = 5
my_party = my_party + 2
```

Result:

```text
7
```

You'll learn more about this soon, but it builds directly on the reassignment concept introduced in this lesson.

---

## Variable Lifecycle

Throughout this lesson, variables follow a simple lifecycle:

1. **Create:** `meal_total = 85`
2. **Use:** `print(meal_total)`
3. **Update:** `meal_total = 120`
4. **Use Again:** `print(meal_total)`

This pattern appears everywhere in programming.

---

## Mental Model

Think of a variable as a whiteboard.

Initially:

```python
my_party = 5
```

Whiteboard:

```text
my_party = 5
```

Later:

```python
my_party = 10
```

You erase the old value and write:

```text
my_party = 10
```

The board only displays the most recent value.

---

## Common Beginner Mistakes

### Forgetting to Print the Variable

Incorrect:

```python
my_party = 5
```

Nothing appears because there is no print statement.

Correct:

```python
my_party = 5
print(my_party)
```

### Treating a Variable Name Like Text

Incorrect:

```python
print("my_party")
```

Output:

```text
my_party
```

Python prints the text literally.

Correct:

```python
print(my_party)
```

Output:

```text
5
```

### Assuming Old Values Are Preserved

Incorrect assumption:

```python
my_party = 5
my_party = 10
```

The variable does not contain both values.
It only contains:

```text
10
```

after reassignment.

---

## Key Terms

- **Variable:** A named container that stores a value.
- **Value:** The actual information stored in a variable.
- **Assignment:** Storing a value in a variable using `=`.
- **Reassignment:** Replacing a variable's current value with a new one.
- **`print()`:** A function used to display information in the terminal.
- **Variable Name:** The identifier used to reference stored data.

---

## Key Takeaways

1. Variables allow programs to store information for later use.
2. Assignment uses the `=` operator.
3. The variable name goes on the left and the value goes on the right.
4. Variables can store numbers such as `meal_total = 85`.
5. `print()` retrieves and displays a variable's current value.
6. Variables can be updated through reassignment.
7. Reassignment replaces the previous value.
8. Python always uses the variable's current value when executing code.
9. Storing data in variables makes programs easier to maintain and update.
10. A variable's basic lifecycle is: `Create → Use → Update → Use Again`.

This lesson solidifies the foundational Python workflow you'll use throughout the rest of the course: store a value, recall it, update it, and reuse it. 🐍
rather than mathematical equality.