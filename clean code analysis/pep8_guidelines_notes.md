# PEP 8 Python Coding Guidelines -- Study Notes

## 1. What is PEP 8?

PEP 8 stands for **Python Enhancement Proposal 8**.\
It is the official style guide for writing **clean, readable, and
consistent Python code**.

Goals: - Improve readability - Maintain consistency across projects -
Make collaboration easier

------------------------------------------------------------------------

# Code Formatting

## Indentation

-   Python uses indentation to define code blocks.
-   **PEP 8 recommends 4 spaces per indentation level.**

Example:

``` python
def login():
    if True:
        print("Login successful")
```

------------------------------------------------------------------------

## Limit Line Length

-   Recommended maximum line length: **79 characters**.
-   Break long lines using parentheses.

Example:

``` python
result = (
    login_user(username, password)
    and validate_session(user)
)
```

------------------------------------------------------------------------

# Naming Conventions

## Variables

Use **snake_case**.

``` python
user_name = "admin"
total_count = 5
```

------------------------------------------------------------------------

## Functions

Use **snake_case**.

``` python
def login_user():
    pass
```

------------------------------------------------------------------------

## Classes

Use **PascalCase (CapWords)**.

``` python
class LoginPage:
    pass
```

------------------------------------------------------------------------

## Constants

Use **UPPER_CASE**.

``` python
MAX_RETRY = 3
BASE_URL = "https://example.com"
```

------------------------------------------------------------------------

# Whitespace Rules

## Around Operators

Use spaces around operators.

``` python
total = a + b
```

Avoid:

``` python
total=a+b
```

------------------------------------------------------------------------

## After Commas

Always add one space.

``` python
numbers = [1, 2, 3]
```

------------------------------------------------------------------------

## Avoid Extra Spaces

Incorrect:

``` python
numbers = [ 1, 2, 3 ]
```

Correct:

``` python
numbers = [1, 2, 3]
```

------------------------------------------------------------------------

# Blank Lines

Use blank lines to separate sections of code.

-   **2 blank lines between top‑level functions**
-   **2 blank lines between classes**
-   **1 blank line between methods inside a class**

Example:

``` python
def login():
    pass


def logout():
    pass
```

------------------------------------------------------------------------

# Import Guidelines

## Import What You Need

Preferred:

``` python
from math import sqrt
```

Avoid unnecessary imports.

------------------------------------------------------------------------

## Prefer Absolute Imports

Absolute import:

``` python
from pages.login_page import LoginPage
```

Relative import:

``` python
from .login_page import LoginPage
```

PEP 8 prefers **absolute imports**.

------------------------------------------------------------------------

## Avoid Wildcard Imports

Avoid:

``` python
from math import *
```

Use:

``` python
from math import sqrt
```

------------------------------------------------------------------------

# Docstrings and Comments

## Comments

Used to explain **specific logic**.

``` python
# retry login because API may fail
retry_login()
```

Rules: - Use a space after `#` - Explain **why**, not obvious code

------------------------------------------------------------------------

## Docstrings

Used to document **functions, classes, or modules**.

``` python
def add(a, b):
    """Add two numbers and return the result."""
    return a + b
```

Docstrings can be accessed using:

``` python
help(add)
```

------------------------------------------------------------------------

# Linting Tools

Linting tools automatically check if code follows PEP 8.

Common tools:

-   **flake8** → style checker
-   **pylint** → deeper code analysis
-   **black** → automatic formatter
-   **isort** → sorts imports

Example:

``` bash
pip install flake8
flake8 test_file.py
```

------------------------------------------------------------------------

# Black Formatter

Install:

``` bash
pip install black
```

Format a file:

``` bash
black test_login.py
```

Format an entire project:

``` bash
black .
```

Black automatically fixes formatting issues.

------------------------------------------------------------------------

# Module Naming

A module is a **Python file (.py)**.

Rules: - Use **lowercase** - Use **underscores if needed** - Keep names
descriptive

Examples:

    login_page.py
    api_utils.py
    config_loader.py

Avoid:

    LoginPage.py
    loginPage.py

------------------------------------------------------------------------

# Package Naming

A package is a **folder containing modules**.

Rules: - Use **short lowercase names** - Avoid uppercase letters - Avoid
underscores if possible

Good examples:

    pages
    utils
    tests
    config

Avoid:

    Pages
    TestCases
    UserServices

------------------------------------------------------------------------

# Typical Automation Framework Structure

    framework/
    │
    ├── pages
    │   ├── login_page.py
    │   └── cart_page.py
    │
    ├── utils
    │   └── api_utils.py
    │
    ├── tests
    │   └── test_login.py
    │
    └── config

Benefits: - organized project structure - easier maintenance - scalable
automation framework

------------------------------------------------------------------------

# Quick Memory Summary

PEP 8 Key Rules:

-   4‑space indentation
-   79 character line length
-   snake_case for variables and functions
-   PascalCase for classes
-   UPPER_CASE for constants
-   lowercase module and package names
-   prefer absolute imports
-   use docstrings for documentation
-   use linting tools like **flake8** and **black**
