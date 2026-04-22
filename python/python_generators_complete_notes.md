# 🚀 Python Generators — Complete Interview Notes (Step-by-Step)

---

## 🔹 1. Why Generators?

### Problem with normal functions

```python
def get_numbers():
    return [1, 2, 3]
```

- Returns all values at once
- Stores entire data in memory ❌

👉 Problem:
- Large datasets → memory issues

---

## 🔹 2. What is a Generator?

👉 A generator is a function that:
- Produces values one at a time
- Uses `yield` instead of `return`

```python
def gen_numbers():
    yield 1
    yield 2
    yield 3
```

---

## 🔹 3. List vs Generator

| Feature | List | Generator |
|--------|------|----------|
| Memory | Stores all data | Lazy (one by one) |
| Keyword | return | yield |
| Execution | runs fully | pauses & resumes |

---

## 🔹 4. Execution Behavior

```python
def gen():
    print("start")
    yield 1
    print("middle")
    yield 2
    print("end")
```

### Flow:

1. `g = gen()` → only object created (no execution)
2. `next(g)` → start → return 1 → pause
3. `next(g)` → middle → return 2 → pause
4. `next(g)` → end → StopIteration

---

## 🔹 5. yield vs next()

- `yield` → pause + return value
- `next()` → resume from last state

---

## 🔹 6. Generator State (Important)

Generator stores:
- local variables
- execution position
- function state

👉 Called: **execution frame**

---

## 🔹 7. Generator with Loop

```python
def gen(n):
    for i in range(n):
        yield i
```

Example:

```python
g = gen(3)
print(list(g))
```

Output:
```
[0, 1, 2]
```

---

## 🔹 8. list() Behavior

```python
list(g)
```

👉 Internally:
- Calls `next()` repeatedly
- Stops at StopIteration

---

## 🔹 9. Generator Exhaustion

```python
g = gen(3)
print(list(g))  # [0,1,2]
print(list(g))  # []
```

👉 Generators are:
- single-use
- cannot be reused

---

## 🔹 10. Key Interview Points

- Generator does NOT execute on creation
- Execution starts only on `next()`
- After last yield → remaining code runs → StopIteration
- Memory efficient (lazy evaluation)
- Single-use iterator

---

## 🔹 11. Generator with Condition

```python
def even_gen(n):
    for i in range(n+1):
        if i % 2 == 0:
            yield i
```

Example:

```python
list(even_gen(6))
```

Output:
```
[0, 2, 4, 6]
```

---

## 🔹 12. Mental Model

```
Generator = Pausable function

yield → pause + return
next() → resume
```

---

## 🔹 13. Real-world Use Cases

- Large API responses
- Log processing
- File reading
- Streaming data

---

## 🔹 14. Final Summary

- Generators save memory
- Work lazily
- Maintain state
- Used for large data handling
- Important for interviews

---

## 🎯 Interview One-Liner

👉 "Generators are memory-efficient iterators that produce values lazily using yield, maintaining state between iterations."
