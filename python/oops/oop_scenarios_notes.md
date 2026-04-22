# 📘 OOP Scenario-Based Questions (Interview Practice 🔥)

------------------------------------------------------------------------

## ✅ Question 1: WebDriver Singleton

### ❓ Requirement:

Ensure only one WebDriver instance.

### ✅ Solution:

``` python
class Driver:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.driver = "ChromeDriver"
        return cls._instance
```

------------------------------------------------------------------------

## ✅ Question 2: BaseTest + Child Tests

``` python
class BaseTest:
    def setup(self):
        print("Browser launched")

    def teardown(self):
        print("Browser closed")

class LoginTest(BaseTest):
    def test_login(self):
        self.setup()
        print("Login executed")
        self.teardown()
```

------------------------------------------------------------------------

## ✅ Question 3: Page Object Model

``` python
class LoginPage:
    def __init__(self):
        self.username = "locator"
        self.password = "locator"

    def login(self, user, pwd):
        print(user, pwd)
```

------------------------------------------------------------------------

## ✅ Question 4: Method Overriding

``` python
class BaseEnv:
    def get_url(self):
        return "base"

class QAEnv(BaseEnv):
    def get_url(self):
        return "qa"
```

------------------------------------------------------------------------

## ✅ Question 5: Factory Pattern

``` python
class DriverFactory:
    def get_driver(self, browser):
        if browser == "chrome":
            return "ChromeDriver"
        elif browser == "firefox":
            return "FirefoxDriver"
```

------------------------------------------------------------------------

## ✅ Question 6: Composition

``` python
class Logger:
    def log(self, msg):
        print(msg)

class Test:
    def __init__(self):
        self.logger = Logger()
```

------------------------------------------------------------------------

## ✅ Question 7: Class Variable Counter

``` python
class TestCounter:
    count = 0

    def __init__(self):
        TestCounter.count += 1
```

------------------------------------------------------------------------

## ✅ Question 8: Abstract Class

``` python
from abc import ABC, abstractmethod

class BaseTest(ABC):
    @abstractmethod
    def run_test(self):
        pass
```

------------------------------------------------------------------------

## ✅ Question 9: Context Manager

``` python
class Browser:
    def __enter__(self):
        print("Open")
        return self

    def __exit__(self, *args):
        print("Close")
```

------------------------------------------------------------------------

## ✅ Question 10: Multi-User Manager

``` python
class UserManager:
    def __init__(self, users):
        self.users = users

    def get_user(self, role):
        return self.users.get(role)
```

------------------------------------------------------------------------

## 🚀 Key Concepts:

-   Singleton
-   Inheritance
-   Encapsulation
-   Factory Pattern
-   Composition
-   Abstraction
-   Context Manager
