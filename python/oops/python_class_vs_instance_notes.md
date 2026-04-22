# Python Class vs Instance Variables -- Complete Notes

## 🔹 1. Basic Concept

### Class Variable

-   Defined inside class, outside methods
-   Shared across all objects

Example:

    class A:
        x = 10

### Instance Variable

-   Defined inside constructor using `self`
-   Unique for each object

Example:

    def __init__(self):
        self.y = 20

------------------------------------------------------------------------

## 🔹 2. Attribute Lookup Order

When accessing `obj.var`, Python checks: 1. Instance variable 2. Class
variable 3. Parent class

------------------------------------------------------------------------

## 🔹 3. Example Explained

    class LoginPage:
        username = "ruchika"

        def __init__(self, password):
            self.password = password

    login1 = LoginPage("123")
    login1.username = "admin"

    login2 = LoginPage("345")

### Output:

    login1.username → admin
    login2.username → ruchika

### Explanation:

-   `login1.username` becomes instance variable
-   `login2` uses class variable

------------------------------------------------------------------------

## 🔹 4. Important Interview Questions

### Q1

    class A:
        x = 10

    a1 = A()
    a2 = A()

    a1.x = 20

    print(a1.x)
    print(a2.x)

Answer:

    20
    10

------------------------------------------------------------------------

### Q2

    A.x = 50

Answer:

    50
    50

------------------------------------------------------------------------

### Q3 (Tricky)

    a1.x = 20
    A.x = 50

Answer:

    20
    50

------------------------------------------------------------------------

## 🔹 5. Mutable Class Variable Problem

    class A:
        data = []

    a1 = A()
    a2 = A()

    a1.data.append(1)

Output:

    [1]
    [1]

### Problem:

-   Shared memory

### Fix:

    def __init__(self):
        self.data = []

------------------------------------------------------------------------

## 🔹 6. Delete Instance Variable

    a.x = 20
    del a.x
    print(a.x)

Output:

    10

------------------------------------------------------------------------

## 🔹 7. Key Differences

  Feature   Class Variable   Instance Variable
  --------- ---------------- -------------------
  Scope     Shared           Per object
  Defined   Class level      Constructor
  Memory    One copy         Multiple copies

------------------------------------------------------------------------

## 🔹 8. QA Automation Insight

### ❌ Bad Practice

    class LoginPage:
        username = "admin"

### ✅ Good Practice

    def __init__(self, username):
        self.username = username

### Why?

-   Avoid data conflicts
-   Supports parallel execution
-   Better for multi-environment testing

------------------------------------------------------------------------

## 🔹 9. Final Cheat Sheet

-   `obj.var = value` → Instance variable
-   `Class.var = value` → Class variable
-   Instance has higher priority
-   Mutable class variables are shared ⚠️

------------------------------------------------------------------------

## 🚀 Summary

-   Always prefer instance variables for test data
-   Use class variables for constants
-   Be careful with mutable objects
