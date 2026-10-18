# Python Inheritance — Interview Preparation Guide

A beginner-friendly guide with simple interview answers, runnable Python examples, outputs, and code explanations.

> **What does “inherit” mean?** In general English, *inherit* means receiving something from someone else. In Python, it means a child class can use attributes and methods defined in a parent class without writing them again.
>
> For example, if `Animal` has an `eat()` method and `Dog` inherits from `Animal`, the `Dog` class can use `eat()`.

---

<h2 style="color:#d32f2f">Q1. What is inheritance?</h2>

**Interview answer:**

Inheritance is an OOP concept in which one class acquires attributes and methods from another class. The existing class is called the **parent class**, and the class that receives them is called the **child class**. It helps us reuse existing code instead of writing the same code again. It also allows child classes to add new features or customize existing behavior. Inheritance generally represents an **Is-A relationship**, such as a Dog is an Animal.

<h3 style="color:#2e7d32">Example code: Basic inheritance</h3>

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


dog = Dog()
dog.eat()   # Inherited from Animal
dog.bark()  # Defined in Dog
```

**Output:**

```text
Animal is eating
Dog is barking
```

**Code explanation:** `Dog(Animal)` means `Dog` inherits from `Animal`. The `Dog` object can call `eat()` even though that method is defined in `Animal`. The `bark()` method belongs directly to `Dog`.

---

<h2 style="color:#d32f2f">Q2. What is single inheritance?</h2>

**Interview answer:**

Single inheritance occurs when one child class inherits from one parent class. The child class can access the parent's available attributes and methods. It can also define its own methods and attributes. This makes it easy to extend an existing class without duplicating code. For example, `Dog` inherits from `Animal`.

<h3 style="color:#2e7d32">Example code: Single inheritance</h3>

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


dog = Dog()
dog.eat()
dog.bark()
```

**Output:**

```text
Eating
Barking
```

**Code explanation:** `Dog` has one direct parent, `Animal`. It inherits `eat()` and adds its own `bark()` method.

---

<h2 style="color:#d32f2f">Q3. What is multilevel inheritance?</h2>

**Interview answer:**

Multilevel inheritance occurs when inheritance forms a chain of classes. One class inherits from a parent, and another class inherits from that child class. The last child can access available methods and attributes from the classes above it. This allows functionality to be reused across multiple levels. For example, `Puppy` inherits from `Dog`, which inherits from `Animal`.

<h3 style="color:#2e7d32">Example code: Multilevel inheritance</h3>

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


class Puppy(Dog):
    def weep(self):
        print("Weeping")


puppy = Puppy()
puppy.eat()
puppy.bark()
puppy.weep()
```

**Output:**

```text
Eating
Barking
Weeping
```

**Code explanation:** `Puppy` inherits from `Dog`, and `Dog` inherits from `Animal`. Therefore, a `Puppy` object can use available methods from all three classes.

---

<h2 style="color:#d32f2f">Q4. What is multiple inheritance?</h2>

**Interview answer:**

Multiple inheritance occurs when one child class inherits from two or more parent classes. The child class can use available functionality from all those parents. This is useful when a class needs features from different classes. If parent classes have methods with the same name, Python follows the Method Resolution Order (MRO) to determine which implementation is found first. For example, `Smartphone` inherits from `Camera` and `Phone`.

<h3 style="color:#2e7d32">Example code: Multiple inheritance</h3>

```python
class Camera:
    def take_photo(self):
        print("Taking photo")


class Phone:
    def make_call(self):
        print("Making call")


class Smartphone(Camera, Phone):
    pass


mobile = Smartphone()
mobile.take_photo()
mobile.make_call()
```

**Output:**

```text
Taking photo
Making call
```

**Code explanation:** `Smartphone(Camera, Phone)` declares two parent classes. Because `Smartphone` does not define these methods itself, Python finds `take_photo()` in `Camera` and `make_call()` in `Phone`.

---

<h2 style="color:#d32f2f">Q5. What is hierarchical inheritance?</h2>

**Interview answer:**

Hierarchical inheritance occurs when two or more child classes inherit from the same parent class. Each child class receives the shared functionality of the parent. Each child can also define its own specific methods and behavior. This avoids repeating common code in multiple classes. For example, both `Dog` and `Cat` inherit from `Animal`.

<h3 style="color:#2e7d32">Example code: Hierarchical inheritance</h3>

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


class Cat(Animal):
    def meow(self):
        print("Meowing")


dog = Dog()
cat = Cat()

dog.eat()
cat.eat()
dog.bark()
cat.meow()
```

**Output:**

```text
Eating
Eating
Barking
Meowing
```

**Code explanation:** Both `Dog` and `Cat` inherit the shared `eat()` method from `Animal`. They also have their own methods, `bark()` and `meow()`.

---

<h2 style="color:#d32f2f">Q6. What is hybrid inheritance?</h2>

**Interview answer:**

