# Python OOP Notes for Automation Engineers (Playwright Context)

These notes explain **Python Classes and OOP from scratch** using
**automation testing analogies** (especially Playwright / Page Object
Model).

------------------------------------------------------------------------

# 1. Why Do We Need Classes?

In small scripts we can write code using functions and variables.

Example:

``` python
username = "admin"
password = "123"

def login():
    print("Logging in")
```

Problem:

If your automation framework has:

-   50 pages
-   200 tests
-   many locators and actions

Code becomes **messy and difficult to maintain**.

Solution → **Classes**

Classes help us **group related data and behavior together**.

------------------------------------------------------------------------

# 2. What is a Class?

A **Class is a blueprint used to create objects.**

Automation analogy:

A **Login Page** contains:

Data: - username field - password field - login button

Actions: - enter username - enter password - click login

Diagram:

    LoginPage (Class Blueprint)
    │
    ├── username_field
    ├── password_field
    ├── login_button
    │
    ├── enter_username()
    ├── enter_password()
    └── click_login()

------------------------------------------------------------------------

# 3. Creating a Class in Python

``` python
class LoginPage:

    def enter_username(self):
        print("Typing username")

    def enter_password(self):
        print("Typing password")

    def click_login(self):
        print("Click login button")
```

This **defines a blueprint** but does not run anything yet.

------------------------------------------------------------------------

# 4. What is an Object?

An **object is a real instance created from a class**.

Example:

``` python
login = LoginPage()
```

Diagram:

    Class → LoginPage
           │
           ▼
    Object → login

Now we can use it:

``` python
login.enter_username()
login.enter_password()
login.click_login()
```

Output:

    Typing username
    Typing password
    Click login button

------------------------------------------------------------------------

# 5. Understanding `self`

`self` refers to **the current object calling the method**.

Example:

``` python
login = LoginPage()
login.enter_username()
```

Python internally converts this to:

    LoginPage.enter_username(login)

So inside the method:

    self = login object

Diagram:

    login object
       │
       ▼
    enter_username(self)

------------------------------------------------------------------------

# 6. Constructor (`__init__`)

The constructor runs **automatically when an object is created**.

Example:

``` python
class LoginPage:

    def __init__(self, username, password):
        self.username = username
        self.password = password

    def login(self):
        print("Logging in with", self.username, self.password)
```

Create object:

``` python
login = LoginPage("admin", "123")
login.login()
```

Memory view:

    login object
    │
    ├── username = admin
    └── password = 123

------------------------------------------------------------------------

# 7. Class Variables vs Instance Variables

## Class Variable

Shared by **all objects**.

Example:

``` python
class LoginPage:
    url = "https://example.com/login"
```

Diagram:

    LoginPage class
    │
    └── url (shared)
          │
          ├── login1
          └── login2

Both objects access the same value.

------------------------------------------------------------------------

## Instance Variable

Unique for **each object**.

Example:

``` python
class LoginPage:

    def __init__(self, username):
        self.username = username
```

Example:

``` python
login1 = LoginPage("admin")
login2 = LoginPage("tester")
```

Memory:

    login1 → username = admin
    login2 → username = tester

------------------------------------------------------------------------

# 8. Encapsulation

Encapsulation means:

> Grouping data and methods inside a class.

Example:

``` python
class LoginPage:

    username_locator = "#username"
    password_locator = "#password"

    def enter_username(self):
        print("Fill username")

    def enter_password(self):
        print("Fill password")
```

Everything related to **login page functionality** stays in one place.

Benefits:

-   clean code
-   maintainability
-   easy updates

------------------------------------------------------------------------

# 9. Inheritance

Inheritance allows **one class to reuse functionality from another
class**.

Automation frameworks commonly use a **BasePage**.

Diagram:

            BasePage
           (Common methods)
             /        \
            /          \
       LoginPage    SearchPage

------------------------------------------------------------------------

# 10. Inheritance Example

Parent class:

``` python
class BasePage:

    def click(self, locator):
        print("Clicking", locator)

    def fill(self, locator, text):
        print("Filling", locator, text)
```

Child class:

``` python
class LoginPage(BasePage):

    def login(self):
        self.fill("#username", "admin")
        self.fill("#password", "123")
        self.click("#login")
```

Execution:

``` python
login = LoginPage()
login.login()
```

Python searches methods in this order:

    1. Current class
    2. Parent class
    3. Parent's parent class

This search process is called **Method Resolution Order (MRO)**.

------------------------------------------------------------------------

# 11. How OOP is Used in Playwright Frameworks

Typical framework structure:

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

Example Page Object:

``` python
class LoginPage(BasePage):

    def __init__(self, page):
        self.page = page

    def enter_username(self, username):
        self.page.fill("#username", username)

    def enter_password(self, password):
        self.page.fill("#password", password)

    def click_login(self):
        self.page.click("#login")
```

Test:

``` python
login = LoginPage(page)

login.enter_username("admin")
login.enter_password("123")
login.click_login()
```

------------------------------------------------------------------------

# 12. Key Mental Model

    Class → Blueprint

    Object → Real instance

    self → Current object

    Constructor → Runs when object is created

    Class Variable → Shared

    Instance Variable → Unique per object

    Inheritance → Reuse parent class functionality

------------------------------------------------------------------------

# 13. Quick Interview Tips

Why use OOP in automation frameworks?

Answer:

-   Code reusability
-   Maintainable framework
-   Page Object Model implementation
-   Clean test architecture
