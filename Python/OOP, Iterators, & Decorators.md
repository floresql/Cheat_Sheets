# Advanced Python: OOP, Iterators, & Decorators

### 1. Object-Oriented Programming (OOP)
```python
class Animal:
    def __init__(self, name):
        self.name = name  # Instance attribute

    def make_sound(self):
        pass

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name) # Call parent constructor
        self.breed = breed

    def make_sound(self):
        return "Woof!"

my_dog = Dog("Rex", "Collie")
print(my_dog.make_sound())
```

### 2. Decorators
Modify the behavior of a function without changing its code.
```python
def my_decorator(func):
    def wrapper():
        print("Something before the function.")
        func()
        print("Something after the function.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

### 3. Iterators & Generators
Generators use `yield` to return data one piece at a time, saving memory.
```python
# Generator Function
def count_up_to(max):
    count = 1
    while count <= max:
        yield count
        count += 1

counter = count_up_to(3)
print(next(counter)) # 1
print(next(counter)) # 2
```
