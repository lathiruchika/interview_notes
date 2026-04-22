# Python MRO (Method Resolution Order) -- Complete Notes

## 🔥 1. What is MRO?

**MRO (Method Resolution Order)** defines the order in which Python
searches for methods and attributes in a class hierarchy.

👉 When you call:

``` python
obj.method()
```

Python checks: 1. Object 2. Class 3. Parent classes

------------------------------------------------------------------------

## 🔹 2. Basic Example

``` python
class A:
    def show(self):
        print("A")

class B(A):
    pass

b = B()
b.show()
```

### ✅ MRO:

    B → A → object

### ✅ Output:

    A

------------------------------------------------------------------------

## 🔹 3. Multiple Inheritance

``` python
class A:
    def show(self):
        print("A")

class B:
    def show(self):
        print("B")

class C(A, B):
    pass

c = C()
c.show()
```

### ✅ MRO:

    C → A → B → object

### ✅ Output:

    A

------------------------------------------------------------------------

## 🔹 4. Diamond Problem (Tricky)

``` python
class A:
    def show(self):
        print("A")

class B(A):
    pass

class C(A):
    pass

class D(B, C):
    pass

d = D()
d.show()
```

### ✅ MRO:

    D → B → C → A → object

### ✅ Output:

    A

------------------------------------------------------------------------

## 🔹 5. How to Check MRO

``` python
print(D.__mro__)
```

### Output:

    (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)

------------------------------------------------------------------------

## 🔹 6. Key Rules of MRO

-   Left to Right priority
-   Child class first
-   No class repetition
-   Uses C3 Linearization

------------------------------------------------------------------------

## 🔹 7. Internal Working

When calling:

``` python
obj.method()
```

Python searches:

    Object → Class → Parent → Grandparent → object

------------------------------------------------------------------------

## 🔹 8. QA Automation Example

``` python
class BasePage:
    def click(self):
        print("Base click")

class LoginPage(BasePage):
    pass

login = LoginPage()
login.click()
```

### MRO:

    LoginPage → BasePage → object

------------------------------------------------------------------------

## 🔹 9. Interview Answer

MRO (Method Resolution Order) defines the order in which Python searches
for methods in a class hierarchy. It ensures consistent method lookup
using C3 linearization, especially in multiple inheritance.

------------------------------------------------------------------------

## 🔹 10. Cheat Sheet

  Concept                Meaning
  ---------------------- -------------------------------
  MRO                    Method lookup order
  **mro**                Shows resolution order
  Multiple Inheritance   Uses MRO to resolve conflicts

------------------------------------------------------------------------

## 🚀 Summary

-   MRO decides which method gets executed
-   Important in inheritance and overriding
-   Always follows consistent order