Hybrid inheritance is a combination of two or more types of inheritance. For example, a program may combine multilevel and hierarchical inheritance. It allows classes to share common functionality while creating more complex class relationships. Python supports hybrid inheritance, including combinations involving multiple inheritance. However, complex inheritance structures can make code harder to understand and maintain.

<h3 style="color:#2e7d32">Example code: Hybrid inheritance</h3>

```python
class Vehicle:
    def start(self):
        print("Vehicle started")


class Car(Vehicle):
    def drive(self):
        print("Car is driving")


class Bike(Vehicle):
    def ride(self):
        print("Bike is riding")


class ElectricCar(Car):
    def charge(self):
        print("Car is charging")


car = ElectricCar()
car.start()
car.drive()
car.charge()
```

**Output:**

```text
Vehicle started
Car is driving
Car is charging
```

**Code explanation:** This structure combines hierarchical inheritance (`Car` and `Bike` both inherit from `Vehicle`) with multilevel inheritance (`ElectricCar` inherits from `Car`, which inherits from `Vehicle`).

---

<h2 style="color:#d32f2f">Q7. What is method overriding?</h2>

**Interview answer:**

Method overriding occurs when a child class defines a method with the same name as a method in its parent class. When that method is called on a child object, Python generally uses the child's implementation. This allows the child class to customize inherited behavior. The method name and compatible usage should be maintained when overriding methods. For example, `Dog` can override the `sound()` method of `Animal` to print `"Barking"`.

<h3 style="color:#2e7d32">Example code: Method overriding</h3>

```python
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


dog = Dog()
dog.sound()
```

**Output:**

```text
Dog barks
```

**Code explanation:** Both classes define `sound()`. When called on a `Dog` object, Python uses the method defined in `Dog`, overriding the inherited version for that object.

---

<h2 style="color:#d32f2f">Q8. What is `super()` in Python?</h2>

**Interview answer:**

`super()` is a built-in function that provides access to methods in the next class in the Method Resolution Order. It is commonly used to call a parent's method or constructor from a child class. This helps reuse existing behavior instead of rewriting it. It is especially useful when initializing parent and child class attributes. In multiple inheritance, `super()` follows the MRO rather than always referring directly to one specific parent.

<h3 style="color:#2e7d32">Example code: Using `super()`</h3>

```python
class Animal:
    def __init__(self):
        print("Animal initialized")


class Dog(Animal):
    def __init__(self):
        super().__init__()
        print("Dog initialized")


dog = Dog()
```

**Output:**

```text
Animal initialized
Dog initialized
```

**Code explanation:** Creating `Dog()` calls the `Dog` constructor. `super().__init__()` then calls the next applicable constructor in the MRO, which is `Animal.__init__()` in this example. After it finishes, the rest of `Dog.__init__()` runs.

---

<h2 style="color:#d32f2f">Q9. What is MRO in Python?</h2>

**Interview answer:**

MRO stands for **Method Resolution Order**. It defines the order in which Python searches classes for a method or attribute. It is particularly important when multiple inheritance is used. Python follows a consistent algorithm called C3 linearization to calculate this order. You can check it using `ClassName.mro()` or `ClassName.__mro__`.

<h3 style="color:#2e7d32">Example code: MRO with multiple inheritance</h3>

```python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        print("B")
        super().show()


class C(A):
    def show(self):
        print("C")
        super().show()


class D(B, C):
    def show(self):
        print("D")
        super().show()


obj = D()
obj.show()

print([cls.__name__ for cls in D.mro()])
```

**Output:**

```text
D
B
C
A
['D', 'B', 'C', 'A', 'object']
```

**Code explanation:** `D` inherits from both `B` and `C`. Python's MRO for this class is `D → B → C → A → object`. Each `super().show()` continues to the next class in that order, so the output is `D`, `B`, `C`, and `A`. This example also shows why `super()` does not always mean “call my direct parent”; it means “continue to the next class in the MRO.”

---

## Quick revision table

| Concept | Meaning | Example |
|---|---|---|
| Inheritance | A child class reuses or extends a parent class | `Dog(Animal)` |
| Single inheritance | One child inherits from one parent | `Dog(Animal)` |
| Multilevel inheritance | Inheritance forms a chain | `Puppy(Dog)`, `Dog(Animal)` |
| Multiple inheritance | One child inherits from multiple parents | `Smartphone(Camera, Phone)` |
| Hierarchical inheritance | Multiple children inherit from one parent | `Dog(Animal)`, `Cat(Animal)` |
| Hybrid inheritance | A combination of inheritance types | `Vehicle`, `Car`, `Bike`, `ElectricCar` |
| Method overriding | A child redefines an inherited method | `Dog.sound()` overrides `Animal.sound()` |
| `super()` | Calls the next applicable implementation in the MRO | `super().__init__()` |
| MRO | Determines the order Python searches classes | `D.mro()` |

## Final interview tip

Remember: inheritance means **receiving and reusing code from another class**. The parent provides existing functionality, and the child can reuse, extend, or override it. Inheritance generally represents an **Is-A relationship**—for example, a `Dog` is an `Animal`.
