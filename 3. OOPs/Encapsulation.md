# Encapsulation — Interview Guide

---

## <span style="color: red;">1. What is Encapsulation?</span>

<span style="color: dodgerblue;">**Definition:**</span>

Encapsulation is the bundling of data and the methods that operate on that
data into a single unit — a class. It protects classes from accidental
changes or deletions and promotes code reusability and maintainability.

<span style="color: dodgerblue;">**Why it is used:**</span>

- Protects a class's internal data from accidental changes or deletion
- Promotes code reusability and improves maintainability
- Exposes only what is necessary and hides the rest (data hiding)

---

## <span style="color: red;">2. What is a Private Variable?</span>

A private variable is a data member that cannot be accessed or modified
directly from outside the class — only through the class's own methods.

<span style="color: dodgerblue;">**Key characteristics:**</span>

- Hides internal state from the outside world (data hiding)
- Prevents accidental or invalid changes to data
- Access is controlled via **getters** (read) and **setters** (write)
- Enforced by the language's access rules

<span style="color: dodgerblue;">**Syntax:**</span>

| Language | Syntax           | Meaning                              |
|----------|------------------|--------------------------------------|
| Python   | `self.__name`    | Name-mangled (private by convention) |
| Java     | `private int x;` | Access modifier `private`            |

---

## <span style="color: red;">3. What is Name Mangling?</span>

<span style="color: dodgerblue;">**Definition:**</span>

Name mangling is a Python mechanism that automatically modifies attribute
names beginning with two underscores (`__`) to help prevent accidental
access and naming conflicts.

<span style="color: dodgerblue;">**How it works:**</span>

1. **Syntax:** `__variable` becomes `_ClassName__variable`
2. **Example:** Inside the `Student` class, `__marks` becomes `_Student__marks`
3. **Purpose:** Prevents accidental access and naming conflicts, especially in inheritance
4. **Limitation:** Does not provide strict privacy; the attribute can still be accessed using its mangled name

<span style="color: dodgerblue;">**Remember:**</span>

- `__marks` → Name mangling applies
- `_marks` → Name mangling does not apply

---

## <span style="color: red;">4. What are Getter and Setter Methods?</span>

### <span style="color: dodgerblue;">4.1 Getter Method</span>

A getter method is used to **retrieve or read** the value of an attribute.

- Example: `get_marks()`
- Returns the value of `self.__marks`

### <span style="color: dodgerblue;">4.2 Setter Method</span>

A setter method is used to **modify or update** the value of an attribute,
optionally validating it before making changes.

- Example: `set_marks(value)`
- Checks whether the marks are between 0 and 100 before updating `self.__marks`

### <span style="color: dodgerblue;">4.3 Getter vs Setter Comparison</span>

| Getter | Setter |
|---|---|
| Reads an attribute's value | Updates an attribute's value |
| Typically returns a value | Typically accepts a new value |
| `get_marks()` | `set_marks(value)` |

> **Interview takeaway:** Getters and setters provide controlled access to
> an object's attributes. In Python, they are commonly used with
> name-mangled attributes, although properties (`@property`) are another
> Pythonic approach.

### <span style="color: mediumseagreen;">4.4 Example Usage</span>

Using the `Student` class from encapsulation:

```python
s = Student("Ravi", 85)

print(s.get_marks())  # 85 — getter

s.set_marks(90)       # setter
print(s.get_marks())  # 90
```

---

## <span style="color: red;">5. Encapsulation Example (Python)</span>

<span style="color: mediumseagreen;">**A `Student` class — hides marks, controls access**</span>

```python
class Student:
    def __init__(self, name, marks):
        self.name = name            # public
        self.__marks = marks        # private variable

    # Getter
    def get_marks(self):
        return self.__marks

    # Setter with validation
    def set_marks(self, value):
        if 0 <= value <= 100:
            self.__marks = value
        else:
            print("Marks must be between 0 and 100")

# Usage
s = Student("Ravi", 85)
print(s.name)          # Ravi  (public, direct access OK)
print(s.get_marks())   # 85    (private, via getter)

s.set_marks(90)        # valid
print(s.get_marks())   # 90

s.set_marks(150)       # Marks must be between 0 and 100
print(s.__marks)       # AttributeError: 'Student' object has no attribute '__marks'
```

### <span style="color: dodgerblue;">5.1 Explanation</span>

- `name` is public — anyone can read or change it directly
- `__marks` is private (double underscore) — outside code cannot touch it directly
- `get_marks()` is a getter — safe, read-only access
- `set_marks()` is a setter — validates input before changing the value
- Marks can never be set to an invalid number like 150
- This is encapsulation: data is hidden and only changed through controlled methods

---

## <span style="color: red;">6. Instance vs Static (Class) Variables</span>

### <span style="color: dodgerblue;">6.1 What is an Instance Variable?</span>

An instance variable belongs to a specific object. Each object can have its
own value.

### <span style="color: dodgerblue;">6.2 What is a Static Variable (Class Variable)?</span>

A static variable, called a **class variable** in Python, belongs to the
class and is shared among its instances by default.

### <span style="color: dodgerblue;">6.3 Difference Between Instance and Static Variables</span>

| Instance Variable | Static (Class) Variable |
|---|---|
| Belongs to an object | Belongs to the class |
| Each object can have a different value | Shared among instances by default |
| Defined using `self` | Defined directly inside the class |

### <span style="color: mediumseagreen;">6.4 Example Program</span>

```python
class Employee:
    company = "TCS"  # Class variable

    def __init__(self, name):
        self.name = name  # Instance variable


e1 = Employee("Ravi")
e2 = Employee("Priya")

print(e1.name)     # Ravi
print(e2.name)     # Priya

print(e1.company)  # TCS
print(e2.company)  # TCS
```

<span style="color: dodgerblue;">**Explanation:**</span>

- `name` is an instance variable; each employee has a different name
- `company` is a class variable shared by instances by default

> **Interview takeaway:** Instance variables store object-specific data,
> while class variables store data associated with the class.

---
