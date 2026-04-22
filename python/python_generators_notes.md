   # 🧠 Python Generators — Clean Interview Notes

---

## 🔹 1. Why Generators?

### Problem with normal functions

```python
def get_numbers():
    return [1, 2, 3]
```

- Returns **all values at once**
- Entire data stored in **memory**

👉 Problem:
- Large data → high memory usage

---

## 🔹 2. Generator Concept

Generators give:
👉 **One value at a time (lazy evaluation)**

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
| Memory | Full loaded | Lazy (one by one) |
| Keyword | return | yield |
| Execution | runs fully | pauses & resumes |

---

## 🔹 4. Generator Execution Flow

```python
def gen():
    print("start")
    yield 1
    print("middle")
    yield 2
    print("end")
```

### Internal Flow:

1. `g = gen()`  
   → Only generator object created (NO execution)

2. `next(g)`  
   → start  
   → returns 1  
   → pauses

3. `next(g)`  
   → middle  
   → returns 2  
   → pauses

4. `next(g)`  
   → end  
   → StopIteration

---

## 🔹 5. Important Concepts

### yield
- Pauses execution
- Returns value

### next()
- Starts/resumes execution
- Continues from last paused state

### Generator stores:
👉 **Execution frame**
- Local variables
- Current position
- State of function

---

## 🔹 6. Key Interview Points

- Generator does NOT execute on creation
- Execution starts only when `next()` is called
- After last `yield` → remaining code runs → then StopIteration
- Memory efficient (lazy evaluation)

---

## 🔹 7. Mental Model

```
Generator = Pausable function

yield → pause + return value  
next() → resume from same point  
```
yield → pauses execution and returns a value
next() → resumes execution from last paused state
Generator stores → execution state (local variables + instruction pointer)
“Generator stores execution frame”

That includes:

local variables
current line position
call stack info

---

## 🚀 Summary

- Generators save memory
- Used for large data processing
- Core concept: **pause → resume → state preservation**
----------------------------------------------------------------
Why are generators memory efficient?
👉 “Generators are memory efficient because they generate values on demand instead of storing the entire dataset in memory.”
--------------------------------------------------------------------
🎯 Final Interview Answer (remember this)

👉 Say this confidently:

Generators are memory efficient because they produce values lazily (one at a time) instead of loading all values into memory at once.