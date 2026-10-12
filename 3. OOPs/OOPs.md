what is oops ?

- OOP (Object-Oriented Programming) is a programming paradigm that organizes code around objects and classes. 

- It helps make code reusable, modular, maintainable, and easier to manage. 

- OOP is based on four main principles: Encapsulation, Inheritance, Polymorphism, and Abstraction. 

- Python supports OOP, allowing developers to build structured and scalable applications.


what is class and object?

Class: A class is a blueprint for creating objects. It defines the attributes and methods that describe the data and behaviour of those objects.

Object: An object is an instance of a class. Multiple objects can be created from the same class, each having its own data while sharing the same structure and behaviour.

Example: In Python, `Car` can be a class, while `electric_car` and `petrol_car` are objects created from that class. Both objects share the same class structure but store different values `fuel_type`.


```python
class Car:

    def __init__(self, fuel_type):
        self.fuel_type = fuel_type

electric_car = Car("Electric")
petrol_car = Car("Petrol")
```


### 1. What is a constructor in Python?

A constructor is used to initialize an object when it is created. In Python, the `__init__()` method initializes an object's attributes with the required values. It is called automatically when an object is created, helping the object start with its initial data.

#### __init__() 

- `__init__()` is a special method in Python that initializes an object's attributes.
- It is automatically called when an object is created. Technically, it is an initializer, not the method that creates the object.

#### self

- `self` refers to the current object of the class.
- It is used to access and assign that object's attributes and methods. Python passes the object as the first argument to an instance method automatically.

### Python Example

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person_details = Person("Alan", 22)
print(person_details.name, person_details.age)
```

Code explanation:

- `__init__()` initializes the `name` and `age` attributes when `person_details` is created.
- `self.name` and `self.age` store values in the current object, while `person_details` refers to that object.