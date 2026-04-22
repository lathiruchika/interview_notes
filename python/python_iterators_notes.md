# Python Iterators & Iterables --- Clean Notes

------------------------------------------------------------------------

## 🔹 1. Iterable

### Definition

An **iterable** is an object that can return an iterator using `iter()`.

### Examples

-   list → `[1,2,3]`
-   tuple → `(1,2,3)`
-   string → `"hello"`
-   set → `{1,2,3}`
-   range → `range(5)`

### Key Points

-   Has `__iter__()`
-   Cannot use `next()` directly

``` python
lst = [1,2,3]
iter(lst)   # ✅ works
next(lst)   # ❌ error
```

------------------------------------------------------------------------

## 🔹 2. Iterator

### Definition

An **iterator** is an object that returns values one by one using
`next()`.

### Key Points

-   Has `__iter__()` and `__next__()`
-   Raises `StopIteration` when exhausted

``` python
lst = [10,20,30]
it = iter(lst)

print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30
print(next(it))  # StopIteration
```

------------------------------------------------------------------------

## 🔹 3. Iterable vs Iterator

  Feature   Iterable     Iterator
  --------- ------------ ------------------------
  Method    **iter**()   **iter**(), **next**()
  next()    ❌ No        ✅ Yes
  Usage     Collection   Value generator

------------------------------------------------------------------------

## 🔹 4. How for loop works

``` python
for i in lst:
    print(i)
```

Internally:

``` python
it = iter(lst)
next(it)
```

------------------------------------------------------------------------

## 🔹 5. Important Concepts

-   Iterator is also iterable
-   `iter(it) == it`
-   Iterator gets exhausted

------------------------------------------------------------------------

## 🔹 6. Custom Iterator Example

### 1. Numbers from 1 to n

``` python
class MyIterator:
    def __init__(self,n):
        self.n=n
        self.current=1

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.n:
            raise StopIteration
        value=self.current
        self.current+=1
        return value
```

------------------------------------------------------------------------

### 2. Even Numbers

``` python
class EvenIterator:
    def __init__(self,n):
        self.n=n
        self.current=2

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.n:
            raise StopIteration
        value=self.current
        self.current+=2
        return value
```

------------------------------------------------------------------------

### 3. Square Numbers

``` python
class SquareIterator:
    def __init__(self,n):
        self.n=n
        self.current=1

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.n:
            raise StopIteration
        value=self.current**2
        self.current+=1
        return value
```

------------------------------------------------------------------------

### 4. Fibonacci Iterator

``` python
class FibonacciIterator:
    def __init__(self,n):
        self.n=n
        self.a=0
        self.b=1
        self.current=0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.n:
            raise StopIteration
        value=self.a
        self.a, self.b = self.b, self.a + self.b
        self.current+=1
        return value
```

------------------------------------------------------------------------

## 🔹 7. Key Interview Points

-   `iter(obj)` → calls `obj.__iter__()`
-   `next(it)` → calls `it.__next__()`
-   Always return `self` in `__iter__()`
-   Iterator is one-time usable
-   Iterable can create multiple iterators

------------------------------------------------------------------------

## 🔹 8. Memory Advantage

Iterators are **memory efficient** because they generate values one at a
time instead of storing all values.

------------------------------------------------------------------------

## 🔹 Final Summary

-   Iterable = container
-   Iterator = value generator
-   Iterator = iterable + next()

------------------------------------------------------------------------

🚀 You are interview ready!
