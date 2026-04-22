
# Python OOP Notes for Automation Engineers (Playwright Context)

These notes explain **Python Classes and OOP from scratch** using **automation testing analogies** (especially Playwright / Page Object Model).

---

# 1. Why Do We Need Classes?

In small scripts we can write code using functions and variables.

Example:

```python
username = "admin"
password = "123"

def login():
    print("Logging in")
```

Problem:

If your automation framework has:

- 50 pages
- 200 tests
- many locators and actions

Code becomes **messy and difficult to maintain**.

Solution → **Classes**

Classes help us **group related data and behavior together**.

---

# 2. What is a Class?

A **Class is a blueprint used to create objects.**

Automation analogy:

A **Login Page** contains:

Data:
- username field
- password field
- login button

Actions:
- enter username
- enter password
- click login

Diagram:

```
LoginPage (Class Blueprint)
│
├── username_field
├── password_field
├── login_button
│
├── enter_username()
├── enter_password()
└── click_login()
```

---

# 3. Creating a Class in Python

```python
class LoginPage:

    def enter_username(self):
        print("Typing username")

    def enter_password(self):
        print("Typing password")

    def click_login(self):
        print("Click login button")
```

This defines a **blueprint** but does not run anything yet.

---

# 4. What is an Object?

An **object is a real instance created from a class**.

Example:

```python
login = LoginPage()
```

Diagram:

```
Class → LoginPage
       │
       ▼
Object → login
```

Use the object:

```python
login.enter_username()
login.enter_password()
login.click_login()
```

---

# 5. Understanding `self`

`self` refers to **the current object calling the method**.

Example:

```python
login = LoginPage()
login.enter_username()
```

Python internally executes:

```python
LoginPage.enter_username(login)
```

So:

```
self = login object
```

---

# 6. Constructor (`__init__`)

The constructor runs **automatically when an object is created**.

```python
class LoginPage:

    def __init__(self, username, password):
        self.username = username
        self.password = password

    def login(self):
        print("Logging in with", self.username, self.password)
```

Create object:

```python
login = LoginPage("admin", "123")
login.login()
```

---

# 7. Class Variables

Class variables are **shared by all objects**.

```python
class LoginPage:
    url = "https://example.com/login"
```

Example:

```python
login1 = LoginPage()
login2 = LoginPage()

print(login1.url)
print(login2.url)
```

Both objects access the **same value**.

---

# 8. Instance Variables

Instance variables belong to **each object individually**.

```python
class LoginPage:

    def __init__(self, username):
        self.username = username
```

Example:

```python
login1 = LoginPage("admin")
login2 = LoginPage("tester")

print(login1.username)
print(login2.username)
```

Output:

```
admin
tester
```

---

# 9. Encapsulation

Encapsulation means **grouping related data and methods inside a class**.

```python
class LoginPage:

    username_locator = "#username"
    password_locator = "#password"

    def enter_username(self):
        print("Fill username")

    def enter_password(self):
        print("Fill password")
```

Benefits:

- better structure
- maintainable code
- reusable components

---

# 10. Inheritance

Inheritance allows **one class to reuse another class's functionality**.

Example hierarchy:

```
BasePage
   ↑
   │
LoginPage
```

---

# 11. Inheritance Example

Parent class:

```python
class BasePage:

    def click(self, locator):
        print("Clicking", locator)

    def fill(self, locator, text):
        print("Filling", locator, text)
```

Child class:

```python
class LoginPage(BasePage):

    def login(self):
        self.fill("#username", "admin")
        self.fill("#password", "123")
        self.click("#login")
```

Execution:

```python
login = LoginPage()
login.login()
```

---

# 12. Playwright Page Object Example

```python
class LoginPage:

    def __init__(self, page):
        self.page = page

    def enter_username(self, username):
        self.page.fill("#username", username)

    def enter_password(self, password):
        self.page.fill("#password", password)

    def click_login(self):
        self.page.click("#login")
```

Test example:

```python
login = LoginPage(page)

login.enter_username("admin")
login.enter_password("123")
login.click_login()
```

---

# 13. Framework Structure

```
framework/
│
├── base/
│   └── base_page.py
│
├── pages/
│   ├── login_page.py
│   └── search_page.py
│
└── tests/
    └── test_login.py
```

---

# 14. Key Mental Model

```
Class → Blueprint

Object → Instance created from class

self → Current object

Constructor → Runs during object creation

Class Variable → Shared

Instance Variable → Unique per object

Inheritance → Child class reuses parent class methods
```

---

# 15. Interview Tip

Why use OOP in automation frameworks?

Answer:

- Reusability
- Maintainability
- Clean Page Object Model
- Scalable automation framework
