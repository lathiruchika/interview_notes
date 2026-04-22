# 🚀 Class Decorators & OOP Behavior (Interview Notes)

---

## 1. What is a Class Decorator?

A **class decorator** is a function that:
- Takes a class as input
- Modifies or enhances it
- Returns the modified class

```python
def decorator(cls):
    return cls
```

Usage:
```python
@decorator
class Test:
    pass
```

---

## 2. Execution Flow (VERY IMPORTANT)

```text
1. Class body executes
2. Class object is created
3. Decorator runs
4. Object creation → __init__ runs
```

👉 Decorator runs at **class definition time**, NOT object creation time.

---

## 3. Internal Working

```python
@decorator
class Test:
    pass
```

Internally:
```python
Test = decorator(Test)
```

---

## 4. Example: Adding Class Variable

```python
def decorator(cls):
    cls.env = "QA"
    return cls
```

Access:
```python
t = Test()
print(t.env)  # QA
```

---

## 5. Class vs Instance Variable

### Class Variable
- Shared across all objects

```python
Test.env = "QA"
```

### Instance Variable
- Unique per object

```python
t.env = "PROD"
```

---

## 6. Key Rule (IMPORTANT)

```text
t.env = "PROD"
→ Creates instance variable
→ Does NOT modify class variable
```

Memory Model:
```text
Class → env = "QA"

Object t →
    env = "PROD"
```

---

## 7. Variable Lookup Order

```text
1. Instance
2. Class
```

Example:
```python
print(t.env)
```

- If found in instance → use it
- Else → check class

---

## 8. Adding Methods via Decorator

```python
def decorator(cls):
    cls.base_url = "https://qa.com"

    def get_url(self):
        return self.base_url

    cls.get_url = get_url
    return cls
```

Usage:
```python
t = Test()
print(t.get_url())  # https://qa.com
```

---

## 9. Function vs Method Reference

```python
print(t.get_url)   # memory reference
print(t.get_url()) # execution
```

### Key Rule:
```text
name     → reference
name()   → execution
```

---

## 10. Class vs Object Method Access

| Expression        | Output                      |
|------------------|-----------------------------|
| Test.get_url     | function reference          |
| t.get_url        | bound method reference      |
| t.get_url()      | actual value                |

---

## 11. Real Use Cases in Automation Framework

- Add base_url to all page classes
- Add logging to all methods
- Add retry mechanism
- Attach Allure steps
- Add environment configuration

---

## 12. Interview Answer (Final)

**Q: What is a class decorator?**

👉 "A class decorator is a function that takes a class, modifies or enhances it, and returns the modified class. It executes at class definition time."

---

## 13. Golden Mental Model 🔐

```text
Decorator → modifies class at definition time

Object assignment → creates instance variable

Lookup → instance → class
```

---

## 14. Common Interview Trap 🚨

❌ Wrong: Decorator runs at object creation

✅ Correct: Decorator runs at class definition

---

## 15. Summary

- Class decorator modifies class
- Runs once at definition
- Can add variables and methods
- Instance assignment does NOT affect class
- Lookup order: instance → class

---

💡 Tip: Always explain with execution flow + example in interview

