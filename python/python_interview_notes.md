# 📘 Python Interview Notes -- Week 2

------------------------------------------------------------------------

## ✅ Question 1: Dictionary Key Error

### ❓ Code:

``` python
dictz = {[]: "one"}
```

### ❌ Output:

TypeError: unhashable type: 'list'

### 💡 Explanation:

-   Dictionary keys must be **immutable (hashable)**.
-   `list` is mutable → cannot be used as a key.

### ✅ Correct Example:

``` python
dictz = {(): "one"}  # tuple is allowed
```

------------------------------------------------------------------------

## ✅ Question 2: List of Dictionaries

### ❓ Input:

``` python
input_list = [
    {"name": "EPAM", "class": 1234},
    {"name": "systems", "class": 456}
]
```

### 🎯 Expected Output:

Name: EPAM, Class: 1234\
Name: systems, Class: 456

### ✅ Solution:

``` python
for item in input_list:
    print(f"Name: {item['name']}, Class: {item['class']}")
```

------------------------------------------------------------------------

## ✅ Question 3: OOP Scenario (Employee & Department)

### ❓ Requirement:

-   Employee parent class
-   Department child class
-   Auto assign global ID

### ✅ Solution:

``` python
class Employee:
    global_id = 1

    def __init__(self, name):
        self.name = name
        self.id = Employee.global_id
        Employee.global_id += 1

class Department(Employee):
    def __init__(self, name, dept_name):
        super().__init__(name)
        self.dept_name = dept_name

    def display(self):
        print(f"ID: {self.id}, Name: {self.name}, Dept: {self.dept_name}")
```

### ✅ Usage:

``` python
emp1 = Department("Ruchika", "QA")
emp2 = Department("Amit", "Dev")

emp1.display()
emp2.display()
```

------------------------------------------------------------------------

## 🔥 Key Concepts:

-   Hashable vs Unhashable
-   List & Dict iteration
-   Inheritance
-   Class variables
-   super()
