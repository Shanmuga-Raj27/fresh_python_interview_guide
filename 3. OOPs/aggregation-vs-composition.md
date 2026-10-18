# Python Interview Guide: Aggregation vs Composition

A practical interview-preparation guide covering **aggregation**, **composition**, and when to choose them over **inheritance**.

> **Quick memory trick**
> - **Inheritance = Is-A** relationship. Example: `Dog` is an `Animal`.
> - **Aggregation = Has-A, with independent objects.** Example: a `Team` has `Player` objects.
> - **Composition = Has-A, with ownership of parts.** Example: an `Order` contains `OrderItem` objects.

---

## 1. Core Concepts

### <span style="color: #d32f2f;">Q1. What is aggregation in Python?</span>

**Interview answer:**

Aggregation is a type of **Has-A relationship** in which one class refers to or uses an object of another class, while that object can exist independently of the containing class. The objects are related, but one does not own the other's entire lifecycle.

For example, a `Team` has `Player` objects. A player can exist before joining a team and can continue to exist after leaving it.

#### <span style="color: #2e7d32;">Example 1: Aggregation — a Team has a Player</span>

```python
class Player:
    def __init__(self, name):
        self.name = name


class Team:
    def __init__(self, player):
        # The Player object is supplied from outside.
        self.player = player


player1 = Player("Raj")
team1 = Team(player1)

print(team1.player.name)  # Raj
print(player1.name)       # Raj — the player exists independently
```

**Why is this aggregation?**

- `player1` is created separately from `Team`.
- The team receives a reference to an existing player.
- The `Player` object can be used without the `Team` object.
- The team does not need to create or exclusively own the player.

**When should you use aggregation?**

Use aggregation when objects collaborate but have independent lifecycles. Common examples include a department referring to employees, a team grouping players, or a course referring to students.

---

### <span style="color: #d32f2f;">Q2. What is composition in Python?</span>

**Interview answer:**

Composition is a strong form of **Has-A relationship** in which one object owns or manages other objects as parts of its design. Those parts are conceptually tied to the owner's lifecycle.

For example, an `Order` contains `OrderItem` objects representing items belonging to that order. If the order is removed from the system, its order items may also be removed as part of the same business operation.

#### <span style="color: #2e7d32;">Example 2: Composition — an Order has an OrderItem</span>

```python
class OrderItem:
    def __init__(self, product, quantity):
        self.product = product
        self.quantity = quantity


class Order:
    def __init__(self, product, quantity):
        # Order creates and manages its own OrderItem.
        self.item = OrderItem(product, quantity)


order1 = Order("Laptop", 1)

print(order1.item.product)   # Laptop
print(order1.item.quantity)  # 1
```

**Why is this composition?**

- `Order` creates its `OrderItem` as part of its own setup.
- The item represents a component of that particular order.
- The design treats the item as belonging to the order.
- The order is responsible for managing that component.

**When should you use composition?**

Use composition when an object is made up of components that it should create, coordinate, or manage. Examples include a computer containing a motherboard, a house containing rooms, or an order containing order-line items.

> **Important Python note:** Python does not automatically enforce aggregation or composition. These are design relationships. Creating a component inside a class is a common composition pattern, but the real distinction is based on ownership and lifecycle rules. A referenced Python object can technically continue to exist even after its owner is deleted if another reference to it remains.

---

### <span style="color: #d32f2f;">Q3. What is the difference between aggregation and composition?</span>

**Interview answer:**

Both aggregation and composition describe **Has-A** relationships. The main difference is ownership and lifecycle: aggregation connects objects that can exist independently, whereas composition models parts that are owned or managed as part of a whole.

| Feature | Aggregation | Composition |
|---|---|---|
| Relationship | Has-A | Strong Has-A |
| Ownership | Usually no exclusive ownership | Whole owns or manages its parts conceptually |
| Object setup | Often created externally and passed in | Often created or managed by the owner |
| Lifecycle | Objects can exist independently | Parts are conceptually tied to the whole's lifecycle |
| Coupling | Usually looser | Usually stronger |
| Example | `Team` has `Player` objects | `Order` has `OrderItem` objects |

**Easy way to remember:** If the two objects can meaningfully exist independently, aggregation is often appropriate. If one object is a component of the other and is managed as part of it, composition is often appropriate.

---

## 2. Relationship with Inheritance

### <span style="color: #d32f2f;">Q4. What is inheritance, and how is it different from aggregation and composition?</span>

**Interview answer:**

Inheritance allows a child class to reuse or extend the behavior of a parent class. It models an **Is-A relationship**. Aggregation and composition model **Has-A relationships**, where a class collaborates with another object instead of becoming a subtype of it.

#### <span style="color: #2e7d32;">Example 3: Inheritance — a Dog is an Animal</span>

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")


class Dog(Animal):
    pass


dog = Dog()
dog.speak()  # Animal makes a sound
```

`Dog` is a kind of `Animal`, so inheritance makes sense.

#### <span style="color: #2e7d32;">Example 4: Composition — a Car has an Engine</span>

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()


car = Car()
car.start()  # Engine started
```

A car is **not** an engine; it **has** an engine. Composition better represents this relationship.

| Relationship | Meaning | Example |
|---|---|---|
| Inheritance | Is-A | `Dog` is an `Animal` |
| Aggregation | Has-A, independent objects | `Team` has `Player` objects |
| Composition | Has-A, owned components | `Car` has an `Engine` |

---

### <span style="color: #d32f2f;">Q5. Why use aggregation or composition instead of inheritance?</span>

**Interview answer:**

Use aggregation or composition when a class needs to **use another object's functionality**, rather than being a specialized type of that object. This avoids forcing an incorrect Is-A relationship and can make the design more flexible.

