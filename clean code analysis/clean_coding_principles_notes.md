# Clean Coding Principles -- Study Notes

## What is Clean Code?

Clean code is code that is **easy to read, understand, maintain, and
extend**. The concept was popularized by **Robert C. Martin (Uncle
Bob)** in the book *Clean Code*.

Goals: - Readable - Maintainable - Scalable - Easy to debug

------------------------------------------------------------------------

# 1. Meaningful Names

Names should clearly describe their purpose.

Bad:

``` python
x = 5
y = 10
z = x + y
```

Good:

``` python
price = 5
tax = 10
total_price = price + tax
```

Guidelines: - Use descriptive variable names - Avoid abbreviations - Use
domain-related names

------------------------------------------------------------------------

# 2. Small Functions

Functions should do **one thing only**.

Bad:

``` python
def login_and_save_user():
    authenticate_user()
    save_user_data()
    send_email()
```

Better:

``` python
def authenticate_user():
    pass

def save_user_data():
    pass

def send_email():
    pass
```

Benefits: - easier testing - easier debugging

------------------------------------------------------------------------

# 3. Single Responsibility Principle

Each function, class, or module should have **one responsibility**.

Example:

Bad:

``` python
class UserManager:
    def login(self):
        pass

    def send_email(self):
        pass

    def generate_report(self):
        pass
```

Better:

``` python
class UserAuthentication:
    pass

class EmailService:
    pass

class ReportGenerator:
    pass
```

------------------------------------------------------------------------

# 4. Avoid Deep Nesting

Too many nested conditions make code difficult to read.

Bad:

``` python
if user:
    if user.is_active:
        if user.is_admin:
            allow_access()
```

Better:

``` python
if not user:
    return

if not user.is_active:
    return

if user.is_admin:
    allow_access()
```

------------------------------------------------------------------------

# 5. Use Constants Instead of Magic Numbers

Bad:

``` python
if retry_count > 3:
    stop_login()
```

Better:

``` python
MAX_RETRY = 3

if retry_count > MAX_RETRY:
    stop_login()
```

------------------------------------------------------------------------

# 6. Keep Code DRY (Don't Repeat Yourself)

Avoid duplicate code.

Bad:

``` python
total1 = price1 + tax
total2 = price2 + tax
```

Better:

``` python
def calculate_total(price, tax):
    return price + tax
```

------------------------------------------------------------------------

# 7. Use Clear Comments

Comments should explain **why**, not what.

Bad:

``` python
# add numbers
total = a + b
```

Better:

``` python
# retry login because server occasionally times out
retry_login()
```

------------------------------------------------------------------------

# 8. Consistent Formatting

Follow style guides like **PEP 8**.

Examples: - 4 spaces indentation - max line length 79 - snake_case for
variables and functions

Example:

``` python
def calculate_total(price, tax):
    total = price + tax
    return total
```

------------------------------------------------------------------------

# 9. Avoid Large Classes

Classes should represent a **single concept**.

Bad:

``` python
class ApplicationManager:
    pass
```

Better:

``` python
class LoginService:
    pass

class CartService:
    pass
```

------------------------------------------------------------------------

# 10. Write Readable Code First

Prioritize readability over clever code.

Bad:

``` python
result = [x for x in range(100) if x % 2 == 0]
```

Sometimes clearer:

``` python
even_numbers = []
for number in range(100):
    if number % 2 == 0:
        even_numbers.append(number)
```

------------------------------------------------------------------------

# Clean Code Checklist

Before committing code ask:

-   Is the code readable?
-   Are function names meaningful?
-   Are functions small?
-   Is duplicate code removed?
-   Are constants used instead of magic numbers?
-   Does the code follow PEP 8?

------------------------------------------------------------------------

# Clean Code Example

Bad:

``` python
def f(a,b):
 return a+b
```

Clean version:

``` python
def calculate_total(price, tax):
    """Calculate total price including tax."""
    total_price = price + tax
    return total_price
```

------------------------------------------------------------------------

# Key Takeaway

Clean code is not just about making code run.

It is about writing code that **humans can easily read, understand, and
maintain**.
