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

This defines a **blueprint** but does not run anything yet.

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

Use the object:

``` python
login.enter_username()
login.enter_password()
login.click_login()
```

------------------------------------------------------------------------

# 5. Understanding `self`

`self` refers to **the current object calling the method**.

Example:

``` python
login = LoginPage()
login.enter_username()
```

Python internally executes:

``` python
LoginPage.enter_username(login)
```

So:

    self = login object

------------------------------------------------------------------------

# 6. Constructor (`__init__`)

The constructor runs **automatically when an object is created**.

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

------------------------------------------------------------------------

# 7. Class Variables

Class variables are **shared by all objects**.

``` python
class LoginPage:
    url = "https://example.com/login"
```

Example:

``` python
login1 = LoginPage()
login2 = LoginPage()

print(login1.url)
print(login2.url)
```

Both objects access the **same value**.

------------------------------------------------------------------------

# 8. Instance Variables

Instance variables belong to **each object individually**.

``` python
class LoginPage:

    def __init__(self, username):
        self.username = username
```

Example:

``` python
login1 = LoginPage("admin")
login2 = LoginPage("tester")

print(login1.username)
print(login2.username)
```

Output:

    admin
    tester

------------------------------------------------------------------------

# 9. Encapsulation

Encapsulation means **grouping related data and methods inside a
class**.

``` python
class LoginPage:

    username_locator = "#username"
    password_locator = "#password"

    def enter_username(self):
        print("Fill username")

    def enter_password(self):
        print("Fill password")
```

Benefits:

-   better structure
-   maintainable code
-   reusable components

------------------------------------------------------------------------

# 10. Inheritance

Inheritance allows **one class to reuse another class's functionality**.

Example hierarchy:

    BasePage
       ↑
       │
    LoginPage

------------------------------------------------------------------------

# 11. Inheritance Example

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

------------------------------------------------------------------------

# 12. Playwright Page Object Example

``` python
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

``` python
login = LoginPage(page)

login.enter_username("admin")
login.enter_password("123")
login.click_login()
```

------------------------------------------------------------------------

# 13. Framework Structure

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

------------------------------------------------------------------------

# 14. Key Mental Model

    Class → Blueprint

    Object → Instance created from class

    self → Current object

    Constructor → Runs during object creation

    Class Variable → Shared

    Instance Variable → Unique per object

    Inheritance → Child class reuses parent class methods

------------------------------------------------------------------------

# 15. Interview Tip

Why use OOP in automation frameworks?

Answer:

-   Reusability
-   Maintainability
-   Clean Page Object Model
-   Scalable automation framework

------------------------------------------------------------------------

# 16. Method Overriding

Method overriding occurs when a **child class provides its own
implementation of a method that already exists in the parent class**.

``` python
class BasePage:

    def click(self):
        print("Base click")


class LoginPage(BasePage):

    def click(self):
        print("Login click")


login = LoginPage()
login.click()
```

Output

    Login click

------------------------------------------------------------------------

# 17. Method Resolution Order (MRO)

MRO defines **how Python searches for methods in inheritance
hierarchies**.

Search order:

    Current Class
    ↓
    Parent Class
    ↓
    Grandparent Class
    ↓
    object

Example

``` python
class A:
    def show(self):
        print("A")

class B(A):
    pass

class C(B):
    pass

c = C()
c.show()
```

Output

    A

MRO chain

    C → B → A → object

------------------------------------------------------------------------

# 18. Multi‑Level Inheritance

Inheritance can extend across multiple levels.

``` python
class BasePage:
    def click(self):
        print("Base")

class LoginPage(BasePage):
    def click(self):
        print("Login")

class AdminLoginPage(LoginPage):
    pass

admin = AdminLoginPage()
admin.click()
```

Output

    Login

Search order

    AdminLoginPage → LoginPage → BasePage

------------------------------------------------------------------------

# 19. Constructor Inheritance

If a child class **does not define a constructor**, Python automatically
calls the parent constructor.

``` python
class A:
    def __init__(self):
        print("A")

class B(A):
    pass

b = B()
```

Output

    A

------------------------------------------------------------------------

# 20. Constructor Override Without super()

If a child class defines its own constructor, the parent constructor
**will NOT run automatically**.

``` python
class BasePage:

    def __init__(self, page):
        self.page = page


class LoginPage(BasePage):

    def __init__(self, page):
        print("LoginPage constructor")

login = LoginPage("BrowserPage")
```

------------------------------------------------------------------------

# 21. Using super()

To run the parent constructor explicitly we use `super()`.

``` python
class BasePage:

    def __init__(self, page):
        self.page = page


class LoginPage(BasePage):

    def __init__(self, page):
        super().__init__(page)
```

Execution flow

    LoginPage.__init__()
    ↓
    BasePage.__init__()
    ↓
    self.page created

------------------------------------------------------------------------

# 22. Polymorphism

Polymorphism means **same method name but different behavior depending
on the object type**.

``` python
class BasePage:
    def click(self):
        print("Base click")

class LoginPage(BasePage):
    def click(self):
        print("Login click")

class CartPage(BasePage):
    def click(self):
        print("Cart click")

pages = [LoginPage(), CartPage()]

for page in pages:
    page.click()
```

Output

    Login click
    Cart click

------------------------------------------------------------------------

# 23. Why These Concepts Matter in Automation Frameworks

Typical automation framework structure

    BasePage
       ↑
    LoginPage
       ↑
    AdminLoginPage

Benefits

-   Code reuse
-   Less duplication
-   Easier maintenance
-   Clean Page Object Model design
-   Scalable automation framework

------------------------------------------------------------------------

# Final OOP Mental Model

    Class → Blueprint
    Object → Instance created from class
    self → Reference to current object
    Constructor → Initializes object
    Inheritance → Reuse parent class behavior
    Method Overriding → Child replaces parent method
    MRO → Python method search order
    super() → Calls parent class constructor
    Polymorphism → Same method, different behavior
