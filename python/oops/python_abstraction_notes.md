# Python Abstraction Notes (OOP) -- QA Automation Perspective

## 1. What is Abstraction?

**Abstraction means hiding implementation details and exposing only the
essential functionality.**

In simple words:

> User sees *what a function does*, not *how it does it*.

### Real‑Life Example

Driving a car:

You see:

-   Steering
-   Brake
-   Accelerator

You **do not see**:

-   Engine mechanics
-   Fuel injection system
-   Internal machine parts

That hidden complexity = **Abstraction**.

------------------------------------------------------------------------

# 2. Abstraction in Automation Frameworks

Without abstraction, test code may look like this:

``` python
page.fill("#username", "admin")
page.fill("#password", "123")
page.click("#login")
```

This exposes **implementation details**.

Using abstraction:

``` python
login_page.login("admin", "123")
```

Inside the `login()` method the framework handles:

-   entering username
-   entering password
-   clicking login
-   waits and validations

Test cases remain **clean and readable**.

------------------------------------------------------------------------

# 3. Abstract Classes in Python

Python supports abstraction using:

``` python
from abc import ABC, abstractmethod
```

Components:

  -----------------------------------------------------------------------
  Component                           Purpose
  ----------------------------------- -----------------------------------
  ABC                                 Base class for abstract classes

  @abstractmethod                     Declares method that must be
                                      implemented by child classes
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 4. Creating an Abstract Class

``` python
from abc import ABC, abstractmethod

class Page(ABC):

    @abstractmethod
    def open(self):
        pass
```

Meaning:

-   `Page` is an **abstract class**
-   `open()` is an **abstract method**
-   Child classes **must implement this method**

------------------------------------------------------------------------

# 5. Child Class Implementation

``` python
class LoginPage(Page):

    def open(self):
        print("Opening Login Page")
```

Now `LoginPage` becomes a **concrete class**.

Object creation is allowed:

``` python
login = LoginPage()
login.open()
```

Output:

    Opening Login Page

------------------------------------------------------------------------

# 6. Rule: Abstract Class Cannot Be Instantiated

This will fail:

``` python
page = Page()
```

Error:

    TypeError: Can't instantiate abstract class Page

Because abstract classes are **only blueprints**.

------------------------------------------------------------------------

# 7. When Child Class Does NOT Implement Abstract Method

Example:

``` python
class LoginPage(Page):
    pass
```

Now:

    login = LoginPage()

Error occurs because:

-   `open()` is not implemented
-   `LoginPage` is still **abstract**

------------------------------------------------------------------------

# 8. Important Rule

A class **cannot be instantiated if it still contains unimplemented
abstract methods**.

Python checks this during object creation.

------------------------------------------------------------------------

# 9. Multi-Level Inheritance with Abstract Classes

Example:

``` python
class A(ABC):

    @abstractmethod
    def show(self):
        pass


class B(A):
    pass


class C(B):

    def show(self):
        print("C")
```

Object creation:

``` python
c = C()
c.show()
```

Works because:

-   `C` finally implements `show()`
-   So `C` becomes a **concrete class**.

------------------------------------------------------------------------

# 10. When No Class Implements Abstract Method

Example:

``` python
class A(ABC):

    @abstractmethod
    def show(self):
        pass


class B(A):
    pass


class C(B):
    pass
```

Now:

    c = C()

Error occurs because:

-   `show()` is never implemented
-   All classes remain **abstract**

------------------------------------------------------------------------

# 11. Key Mental Model

    Abstract Class
          ↓
    Defines rules

    Child Class
          ↓
    Must implement abstract methods

    If implemented → Concrete Class → Object allowed
    If not implemented → Still Abstract → Object NOT allowed

------------------------------------------------------------------------

# 12. Automation Framework Example

Abstract base page:

``` python
class BasePage(ABC):

    @abstractmethod
    def page_url(self):
        pass
```

Child page:

``` python
class LoginPage(BasePage):

    def page_url(self):
        return "/login"
```

Benefit:

Every page **must define its URL**, ensuring framework consistency.

------------------------------------------------------------------------

# 13. Interview Definition

**Abstraction**:

> Abstraction hides implementation details and exposes only necessary
> functionality.\
> In automation frameworks it helps create clean test APIs like
> `login()` or `checkout()` while hiding internal UI interactions.

------------------------------------------------------------------------

# 14. Quick Summary

  Concept           Meaning
  ----------------- ---------------------------------------
  Abstract Class    Blueprint that cannot be instantiated
  Abstract Method   Method without implementation
  Child Class       Must implement abstract methods
  Concrete Class    Class with all implementations
  Object Creation   Allowed only for concrete classes
