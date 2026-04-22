# 🚀 Python Generators — Complete Interview Guide (Step-by-Step)

---

# 🔹 1. Why Generators?

### Problem with normal functions

```python
def get_numbers():
    return [1, 2, 3]
```

- Returns all values at once ❌
- Stores entire data in memory ❌

👉 Problem:
- Large datasets → memory issues

---

# 🔹 2. What is a Generator?

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

# 🔹 3. List vs Generator

| Feature | List | Generator |
|--------|------|----------|
| Memory | Stores all data | Lazy (one by one) |
| Keyword | return | yield |
| Execution | runs fully | pauses & resumes |

---

# 🔹 4. Execution Behavior

```python
def gen():
    print("start")
    yield 1
    print("middle")
    yield 2
    print("end")
```

### Flow:

- `g = gen()` → object created (no execution)
- `next(g)` → start → return 1 → pause
- `next(g)` → middle → return 2 → pause
- `next(g)` → end → StopIteration

---

# 🔹 5. yield vs next()

- `yield` → pause + return value
- `next()` → resume execution

---

# 🔹 6. Generator State

Generator stores:
- local variables
- execution position
- function state (execution frame)

---

# 🔹 7. Generator with Loop

```python
def gen(n):
    for i in range(n):
        yield i
```

```python
list(gen(3))  # [0, 1, 2]
```

---

# 🔹 8. Generator Exhaustion

```python
g = gen(3)
print(list(g))  # [0,1,2]
print(list(g))  # []
```

👉 Generators are single-use

---

# 🔹 9. Generator Expressions

```python
g = (i for i in range(3))
print(list(g))  # [0,1,2]
```

---

# 🔹 10. Partial Consumption

```python
g = (i*i for i in range(3))

print(next(g))   # 0
print(list(g))   # [1,4]
```

---

# 🔹 11. yield from

```python
def gen1():
    yield 1
    yield 2

def gen2():
    yield from gen1()
    yield 3

print(list(gen2()))  # [1,2,3]
```

👉 Works with any iterable

---

# 🔹 12. send()

```python
def gen():
    x = yield
    print(x)

g = gen()
next(g)
g.send(10)   # prints 10
```

---

# 🔹 13. close()

```python
g = gen()
next(g)
g.close()
next(g)  # StopIteration
```

---

# 🔹 14. throw()

```python
def gen():
    try:
        yield 1
    except ValueError:
        print("Error handled")

g = gen()
next(g)
g.throw(ValueError)  # Error handled
```

---

# 🔹 15. Memory Efficiency

```python
for i in gen(1000000):
    process(i)
```

✔️ Low memory (one by one)

```python
list(gen(1000000))
```

❌ High memory (all at once)

---

# 🔹 16. Final Combined Example (INTERVIEW)

```python
def process_logs(n):
    print("Generator started")

    for i in range(n):
        try:
            status = yield f"log-{i}"

            if status == "skip":
                print(f"Skipping log-{i}")

        except ValueError:
            print("Error handled inside generator")

    print("Generator finished")
```

### Usage

```python
g = process_logs(3)

print(next(g))          # log-0
print(g.send("skip"))   # skip log-0 → log-1
print(next(g))          # log-2

g.throw(ValueError)     # Error handled
g.close()
```

---

# 🎯 Final Interview Answer

> Generators are lazy, memory-efficient iterators that use `yield` to produce values one at a time, maintain execution state, and support advanced control via `send()`, `yield from`, `throw()`, and `close()`.

---

# 🚀 Key Takeaways

- Lazy evaluation
- Memory efficient
- Maintain state
- Single-use
- Powerful control mechanisms
