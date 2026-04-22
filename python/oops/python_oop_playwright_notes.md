# Python OOP Basics for Automation Testers (Playwright Context)

## 1. Why Classes Exist

In large programs we need a way to group **data and behavior together**.

Example without class:

``` python
username = "admin"
password = "123"

def login():
    print("login user")
```

Problem: When projects grow (100 pages, 100 tests), code becomes messy.

Solution → **Classes**

------------------------------------------------------------------------

# 2. What is a Class?

A **class is a blueprint to create objects**.

Automation analogy:

Login Page contains:

Data: - username field - password field - login button

Actions: - enter username - enter password - click login

Diagram:

    LoginPage (Class)
    │
    ├── username_field
    ├── password_field
    ├── login_button
    │
    ├── enter_username()
    ├── enter_password()
    └── click_login()

------------------------------------------------------------------------

# 3. Python Class Example

``` python
class LoginPage:

    def enter_username(self):
        print("Typing username")

    def enter_password(self):
        print("Typing password")

    def click_login(self):
        print("Click login")
```

This defines a **blueprint**.

------------------------------------------------------------------------

# 4. What is an Object?

A **real instance created from a class**.

``` python
login = LoginPage()
```

Diagram:

    Class → LoginPage
           │
           ▼
    Object → login

Use object:

``` python
login.enter_username()
login.enter_password()
login.click_login()
```

------------------------------------------------------------------------

# 5. What is `self`?

`self` refers to **the current object calling the method**.

Example:

``` python
login = LoginPage()
login.enter_username()
```

Python internally runs:

    LoginPage.enter_username(login)

So:

    self = login object

------------------------------------------------------------------------

# 6. Constructor (`__init__`)

Runs automatically when object is created.

``` python
class LoginPage:

    def __init__(self, username, password):
        self.username = username
        self.password = password
```

Create object:

``` python
login = LoginPage("admin", "123")
```

Memory view:

    login object
    │
    ├── username = admin
    └── password = 123

------------------------------------------------------------------------

# 7. Class Variable vs Instance Variable

## Class Variable

Shared by all objects.

``` python
class LoginPage:
    url = "https://example.com/login"
```

Diagram:

    LoginPage
    │
    └── url (shared)
          │
          ├── login1
          └── login2

------------------------------------------------------------------------

## Instance Variable

Unique for each object.

``` python
class LoginPage:

    def __init__(self, username):
        self.username = username
```

    login1 → username = admin
    login2 → username = tester

------------------------------------------------------------------------

# 8. Inheritance

Allows one class to reuse another class's functionality.

Framework example:

    BasePage
       ↑
       │
     ┌─┴─────────────┐
     │               │
    LoginPage     SearchPage

------------------------------------------------------------------------

# 9. Inheritance Example

``` python
class BasePage:

    def click(self, locator):
        print("Click", locator)

class LoginPage(BasePage):

    def login(self):
        self.click("#login")
```

Here:

    LoginPage inherits BasePage

Execution flow:

    login.login()
       │
       ▼
    self.click()
       │
       ▼
    BasePage.click()

------------------------------------------------------------------------

# 10. Why OOP is Used in Automation Frameworks

Benefits:

-   Code Reusability
-   Clean Framework Design
-   Maintainability
-   Scalable test frameworks

Example structure:

    framework
    │
    ├── base
    │   └── base_page.py
    │
    ├── pages
    │   ├── login_page.py
    │   └── search_page.py
    │
    └── tests
        └── test_login.py

------------------------------------------------------------------------

# Final Mental Model

    Class → Blueprint

    Object → Real instance

    self → Current object

    Inheritance → Reuse parent class functionality

------------------------------------------------------------------------

These concepts form the foundation of **Page Object Model (POM)** used
in Playwright, Selenium, and most automation frameworks.
