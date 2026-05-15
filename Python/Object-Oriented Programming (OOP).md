# Python Object-Oriented Programming (OOP) Cheat Sheet

[📄 View GitLab Markdown Documentation](https://gitlab.com)

### 🧱 Core Concepts
* **Class:** Blueprint for creating objects.
* **Object:** Instance of a class.
* **Attributes:** Variables inside a class.
* **Methods:** Functions inside a class.

```python
class Car:
    def __init__(self, brand):
        self.brand = brand  # Attribute

    def drive(self):
        return f"{self.brand} is moving"  # Method

my_car = Car("Toyota")  # Object instantiation
```
💡 **Use Case:** Creating independent user profiles, database connections, or game characters with distinct states.

---

### 🧬 The 4 Pillars of OOP

#### 1. Polymorphism
* Allows different classes to have methods with the same name.
* Adapts behavior based on the object calling it.

```python
class Boat:
    def drive(self):
        return "Sailing on water"

# Both Car and Boat have a .drive() method
for vehicle in [my_car, Boat()]:
    print(vehicle.drive())
```
💡 **Use Case:** Building payment system integrations where `Paypal.process()` and `Stripe.process()` handle logic differently but share an identical execution interface.

#### 2. Encapsulation
* Restricts direct access to methods and variables.
* **Protected:** Single underscore `_variable` (convention only).
* **Private:** Double underscore `__variable` (triggers name mangling).

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0  # Private attribute

    def get_balance(self):  # Getter
        return self.__balance
```
💡 **Use Case:** Preventing sensitive properties (like API keys, passwords, or financial balances) from being accidentally altered by external code.

#### 3. Abstraction
* Hides complex implementation details.
* Requires the `abc` module.
* Abstract methods *must* be overridden by child classes.

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass
```
💡 **Use Case:** Designing structural architecture templates for large development teams to enforce a consistent API design across different database adapters.

#### 4. Inheritance
* Allows a child class to adopt attributes and methods from a parent class.
* Enables code reuse and hierarchies.
* Supports overriding parent methods or expanding them via `super()`.

```python
class ElectricCar(Car):  # Child inherits from Car parent
    def __init__(self, brand, battery_size):
        super().__init__(brand)  # Links to parent constructor
        self.battery_size = battery_size

    def charge(self):
        return "Charging battery..."
```
💡 **Use Case:** Modeling shared system user types where a base `User` class shares basic login logic with specialized `Admin` and `Customer` child subclasses.

---

### 🎛️ Decorators & Method Types
* **Instance Methods:** Take `self` as the first argument. Access instance data.
* **Class Methods:** Take `cls` as the first argument. Use `@classmethod`. Access class-level data.
* **Static Methods:** Take no automatic arguments. Use `@staticmethod`. Isolated behavior.
* **Properties:** Turn methods into attributes using `@property` (getters/setters).

```python
class Demo:
    population = 0  # Class attribute

    @classmethod
    def get_pop(cls):
        return cls.population

    @staticmethod
    def generic_utility(x, y):
        return x + y
```
💡 **Use Case:** Tracking global configuration limits across instances (`@classmethod`) or grouping standalone mathematical helper tools inside an associated class ecosystem (`@staticmethod`).

---

### 📦 Data Classes (`@dataclass`)
* Automatically generates boilerplate methods (`__init__`, `__repr__`, `__eq__`).
* Enabled by importing the `dataclasses` module.
* Use `frozen=True` to create read-only, immutable objects.

```python
from dataclasses import dataclass

@dataclass
class Product:
    name: str
    price: float
    stock: int = 0
```
💡 **Use Case:** Ideal for storing configurations, JSON API responses, database row structures, and lightweight state representations without building heavy logic classes.

---

### 🪄 Magic (Dunder) Methods
* `__init__(self)`: Constructor method.
* `__str__(self)`: Returns a readable string for end-users (`print(obj)`).
* `__repr__(self)`: Returns an unambiguous string for developers.
* `__eq__(self, other)`: Defines behavior for equality operator (`==`).
* `__len__(self)`: Defines behavior for the `len()` function.
