# Python Object-Oriented Programming (OOP) — Interview Preparation

## 1. What is OOP?

- **OOP (Object-Oriented Programming)** is a programming paradigm that organizes code around objects and classes.
- It helps make code reusable, modular, maintainable, and easier to manage.
- OOP is based on four main principles:
  1. **Encapsulation**
  2. **Inheritance**
  3. **Polymorphism**
  4. **Abstraction**
- Python supports OOP, allowing developers to build structured and scalable applications.

---

## 2. What is a Class and an Object?

- **Class:** A class is a blueprint for creating objects. It defines the attributes and methods that describe the data and behaviour of those objects.
- **Object:** An object is an instance of a class. Multiple objects can be created from the same class, each having its own data while sharing the same structure and behaviour.

### Example

In Python, `Car` can be a class, while `electric_car` and `petrol_car` are objects created from that class. Both objects share the same class structure but store different values for `fuel_type`.

```python
class Car:
    def __init__(self, fuel_type):
        self.fuel_type = fuel_type

electric_car = Car("Electric")
petrol_car = Car("Petrol")
```

---

## 3. What is a Constructor in Python?

A constructor is used to initialize an object when it is created. In Python, the `__init__()` method initializes an object's attributes with the required values. It is called automatically when an object is created, helping the object start with its initial data.

### `__init__()`
- `__init__()` is a special method in Python that initializes an object's attributes.
- It is automatically called when an object is created. Technically, it is an initializer, not the method that allocates memory/creates the object (`__new__()` creates it).

### `self`
- `self` refers to the current instance (object) of the class.
- It is used to access and assign that object's attributes and methods. Python passes the object as the first argument to an instance method automatically.

### Code Example

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person_details = Person("Alan", 22)
print(person_details.name, person_details.age)
# Output: Alan 22
```

**Code Explanation:**
- `__init__()` initializes the `name` and `age` attributes when `person_details` is created.
- `self.name` and `self.age` store values in the current object, while `person_details` refers to that object.

---

## 4. What is `self` in Python OOP?

`self` is a reference to the current object of a class. It is used to access the object's attributes and methods inside the class. In Python, `self` is passed automatically as the first argument when an instance method is called through an object. Although `self` is the standard naming convention, it is not a reserved keyword in Python.

---

## 5. What is the Difference Between a Function and a Method?

- **Function:** A reusable block of code that performs a specific task. It is defined using the `def` keyword and can be called independently. It can accept arguments and return a result using the `return` statement.

- **Method:** A function defined inside a class and associated with its objects or class. An instance method typically uses `self` to access the object's attributes and other methods. Like a function, it can also accept arguments and return a result.

### Comparison Table

| Feature | Function | Method |
| :--- | :--- | :--- |
| **Definition** | Defined independently using `def`. | Defined inside a class using `def`. |
| **Invocation** | Called by its name independently (`add_numbers(10, 20)`). | Called on an object or class (`obj.multiply(10, 20)`). |
| **First Argument** | Does not require an implicit first argument. | Instance methods take `self` as the first argument. |
| **Association** | Not bound to any class or object. | Bound to a class or instance. |

### Code Example

```python
def add_numbers(a, b):          # Standalone function
    return a + b

class Calculator:
    def multiply(self, a, b):   # Method inside class
        return a * b

print(add_numbers(10, 20))      # Function call independently (Output: 30)

obj = Calculator()       
print(obj.multiply(10, 20))     # Method call via object (Output: 200)
```

**Code Explanation:** `add_numbers()` is a standalone function that returns the sum of two numbers, whereas `multiply()` is a method defined inside the `Calculator` class that returns their product.

---

## 6. What are Dunder Methods in Python?

Dunder methods, also called **double underscore methods** or **magic methods**, are special methods in Python that begin and end with double underscores, such as `__init__()` and `__str__()`. They allow objects to define how they behave with built-in operations, such as object creation, string representation, comparisons, and arithmetic. Python automatically calls many of these methods when the corresponding operation is performed.

### Top 10 Important Dunder Methods

| Dunder Method | Use Case |
| :--- | :--- |
| `__init__()` | Initializes an object's attributes when it is created. |
| `__str__()` | Returns a readable string representation of an object (for `str()`, `print()`). |
| `__repr__()` | Returns an unambiguous, developer-oriented representation of an object. |
| `__len__()` | Defines the behaviour of `len()` for an object. |
| `__add__()` | Defines behaviour for the `+` operator. |
| `__eq__()` | Defines equality comparison using `==`. |
| `__getitem__()` | Allows accessing items using indexing or keys (`obj[key]`). |
| `__iter__()` | Makes an object iterable by returning an iterator. |
| `__next__()` | Returns the next item from an iterator. |
| `__call__()` | Allows an instance to be called like a function (`obj()`). |

---

## 7. How Does an Object Access Attributes?

- An object accesses its attributes using **dot notation** (`.`).
- We use the object name followed by a dot and the attribute name to get its value.
- **Example:** `person_details.name` accesses the `name` attribute of the `person_details` object.

```python
class Person:
    def __init__(self, name):
        self.name = name

person_details = Person("Alan")
print(person_details.name)
# Output: Alan
```

---

## 8. How Can an Object Create an Attribute Outside the Class?

- An object can create a new attribute outside the class dynamically using **dot notation and assignment**.
- The new attribute belongs **only to that specific object** and is not automatically available on other objects of the same class.
- **Example:** `person_details.age = 27` creates an `age` attribute for that specific object, even if it was not defined inside the class.

```python
class Person:
    def __init__(self, name):
        self.name = name

person_details = Person("Alan")

# Creating an attribute dynamically outside the class:
person_details.age = 27
print(person_details.age)
# Output: 27
```
