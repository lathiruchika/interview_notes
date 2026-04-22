# Python Methods -- Instance vs Class vs Static (Interview Notes)

## 🔥 1. Overview

  Type              First Parameter   Access             Called By
  ----------------- ----------------- ------------------ --------------
  Instance Method   self              Instance + Class   Object
  Class Method      cls               Class only         Class/Object
  Static Method     None              None directly      Class/Object

------------------------------------------------------------------------

## 🔹 2. Instance Method

``` python
class Student:
    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)
```

### Rules:

-   Must have `self`
-   Access instance + class variables
-   Called using object

------------------------------------------------------------------------

## 🔹 3. Class Method

``` python
class Student:
    school = "ABC"

    @classmethod
    def show_school(cls):
        print(cls.school)
```

### Rules:

-   Uses `@classmethod`
-   First parameter `cls`
-   Access class variables
-   Cannot access instance variables directly

------------------------------------------------------------------------

## 🔹 4. Static Method

``` python
class Student:

    @staticmethod
    def add(a, b):
        return a + b
```

### Rules:

-   Uses `@staticmethod`
-   No `self` or `cls`
-   Cannot access class or instance variables directly

------------------------------------------------------------------------

## 🔥 5. Comparison Example

``` python
class Demo:
    x = 100

    def __init__(self, y):
        self.y = y

    def instance_method(self):
        print("Instance:", self.x, self.y)

    @classmethod
    def class_method(cls):
        print("Class:", cls.x)

    @staticmethod
    def static_method():
        print("Static: no access")
```

### Output:

    Instance: 100 10
    Class: 100
    Static: no access

------------------------------------------------------------------------

## 🔥 6. Key Differences

  Feature           Instance   Class          Static
  ----------------- ---------- -------------- ---------------
  First Param       self       cls            none
  Access Instance   ✅         ❌             ❌
  Access Class      ✅         ✅             ❌
  Needs Object      ✅         ❌             ❌
  Decorator         ❌         @classmethod   @staticmethod

------------------------------------------------------------------------

## 🔥 7. QA Example

``` python
class LoginPage:

    base_url = "dev.com"

    def login(self, user):
        print("Login user:", user)

    @classmethod
    def get_base_url(cls):
        return cls.base_url

    @staticmethod
    def validate_password(pwd):
        return len(pwd) > 5
```

------------------------------------------------------------------------

## 🔥 8. Tricky Interview Questions

### Q1: Can class method access instance variable?

❌ No

### Q2: Can instance method access class variable?

✅ Yes

### Q3: Can static method access class variable?

❌ No

### Q4: Can we call class method using object?

✅ Yes

------------------------------------------------------------------------

## 🧠 Cheat Sheet

-   Instance → self → object data
-   Class → cls → shared data
-   Static → no relation → utility

------------------------------------------------------------------------

## 🚀 Summary

-   Instance → object behavior
-   Class → shared logic
-   Static → helper functions
