# Python Decorators -- Complete Notes

## 1. Definition

A **decorator** is a function that modifies or extends the behavior of
another function **without changing the original function code**.

Simple idea:

Decorator = function that **wraps another function**.

Common uses: - Logging - Authentication - Timing execution - Retry
logic - Test reporting in automation frameworks

------------------------------------------------------------------------

# 2. Basic Decorator Syntax

Normal function:

``` python
def greet():
    print("Hello")
```

Decorator:

``` python
def decorator(func):

    def wrapper():
        print("Before function")
        func()
        print("After function")

    return wrapper
```

Using decorator:

``` python
@decorator
def greet():
    print("Hello")

greet()
```

Python internally converts this to:

``` python
greet = decorator(greet)
```

------------------------------------------------------------------------

# 3. Execution Flow

Calling:

``` python
greet()
```

Execution order:

1.  wrapper starts
2.  prints "Before function"
3.  original function runs
4.  prints "After function"

Output:

    Before function
    Hello
    After function

------------------------------------------------------------------------

# 4. Decorator Rules

### Rule 1 --- Decorator must accept a function

``` python
def decorator(func):
```

### Rule 2 --- Decorator must define a wrapper

``` python
def wrapper():
```

### Rule 3 --- Wrapper must call the original function

``` python
func()
```

### Rule 4 --- Decorator must return the wrapper

``` python
return wrapper
```
note: if wrapper is not return will get "NoneType" error

### Rule 5 --- Wrapper should return the function result

Correct pattern:

``` python
result = func(*args, **kwargs)
return result
```
    

------------------------------------------------------------------------

# 5. Using \*args and \*\*kwargs

Decorators don't know the arguments of the function being decorated.

So we use:

``` python
def wrapper(*args, **kwargs):
```

Meaning:

\*args → tuple of positional arguments\
\*\*kwargs → dictionary of keyword arguments

Example:

    func(1,2,3)

    args = (1,2,3)
    kwargs = {}

Example:

    func(name="Ruchika", age=25)

    args = ()
    kwargs = {"name":"Ruchika","age":25}

------------------------------------------------------------------------

# 6. Correct Decorator Pattern

``` python
def decorator(func):

    def wrapper(*args, **kwargs):
        print("Before function")

        result = func(*args, **kwargs)

        print("After function")

        return result

    return wrapper
```

Example:

``` python
@decorator
def add(a,b):
    return a+b

print(add(2,3))
```

Output:

    Before function
    After function
    5

------------------------------------------------------------------------

# 7. If Wrapper Does Not Return Result

Bad decorator:

``` python
def wrapper(*args, **kwargs):
    func(*args, **kwargs)
```

Calling:

``` python
print(add(2,3))
```

Output:

    Before function
    After function
    None

Reason:

Wrapper didn't return the function result, so Python returned **None**.

------------------------------------------------------------------------

# 8. Decorator With Arguments

Example:

``` python
@repeat(3)
```

Implementation:

``` python
def repeat(n):

    def decorator(func):

        def wrapper(*args, **kwargs):
            for i in range(n):
                func(*args, **kwargs)

        return wrapper

    return decorator
```

Usage:

``` python
@repeat(3)
def greet():
    print("Hello")

greet()
```

Output:

    Hello
    Hello
    Hello

------------------------------------------------------------------------

# 9. Execution Flow of Decorator With Arguments

Code:

``` python
@repeat(3)
def greet():
```

Python converts this to:

    greet = repeat(3)(greet)

Flow:

    repeat(3)
       ↓
    returns decorator
       ↓
    decorator(greet)
       ↓
    returns wrapper
       ↓
    greet = wrapper

------------------------------------------------------------------------

# 10. Closure Concept Used in Decorators

The wrapper remembers variables from outer functions.

Example:

    repeat(n)
    decorator(func)
    wrapper()

Wrapper remembers:

    n
    func

This memory behavior is called **closure**.

------------------------------------------------------------------------

# 11. Decorator Mental Model

    repeat(n)
       ↓
    decorator(func)
       ↓
    wrapper(*args, **kwargs)

Wrapper typically performs:

    before logic
    call original function
    after logic
    return result

------------------------------------------------------------------------

# 12. Automation Framework Example

Logging decorator:

``` python
def log_test(func):

    def wrapper(*args, **kwargs):

        print(f"Start Test: {func.__name__}")

        result = func(*args, **kwargs)

        print(f"End Test: {func.__name__}")

        return result

    return wrapper
```

Usage:

``` python
@log_test
def test_login():
    print("Executing login test")
```

Output:

    Start Test: test_login
    Executing login test
    End Test: test_login
