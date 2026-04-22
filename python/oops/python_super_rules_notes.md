# Python super() -- Rules & Concepts (Interview Notes)

## 🔥 1. What is super()?

`super()` is used to call the **next method in the MRO (Method
Resolution Order)**.

👉 It does NOT always call parent class\
👉 It calls next class in MRO chain

------------------------------------------------------------------------

## 🔹 2. Rule 1: super() follows MRO

``` python
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
```

### MRO:

    D → B → C → A → object

------------------------------------------------------------------------

## 🔹 3. Rule 2: Use super() in multiple inheritance

❌ Wrong:

``` python
A.show(self)
```

✔ Correct:

``` python
super().show()
```

------------------------------------------------------------------------

## 🔹 4. Rule 3: super() passes self automatically

``` python
super().show()
```

Internally:

    NextClass.show(self)

------------------------------------------------------------------------

## 🔹 5. Rule 4: Use inside class methods

❌ Wrong:

``` python
super().show()   # outside class
```

✔ Correct:

``` python
class A:
    def show(self):
        super().show()
```

------------------------------------------------------------------------

## 🔹 6. Rule 5: Method must exist in MRO

If method not found → AttributeError

------------------------------------------------------------------------

## 🔹 7. Rule 6: Use in **init** (IMPORTANT)

``` python
class A:
    def __init__(self):
        print("A init")

class B(A):
    def __init__(self):
        super().__init__()
        print("B init")
```

### Output:

    A init
    B init

------------------------------------------------------------------------

## 🔹 8. Rule 7: Avoid hardcoding parent class

❌ Bad:

``` python
A.show(self)
```

✔ Good:

``` python
super().show()
```

------------------------------------------------------------------------

## 🔹 9. Rule 8: Order depends on class definition

``` python
class D(B, C)
```

MRO:

    D → B → C → A

------------------------------------------------------------------------

## 🔹 10. Rule 9: Works with methods and constructors

-   Normal methods
-   **init**()
-   Any callable

------------------------------------------------------------------------

## 🔹 11. Rule 10: Chain must be maintained

If one class skips super() → chain breaks ❌

------------------------------------------------------------------------

## 🔥 MOST IMPORTANT RULE

👉 super() calls next class in MRO, NOT parent

------------------------------------------------------------------------

## 🔹 12. Cheat Sheet

  Rule             Meaning
  ---------------- -------------------------------
  MRO based        Next class in chain
  No hardcoding    Always use super()
  Auto self        No need to pass
  Chain required   All classes must call super()

------------------------------------------------------------------------

## 🚀 Summary

-   super() ensures proper method execution chain
-   Important in multiple inheritance
-   Maintains clean and flexible design
