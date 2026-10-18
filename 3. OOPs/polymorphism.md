# Python Polymorphism — Interview Preparation Guide

> **Main idea:** Polymorphism means that the same operation or method call can produce different behavior depending on the object or values involved.
>
> This guide focuses on how polymorphism actually works in Python. Textbook classifications are included near the end, but they are less important than understanding the examples.

## Contents

1. What is polymorphism? (important!)
2. Runtime polymorphism and method overriding (important!)
3. Duck typing
4. Built-in polymorphic functions
5. Operator overloading
6. Method overloading in Python
7. Using an abstract base class as a common interface
8. Compile-time vs. runtime polymorphism
9. Common interview questions
10. Quick revision table

---

## 1. What is polymorphism in Python?

### <span style="color: #c62828;">Q1. What is polymorphism?</span>

**Interview answer:** Polymorphism is an object-oriented programming concept that means **“many forms.”** The same method or operation can behave differently depending on the object or data it works with. It lets us write common code that can work with different kinds of objects. For example, a `Dog` and a `Cat` can both have a `sound()` method, but each produces a different sound. This makes programs more flexible and easier to extend.

### What do “interface” and “forms” mean?

In the phrase **“one interface, many forms”**:

- **Interface** means the way you use an object—for example, calling a method named `sound()`.
- **Forms** means the different behaviors provided by different objects—for example, a dog barks and a cat meows.

Python does **not** have an `interface` keyword. Here, “interface” simply means a shared method or expected behavior.

### <span style="color: #16803c;">Example: The same method name, different behavior</span>

```python
class Dog:
    def sound(self):
        print("Barking")


class Cat:
    def sound(self):
        print("Meowing")


def make_sound(animal):
    animal.sound()


make_sound(Dog())
make_sound(Cat())
```

**Output:**

```text
Barking
Meowing
```

**Code explanation:**

1. `Dog` and `Cat` both provide a method named `sound()`.
2. `make_sound()` calls `animal.sound()` without needing separate functions for dogs and cats.
3. When the argument is a `Dog`, its method prints `Barking`; when it is a `Cat`, its method prints `Meowing`.
4. The function can work with both objects because they support the behavior it needs.

**Important:** These classes do not inherit from a common parent. Python can still use them this way. This is an example of **duck typing**, explained in Section 3.

---

## 2. Runtime polymorphism and method overriding

### <span style="color: #c62828;">Q2. What is runtime polymorphism?</span>

**Interview answer:** Runtime polymorphism is when the implementation used for a method call is determined while the program is running, based on the object involved. In Python, a common example is method overriding: a child class provides its own implementation of a method defined in a parent class. Calling that method on different objects can produce different results. Python looks up the method according to the object's class and its method resolution order (MRO).

### <span style="color: #c62828;">Q3. What is method overriding?</span>

**Interview answer:** Method overriding occurs when a child class defines a method with the same name as a method in its parent class. The child implementation is normally used when that method is called on an instance of the child class. Overriding allows a child class to customize or extend inherited behavior. It is a common way to demonstrate runtime polymorphism in Python.

### <span style="color: #16803c;">Example: Overriding a parent method</span>

```python
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


animals = [Dog(), Cat(), Animal()]

for animal in animals:
    animal.sound()
```

**Output:**

```text
Dog barks
Cat meows
Animal makes a sound
```

**Code explanation:**

- `Dog` and `Cat` inherit from `Animal`.
- Both child classes override `sound()` with their own implementations.
- The loop calls `sound()` on each object using the same line of code.
- Python runs the implementation appropriate for each object's class.

**Why is this useful?** You can add another class, such as `Cow`, and provide its own `sound()` method without rewriting the loop.

---

## 3. Duck typing

### <span style="color: #c62828;">Q4. What is duck typing in Python?</span>

**Interview answer:** Duck typing is a Python approach in which an object's suitability depends on the behavior it provides, rather than its exact class or whether it inherits from a specific parent. The idea is often summarized as: “If it behaves like a duck in the way we need, we can use it like a duck.” For example, a function that calls `sound()` can accept any object that has a suitable `sound()` method. Duck typing makes it easier to write flexible code, but the object must actually provide the required behavior or the call can fail at runtime.

### <span style="color: #16803c;">Example: Different objects, no shared parent class</span>

```python
class Dog:
    def sound(self):
        print("Barking")


class Doorbell:
    def sound(self):
        print("Ding dong")


def play_sound(device):
    device.sound()


play_sound(Dog())
play_sound(Doorbell())
```

**Output:**

```text
Barking
Ding dong
```