For example, making `Car` inherit from `Engine` would imply that a car is an engine, which is incorrect. Giving `Car` an `Engine` object expresses the real relationship.

Aggregation and composition can also make it easier to replace a dependency, test a class with a substitute object, and keep responsibilities separate.

**Main benefits:**

- **Correct modeling:** represent real Has-A relationships accurately.
- **Flexibility:** swap one collaborator for another when the interface is compatible.
- **Separation of responsibilities:** each class handles its own job.
- **Testability:** dependencies can often be replaced with simple test doubles.
- **Less inheritance coupling:** avoid deep or unnecessary class hierarchies.

Inheritance is still useful when the child truly is a subtype of the parent and can honor the parent's expected behavior.

---

### <span style="color: #d32f2f;">Q6. When should you use inheritance, aggregation, or composition?</span>

**Interview answer:**

Choose based on the relationship and the responsibility of each class, not simply to reuse code.

| Use | Choose it when | Example |
|---|---|---|
| Inheritance | One class is a valid specialized type of another | `Dog` is an `Animal` |
| Aggregation | One class uses objects that have independent lifecycles | `Team` uses `Player` objects |
| Composition | One class owns or manages its component objects | `Order` manages `OrderItem` objects |

**Decision questions:**

1. **Is-A?** If a `Dog` is an `Animal`, inheritance may fit.
2. **Has-A, but independent?** If a `Team` has players who can exist separately, aggregation may fit.
3. **Has-A, with owned parts?** If an `Order` manages its order items as components, composition may fit.

---

## 3. A Practical Design Example

### <span style="color: #d32f2f;">Q7. How can composition make code more flexible than inheritance?</span>

**Interview answer:**

Composition lets a class delegate work to another object. The collaborating object can potentially be changed without changing the class hierarchy. This is useful when behavior may vary independently of the main class.

#### <span style="color: #2e7d32;">Example 5: A NotificationService uses a sender</span>

```python
class EmailSender:
    def send(self, message):
        print(f"Email: {message}")


class SMSSender:
    def send(self, message):
        print(f"SMS: {message}")


class NotificationService:
    def __init__(self, sender):
        # The service receives a compatible sender object.
        self.sender = sender

    def notify(self, message):
        self.sender.send(message)


email_service = NotificationService(EmailSender())
sms_service = NotificationService(SMSSender())

email_service.notify("Your order is ready")
sms_service.notify("Your order is ready")
```

**What does this demonstrate?**

- `NotificationService` is not an `EmailSender` or an `SMSSender`.
- It **has/uses a sender** and delegates the sending operation to it.
- The sender implementation can be changed when it provides the expected `send()` method.
- This is composition-style dependency injection: the dependency is supplied from outside. Whether the relationship is called composition or aggregation depends on the intended ownership and lifecycle. Because the sender is passed in and may be shared, this example can also be understood as aggregation in a looser ownership model.

**Interview tip:** Do not say inheritance is always bad. The more accurate principle is: **prefer composition over inheritance when you need to combine behavior, unless a genuine subtype relationship makes inheritance the clearer choice.**

---

## 4. Common Follow-Up Questions

### <span style="color: #d32f2f;">Q8. Is aggregation or composition a special Python keyword?</span>

**Answer:** No. Python has no `aggregation` or `composition` keyword. These are object-oriented design concepts implemented using ordinary object references and class relationships.

### <span style="color: #d32f2f;">Q9. Does deleting the owner automatically delete its composed objects in Python?</span>

**Answer:** Not necessarily. Python manages object memory using references and garbage collection. If another reference still points to a component, that object can remain alive. Composition describes intended ownership and lifecycle in the design; it is not an automatic memory-deletion rule.

### <span style="color: #d32f2f;">Q10. Can aggregation be implemented by passing an object through a constructor?</span>

**Answer:** Yes. Passing an existing object into a constructor is a common aggregation pattern when that object has an independent lifecycle. However, constructor injection alone does not prove aggregation; the intended ownership and lifecycle determine the relationship.

### <span style="color: #d32f2f;">Q11. Can composition use an object created outside the class?</span>

**Answer:** It can, depending on the design. Composition is about ownership and lifecycle intent, not strictly about which line creates the object. Creating the component inside the owner is common, but a component can be supplied from outside and still be treated as owned by the receiving object if the design establishes that responsibility.

### <span style="color: #d32f2f;">Q12. Which relationship should I choose just to reuse code?</span>

**Answer:** First model the actual relationship. Use inheritance when the child is genuinely a subtype. Use composition when a class should delegate to another object's behavior. Use aggregation when related objects are meant to remain independently managed. Avoid selecting inheritance only because it appears to reduce duplicated code.

---

## 5. Quick Revision Sheet

| Question | Remember this |
|---|---|
| What is aggregation? | Has-A relationship; related objects can exist independently. |
| What is composition? | Strong Has-A relationship; the whole owns or manages its components conceptually. |
| What is inheritance? | Is-A relationship; a child specializes a parent type. |
| Team and Player? | Common aggregation example. |
| Order and OrderItem? | Common composition example. |
| Dog and Animal? | Inheritance example. |
| Car and Engine? | Composition example. |
| Why composition over inheritance? | Better delegation, flexibility, and separation of responsibilities for Has-A relationships. |
| Does Python enforce object lifecycles? | No; these relationships are design conventions, not special language features. |

## 6. One-Sentence Interview Answer

**Aggregation** means one object uses another object that can exist independently; 

**composition** means one object owns or manages component objects as part of its design; 

**inheritance** means one class is a specialized type of another. Choose the relationship that matches the real-world or software-design relationship instead of using inheritance solely for code reuse.
