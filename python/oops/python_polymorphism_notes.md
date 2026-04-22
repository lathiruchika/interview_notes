 # Python Polymorphism Notes

## What is Polymorphism?

**Polymorphism** means *one interface, multiple behaviors*.

In Python, the same method name can perform different actions depending on:
- The object calling it
- The number or type of parameters

Example concept:

```python
class Dog:
    def speak(self):
        print("Bark")

class Cat:
    def speak(self):
        print("Meow")

animals = [Dog(), Cat()]

for animal in animals:
    animal.speak()
```

Output:

```
Bark
Meow
```

Same method → different behavior.

---

# Types of Polymorphism in Python

1. **Method Overloading (Simulated in Python)**
2. **Method Overriding (True runtime polymorphism)**

---

# 1. Method Overloading

## Definition

Method overloading means:

> Multiple methods with the same name but different parameters.

Languages like **Java/C++ support this directly**, but **Python does NOT support true method overloading**.

If multiple methods with the same name are written, **Python keeps only the last one**.

Example:

```python
class Calculator:

    def add(self, a, b):
        return a + b

    def add(self, a, b, c):
        return a + b + c
```

Here, the first method is **overwritten by the second method**.

---

## How Python Achieves Overloading

Python simulates overloading using:

### 1. Default Arguments

```python
class Calculator:

    def add(self, a, b, c=0):
        return a + b + c

calc = Calculator()

print(calc.add(2,3))
print(calc.add(2,3,4))
```

---

### 2. Using *args

```python
class Calculator:

    def add(self, *numbers):
        return sum(numbers)

calc = Calculator()

print(calc.add(1,2))
print(calc.add(1,2,3,4))
```

---

### 3. Using Type Checking

```python
class Printer:

    def show(self, value):

        if isinstance(value, int):
            print("Integer:", value)

        elif isinstance(value, str):
            print("String:", value)
```

---

## Rules of Method Overloading in Python

1. Python does **not allow multiple methods with the same name**.
2. Only the **last defined method is valid**.
3. Overloading is achieved using:

   - Default parameters
   - `*args`
   - `**kwargs`
   - Type checking

4. Happens **inside the same class**.

---

# 2. Method Overriding

## Definition

Method overriding occurs when:

> A child class provides a new implementation of a method already defined in the parent class.

This is **true runtime polymorphism in Python**.

---

## Basic Example

```python
class BasePage:

    def open_page(self):
        print("Opening Base Page")


class LoginPage(BasePage):

    def open_page(self):
        print("Opening Login Page")
```

Usage:

```python
page = LoginPage()
page.open_page()
```

Output:

```
Opening Login Page
```

---

## Rules of Method Overriding

### Rule 1: Inheritance is required

```python
class Child(Parent):
```

---

### Rule 2: Method name must be the same

Correct:

```
open_page()
```

Incorrect:

```
openPage()
```

---

### Rule 3: Method parameters should match

Example:

```python
class A:
    def show(self):
        pass

class B(A):
    def show(self):
        pass
```

---

### Rule 4: Python follows MRO (Method Resolution Order)

Search order:

```
Child → Parent → Grandparent
```

---

### Rule 5: Parent method can be called using super()

```python
class BasePage:

    def open_page(self):
        print("Opening Base Page")


class LoginPage(BasePage):

    def open_page(self):
        super().open_page()
        print("Opening Login Page")
```

Output:

```
Opening Base Page
Opening Login Page
```

---

# Real Automation Framework Example

Example using Page Object Model structure.

```python
class BasePage:

    def open_page(self):
        print("Open base URL")


class LoginPage(BasePage):

    def open_page(self):
        print("Open login URL")


class DashboardPage(BasePage):

    def open_page(self):
        print("Open dashboard URL")
```

Usage:

```python
pages = [LoginPage(), DashboardPage()]

for page in pages:
    page.open_page()
```

Output:

```
Open login URL
Open dashboard URL
```

---

# Comparison Table

| Feature              | Method Overloading | Method Overriding |
|----------------------|--------------------|-------------------|
| Inheritance Required | No                 | Yes |
| Method Name          | Same               | Same |
| Parameters           | Usually Different  | Usually Same |
| Occurs In            | Same Class         | Parent & Child |
| Python Support       | Simulated          | Fully Supported |

---

# Quick Interview Answer

**Polymorphism in Python is of two types:**

### Method Overloading

- Same method name
- Different parameters
- Achieved using `default arguments`, `*args`, `**kwargs`, type checking

### Method Overriding

- Child class redefines parent class method
- Requires inheritance
- Python uses **MRO (Method Resolution Order)** to determine which method runs.

---

# One-Line Memory Trick

**Overloading → Same class, different parameters**  
**Overriding → Parent-child class, same method replaced**