**Code explanation:** `Dog` and `Doorbell` are unrelated classes, but both have `sound()`. `play_sound()` needs that method, not a particular parent class. If we passed an object without a `sound()` method, Python would raise an `AttributeError` when the function tried to call it.

**Duck typing vs. overriding:** Overriding uses inheritance and replaces inherited behavior. Duck typing does not require inheritance; it focuses on whether an object supplies the required behavior. They are related to polymorphism, but they are not the same concept.

---

## 4. Built-in polymorphic functions

### <span style="color: #c62828;">Q5. Can Python's built-in functions demonstrate polymorphism?</span>

**Interview answer:** Yes. Some built-in functions work with different types of objects and perform an operation appropriate to each type. For example, `len()` returns the number of characters in a string, the number of items in a list, or the number of keys in a dictionary. The same function name is used, but the meaning of the result depends on the kind of object passed to it.

### <span style="color: #16803c;">Example: `len()` works with different types</span>

```python
print(len("Python"))
print(len([10, 20, 30]))
print(len({"name": "Raj", "age": 22}))
```

**Output:**

```text
6
3
2
```

**Code explanation:** The same function, `len()`, works with a string, a list, and a dictionary. It returns a length appropriate to each object: six characters, three list items, and two dictionary keys.

---

## 5. Operator overloading

### <span style="color: #c62828;">Q6. What is operator overloading?</span>

**Interview answer:** Operator overloading lets an operator such as `+`, `-`, or `==` have behavior appropriate to the objects on which it is used. Python supports this through special methods, often called *dunder methods*, such as `__add__()` for `+`. For built-in types, `+` can add numbers or concatenate strings. A custom class can define its own behavior for an operator by implementing the relevant special method.

