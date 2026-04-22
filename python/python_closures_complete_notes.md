# Python Closures -- Complete Notes (Interview + Practical Understanding)

## 1. What is a Closure?

A **closure** is a function that **remembers variables from its
enclosing scope even after the outer function has finished executing**.

In simple terms:

> A closure = inner function + remembered variables from outer function.

------------------------------------------------------------------------

## 2. Basic Closure Example

``` python
def outer(msg):

    def inner():
        print(msg)

    return inner


hello = outer("Hello")
hello()
```

### Output

    Hello

### Why?

When `outer()` runs:

    msg = "Hello"

The function `inner()` **remembers this value** even after `outer()`
finishes.

So the returned function carries the variable with it.

Conceptually:

    hello → inner + msg="Hello"

------------------------------------------------------------------------

## 3. Multiple Closures Example

``` python
def outer(msg):

    def inner():
        print(msg)

    return inner


hello = outer("Hello")
bye = outer("Bye")

hello()
bye()
```

### Output

    Hello
    Bye

### Why this works

Each call to `outer()` creates **a new closure environment**.

    hello → inner + msg="Hello"
    bye   → inner + msg="Bye"

------------------------------------------------------------------------

## 4. Closure Inside Loops (Common Interview Question)

``` python
funcs = []

for i in range(3):
    def show():
        print(i)
    funcs.append(show)

for f in funcs:
    f()
```

### Output

    2
    2
    2

### Why?

Python uses **late binding**.

Closures capture **variables**, not values.

All functions reference the same variable `i`, whose final value
becomes:

    i = 2

------------------------------------------------------------------------

## 5. Fixing the Loop Closure Problem

``` python
funcs = []

for i in range(3):
    def show(i=i):
        print(i)
    funcs.append(show)

for f in funcs:
    f()
```

### Output

    0
    1
    2

### Why?

    i=i

captures the **current value of `i` as a default parameter**.

Each function stores its own value.

------------------------------------------------------------------------

## 6. Lambda Closure Example

``` python
funcs = []

for i in range(3):
    funcs.append(lambda: print(i))

for f in funcs:
    f()
```

### Output

    2
    2
    2

Again, **late binding** occurs.

All lambdas reference the same variable `i`.

------------------------------------------------------------------------

### Fixed Version

``` python
funcs = []

for i in range(3):
    funcs.append(lambda i=i: print(i))

for f in funcs:
    f()
```

### Output

    0
    1
    2

------------------------------------------------------------------------

## 7. Closure vs Global (LEGB Rule)

``` python
x = 10

def outer():
    x = 20

    def inner():
        print(x)

    return inner

f = outer()
f()
```

### Output

    20

### Why?

Python searches variables using **LEGB rule**:

    Local
    Enclosing
    Global
    Built-in

The value `x=20` exists in the **enclosing scope**, so it is used.

------------------------------------------------------------------------

## 8. Closure Memory Concept

Closures store variables in:

    function.__closure__

Example:

``` python
def outer(x):

    def inner():
        print(x)

    return inner


f = outer(10)

print(f.__closure__)
```

This shows the captured variable stored in the closure.

------------------------------------------------------------------------

## 9. Why Closures Are Important

Closures are used in:

• Decorators\
• Function factories\
• Functional programming\
• Callbacks\
• Data hiding

------------------------------------------------------------------------

## 10. Closures in Decorators

Decorators rely on closures.

Example:

``` python
def decorator(func):

    def wrapper():
        print("Before")
        func()
        print("After")

    return wrapper


@decorator
def say_hi():
    print("Hi")

say_hi()
```

### Output

    Before
    Hi
    After

Here:

    wrapper

remembers `func` using a closure.

------------------------------------------------------------------------

# Final Mental Model

    Closure =
        Inner Function
        +
        Variables from Enclosing Scope

Example memory structure:

    inner
       │
       ▼
    closure → msg = "Hello"

------------------------------------------------------------------------

# Key Interview Rules

1.  Closures **capture variables, not values**
2.  Python uses **late binding**
3.  Use **default arguments to capture current value**
4.  Closures store data in `__closure__`
5.  Decorators are built using closures

------------------------------------------------------------------------

# One-Line Definition (Interview)

> A closure is a function that remembers variables from its enclosing
> scope even after that scope has finished execution.
