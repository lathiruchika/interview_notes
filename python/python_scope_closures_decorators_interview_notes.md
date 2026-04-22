# 🚀 Python Interview Notes: Scope, Closures, Decorators & Memoization

---

# 🧠 1. LEGB Rule (Scope Resolution)

> Python resolves variables in order: **Local → Enclosing → Global → Built-in**

## ✅ Example
```python
x = 10

def func():
    print(x)

func()  # 10
```

### 🔑 Key Points
- Local → inside function
- Enclosing → outer function (closure)
- Global → module level
- Built-in → print, len

---

# 🔥 2. Local vs Global

## ✅ Local Variable
```python
x = 10

def func():
    x = 20
    print(x)

func()      # 20
print(x)    # 10
```

## ❗ UnboundLocalError
```python
x = 10

def func():
    print(x)
    x = 20

func()  # Error
```

### 🔑 Rule
> Assignment makes variable **local by default**

---

# 🌍 3. global Keyword

```python
x = 10

def func():
    global x
    x = 20

func()
print(x)  # 20
```

---

# 🔁 4. Mutable vs Immutable

## ✅ Works (mutable)
```python
x = []

def func():
    x.append(1)

func()
print(x)  # [1]
```

## ❌ Fails (reassignment)
```python
def func():
    x = x + [1]
```

### 🔑 Rule
> Modify object ✅ | Reassign ❌ (needs global)

---

# 🔒 5. Closures

## ✅ Example
```python
def outer():
    x = 10

    def inner():
        print(x)

    return inner

f = outer()
f()  # 10
```

### 🔑 Concept
> Inner function remembers enclosing variables

---

# 🔄 6. nonlocal Keyword

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 5

    inner()
    print(x)

outer()  # 15
```

---

# 🔥 7. Closure Trap (Loop)

```python
funcs = []

for i in range(3):
    def f():
        return i
    funcs.append(f)

print([f() for f in funcs])  # [2,2,2]
```

## ✅ Fix
```python
def f(i=i):
```

---

# 🎯 8. Decorators

> Modify function behavior without changing code

## ✅ Basic Decorator
```python
def deco(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper
```

---

# ⚙️ 9. Decorator with args

```python
def deco(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

---

# 🔁 10. Return Value Fix

```python
result = func(*args, **kwargs)
return result
```

---

# 🔗 11. Multiple Decorators

```python
@d1
@d2
def f(): pass
```

👉 Equivalent:
```python
f = d1(d2(f))
```

---

# 🧠 12. wraps (VERY IMPORTANT)

```python
from functools import wraps

@wraps(func)
```

### 🔑 Why?
- Preserves function name
- Avoids "wrapper" issue

---

# 🔁 13. Retry Decorator

```python
def retry(attempts=3):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for i in range(attempts):
                try:
                    return func(*args, **kwargs)
                except:
                    pass
            raise Exception("Failed")
        return wrapper
    return decorator
```

---

# 🧠 14. Memoization

> Cache function results

## ✅ Simple
```python
cache = {}

if args in cache:
    return cache[args]
```

## ✅ Decorator
```python
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        result = func(*args)
        cache[args] = result
        return result
    return wrapper
```

---

# 🔑 15. Memoization with kwargs

```python
key = (args, tuple(sorted(kwargs.items())))
```

---

# 🏗️ 16. Class vs Function Decorator

## Function
```python
@deco
def f(): pass
```

## Class
```python
@deco
class A: pass
```

👉 Equivalent:
```python
A = deco(A)
```

---

# 💥 FINAL INTERVIEW SUMMARY

- LEGB rule
- Assignment → local
- global / nonlocal usage
- Closure stores state
- Decorators wrap functions
- Use wraps ALWAYS
- Retry & memoization in automation

---

# 🚀 GOLDEN LINE

> "Python uses LEGB for scope, closures preserve enclosing variables, and decorators wrap functions to extend behavior without modifying original code."