### <span style="color: #16803c;">Example: Overloading `+` for a custom class</span>

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        if not isinstance(other, Point):
            return NotImplemented
        return Point(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Point({self.x}, {self.y})"


p1 = Point(2, 3)
p2 = Point(4, 1)

print(p1 + p2)
```

**Output:**

```text
Point(6, 4)
```

**Code explanation:**

- `p1 + p2` invokes the `Point` class's `__add__()` method.
- The method adds the two objects' `x` values and their `y` values, then returns a new `Point`.
- `__repr__()` controls the readable representation shown by `print()` in this example.
- `NotImplemented` signals that this method does not handle the other operand's type, allowing Python to try the appropriate fallback behavior or raise a `TypeError`.

Operator overloading is related to polymorphism because the same operator can mean different things for different types. In Python, this behavior is implemented through methods and handled at runtime; it should not automatically be called *compile-time polymorphism*.

---

## 6. Method overloading in Python

### <span style="color: #c62828;">Q7. Does Python support method overloading?</span>

**Interview answer:** Python does not support traditional method overloading by defining several methods with the same name but different parameter lists in one class. If a method name is defined again in the same class body, the later definition replaces the earlier one. A common Python alternative is to use default arguments or `*args` when one method needs to accept different numbers of arguments.

### <span style="color: #16803c;">Example: Use default arguments instead</span>

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c


calc = Calculator()

print(calc.add(10))
print(calc.add(10, 20))
print(calc.add(10, 20, 30))
```

**Output:**

```text
10
30
60
```

**Code explanation:** The method accepts one, two, or three numbers because `b` and `c` have default values. This provides flexible argument handling, but it is not traditional signature-based method overloading.

**Useful technical note:** Python's `typing.overload` decorator is a different feature: it lets developers describe multiple call signatures for static type checkers. The overload declarations must be followed by a real implementation; the declarations themselves do not create multiple runtime implementations.

---

## 7. Polymorphism through a common interface

### <span style="color: #c62828;">Q8. How can an abstract base class help with polymorphism?</span>

**Interview answer:** An abstract base class (ABC) can define methods that subclasses are expected to implement. It provides a common contract so that different subclasses can be used through the same method call. The base class defines the expected behavior, while each concrete subclass supplies its own implementation. This is useful when a program needs a clear, shared design for interchangeable components.

### <span style="color: #16803c;">Example: Different payment methods</span>

```python
from abc import ABC, abstractmethod


class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount):
        pass


class CardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Paid ₹{amount} by card")


class WalletPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Paid ₹{amount} by wallet")


def checkout(method, amount):
    method.pay(amount)


checkout(CardPayment(), 500)
checkout(WalletPayment(), 200)
```

**Output:**

```text
Paid ₹500 by card
Paid ₹200 by wallet
```

**Code explanation:**

- `PaymentMethod` defines a common `pay()` contract using `@abstractmethod`.
- `CardPayment` and `WalletPayment` each implement `pay()` differently.
- `checkout()` calls the same method on either object without needing payment-specific branches.
- Because `PaymentMethod` has an abstract method, it cannot be instantiated until its abstract requirements are implemented.

**Do not confuse these ideas:** An ABC is one way to establish a shared interface. Duck typing can provide polymorphic behavior without an ABC or a shared parent class.

---

## 8. Compile-time vs. runtime polymorphism

### <span style="color: #c62828;">Q9. What is the difference between compile-time and runtime polymorphism?</span>

This is a common OOP textbook classification, but it should be applied carefully when discussing Python.

| Term | General OOP meaning | Python-specific note |
|---|---|---|
| Compile-time polymorphism | In languages with static overload resolution, the compiler selects an applicable implementation based on declarations and types. | Python does not use traditional compile-time method overload resolution. It is misleading to label Python's ordinary operator overloading as compile-time polymorphism. |
| Runtime polymorphism | The behavior or implementation is selected while the program runs. | This is a central way to understand Python method calls, including overriding and duck-typed calls. |

**Interview-safe answer:** “Compile-time and runtime polymorphism are common textbook categories across OOP languages. Python is dynamically typed and relies heavily on runtime behavior. For Python, I focus on method overriding, duck typing, and operator overloading, and I note that traditional method overloading by signature is not directly supported.”

There is no single official Python language rule that says polymorphism must be divided into exactly two execution types or exactly four implementation patterns. These labels are teaching classifications; the important thing is to explain the mechanism accurately.

---

## 9. Common interview questions

### <span style="color: #c62828;">Q10. Why is polymorphism useful?</span>

**Answer:** Polymorphism lets different objects be used through a common method or operation. It reduces repeated conditional logic, makes code easier to extend, and allows new implementations to work with existing code. For example, a checkout function can call `pay()` on different payment-method objects without containing separate payment logic for every type.

### <span style="color: #c62828;">Q11. What is the difference between inheritance and polymorphism?</span>

**Answer:** Inheritance lets a class reuse or extend another class's attributes and methods. Polymorphism lets the same operation or interface behave differently for different objects. Inheritance can be used to implement polymorphism, such as through method overriding, but polymorphic behavior in Python can also work through duck typing without inheritance.

### <span style="color: #c62828;">Q12. What is the difference between method overriding and method overloading?</span>

| Method overriding | Method overloading |
|---|---|
| A child class provides its implementation of a method inherited from a parent. | Multiple signatures with the same method name are provided to handle different argument combinations. |
| Supported in Python. | Traditional signature-based overloading is not directly supported in Python. |
| Commonly used to customize inherited behavior. | Defaults or `*args` can often provide similar flexibility. |

### <span style="color: #c62828;">Q13. Must polymorphic classes inherit from the same parent?</span>

**Answer:** No. A common parent class is one way to organize a shared interface, but Python also supports duck typing. Unrelated classes can work with the same function if they provide the behavior that function calls.

### <span style="color: #c62828;">Q14. What happens if an object does not provide the required method?</span>

**Answer:** If code attempts to call a missing method, Python usually raises `AttributeError`. Duck typing does not automatically guarantee that an object has the required behavior; the code must receive a suitable object or handle the possible failure.

### <span style="color: #c62828;">Q15. Is operator overloading the same as method overriding?</span>

**Answer:** No. Operator overloading defines how an operator works for a class through special methods such as `__add__()`. Method overriding replaces an inherited method's implementation in a child class. They are different mechanisms, although both can contribute to polymorphic behavior.

---

## 10. Quick revision

| Concept | Remember this |
|---|---|
| Polymorphism | Same operation or method call, different behavior depending on the object or values. |
| Runtime polymorphism | The behavior used is determined while the program runs. |
| Method overriding | A child class customizes a method inherited from a parent class. |
| Duck typing | Focus on the behavior an object provides, not its exact class. |
| Built-in polymorphism | Functions such as `len()` work with different supported types. |
| Operator overloading | Special methods such as `__add__()` define operator behavior for custom classes. |
| Method overloading | Traditional signature-based method overloading is not directly supported in Python; defaults and `*args` are common alternatives. |
| Abstract base class | Defines a contract that concrete subclasses are expected to implement. |
| “One interface, many forms” | The same way of using different objects can trigger different behavior. |

### Best short answer to memorize

> **Polymorphism means “many forms.” In Python, the same method or operation can behave differently depending on the object. For example, `Dog.sound()` can print “Barking” while `Cat.sound()` prints “Meowing.” Polymorphism helps make code flexible and extensible. Common Python examples include method overriding, duck typing, and operator overloading.**

---

